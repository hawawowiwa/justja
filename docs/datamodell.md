# Justja – datamodell (Firestore)

Datamodellen byggs i byggsteg 1 men är gjord för hela appen: delning med sambon (steg 7) och privat Hjärta ska fungera utan att datan behöver göras om. Fält för senare steg är markerade med *(steg N)* och behöver inte finnas i steg 1.

## Översikt

```
users/{uid}                  en per person: profil och inställningar
categories/{categoryId}      kategorier = listor, även Övrigt och Hjärta
tasks/{taskId}               alla uppgifter, privata och delade
```

**Grundidé:** varje kategori och uppgift har `ownerId` (den som skapade den) och `memberIds` (alla som får se den). En privat sak har `memberIds = [ownerId]`. En delad sak får sambons uid i `memberIds` *(steg 7)*. Appen hämtar allt med en fråga: `where('memberIds', arrayContains: uid)`.

**Hjärta** har `isHeart: true`. Säkerhetsreglerna tillåter då bara `memberIds == [ownerId]`, så Hjärta kan aldrig delas, även om appen skulle ha en bugg.

## users/{uid}

| Fält | Typ | Beskrivning |
| --- | --- | --- |
| displayName | string | Namn från Google |
| email | string | E-post från Google |
| createdAt | timestamp | Första inloggningen |
| onboardingDone | bool | Har valt startkategorier |
| settings | map | Se nedan |
| categoryPrefs | map | `{categoryId: {order: int, showInFeed: bool}}`. Per person, så att ordning och flödesval inte påverkar sambon |
| partnerUid | string? | *(steg 7)* sambons uid |

`settings`:

| Nyckel | Typ | Standard | Steg |
| --- | --- | --- | --- |
| theme | `system` / `fjord` / `kvall` | `system` | 1 |
| mustOnTop | bool | false | 1 |
| sortMode | `time` / `category` / `priority` | `time` | 2 |
| escalation | bool | true | 2 |
| *övriga* | | | läggs till i respektive steg |

## categories/{categoryId}

| Fält | Typ | Beskrivning |
| --- | --- | --- |
| ownerId | string | Skaparens uid |
| memberIds | string[] | Vilka som ser kategorin |
| name | string | T.ex. "Sysslor" |
| letter | string | 1–2 tecken, t.ex. "S" eller "Sa" |
| color | string | Prickfärgen, en av de 12 färgerna (hex) |
| system | string? | `ovrigt`, `hjarta` eller null. Systemkategorier kan inte tas bort, och Övrigt kan inte byta namn |
| isHeart | bool | true bara för Hjärta |
| createdAt, updatedAt | timestamp | |

Vid första inloggningen skapas **Övrigt** och **Hjärta** alltid, plus de förvalda kategorier man bockat i (Sysslor, Jobb, Barnen, Sambo, Jag). Färger och bokstäver finns i specen.

## tasks/{taskId}

| Fält | Typ | Beskrivning |
| --- | --- | --- |
| ownerId | string | Skaparens uid |
| memberIds | string[] | Vilka som ser uppgiften |
| title | string | Enda obligatoriska fältet |
| categoryId | string | Saknas kategori: Övrigts id |
| isHeart | bool | Kopia från kategorin, för säkerhetsreglerna |
| heartType | `blue` / `red` / null | Blått = jag, rött = relationen *(steg 6)* |
| priority | `kanVanta` / `vanlig` / `prio` | Vald prio. Standard `vanlig` |
| must | bool | Måste-markeringen, ovanpå prion |
| date | string? | `YYYY-MM-DD`. Det datum uppgiften är planerad till |
| time | string? | `HH:mm`, eller null för uppgifter utan tid |
| status | `open` / `done` | |
| doneAt | timestamp? | När den bockades av |
| doneBy | string? | Vem som bockade av *(används från steg 7)* |
| postponeCount | int | Antal medvetna uppskjutningar (swipe höger eller nytt datum). Nollställs när uppgiften görs |
| createdAt, updatedAt | timestamp | |
| assignedTo | string? | *(steg 7)* |
| recurrence | map? | *(steg 2)* upprepningsregel och borttagna tillfällen |
| subtasks | list? | *(steg 4)* `[{id, title, done}]` |
| reminder | map? | *(steg 3)* tyst, ljud eller alarm, och tider |
| placeId | string? | *(steg 8)* |
| calendarSync | bool | *(steg 9)* |

### Glömda uppgifter och prio som stiger

- En uppgift är **glömd** när `status == open` och `date` är före idag. Den visas i Idag.
- Prion som visas **räknas fram** och sparas inte: vald prio plus en nivå per dag sedan `date`, som mest `prio`. Är `settings.escalation` av visas vald prio.
- "Har legat i 5 dagar" räknas också från `date`.
- **Medvetet uppskjuten** (swipe höger eller nytt datum): `date` sätts till det nya datumet och `postponeCount` ökar med 1. Prion börjar då om från vald prio.
- Hjärta-uppgifter och platsuppgifter blir aldrig glömda och stiger inte i prio.

Logiken räknas fram i steg 2. I steg 1 räcker det att fälten finns.

## Säkerhetsregler (utkast för steg 1)

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    function signedIn() {
      return request.auth != null;
    }

    function isMember(data) {
      return signedIn() && request.auth.uid in data.memberIds;
    }

    // Hjärta får bara ha ägaren som medlem
    function heartIsPrivate(data) {
      return data.get('isHeart', false) == false
        || data.memberIds == [data.ownerId];
    }

    // Steg 1: bara ägaren. Steg 7 utökar till ägaren + partnerUid.
    function validMembers(data) {
      return data.memberIds == [data.ownerId];
    }

    match /users/{uid} {
      allow read, write: if signedIn() && request.auth.uid == uid;
    }

    match /categories/{id} {
      allow read: if isMember(resource.data);
      allow create: if signedIn()
        && request.resource.data.ownerId == request.auth.uid
        && validMembers(request.resource.data)
        && heartIsPrivate(request.resource.data);
      allow update: if isMember(resource.data)
        && request.resource.data.ownerId == resource.data.ownerId
        && request.resource.data.get('isHeart', false) == resource.data.get('isHeart', false)
        && request.resource.data.get('system', null) == resource.data.get('system', null)
        && validMembers(request.resource.data)
        && heartIsPrivate(request.resource.data);
      allow delete: if signedIn()
        && resource.data.ownerId == request.auth.uid
        && resource.data.get('system', null) == null;
    }

    match /tasks/{id} {
      allow read: if isMember(resource.data);
      allow create: if signedIn()
        && request.resource.data.ownerId == request.auth.uid
        && validMembers(request.resource.data)
        && heartIsPrivate(request.resource.data);
      allow update: if isMember(resource.data)
        && request.resource.data.ownerId == resource.data.ownerId
        && validMembers(request.resource.data)
        && heartIsPrivate(request.resource.data);
      allow delete: if isMember(resource.data);
    }
  }
}
```

Reglerna ligger i `firestore.rules` i repot och laddas upp med `firebase deploy --only firestore:rules`. Testa dem gärna med Firebase-emulatorn. Allt som inte uttryckligen tillåts är förbjudet.

## Index

Frågan på `memberIds` (array-contains) kombinerad med sortering på `date` kan kräva ett sammansatt index. Firestore skriver då ut en länk i felmeddelandet som skapar indexet. Lägg in det i `firestore.indexes.json`.
