# Byggsteg 1: Grund

Målet med steg 1 är en enkel men riktig app att använda varje dag: logga in, se dagens uppgifter, lägga till, bocka av och skjuta upp. Allt sparas i molnet. Detaljerna står i `docs/spec.md`. Skärmbilderna finns i `docs/design/` (01-inloggning till 15-installningar, i Fjord och Kväll), och `docs/design/LASMIG.md` beskriver dem.

## Ingår

1. **Projektgrund**
   - Flutter-projekt för Android och webb, kopplat till Firebase (redan gjort med `flutterfire configure`)
   - Mappstruktur, tema och navigation
   - Färgskalorna Fjord och Kväll med alla färger från specen. Typsnitten Inter och Baloo 2 buntade i appen
   - Appikonen från `assets/brand/justja-ikon.svg` via `flutter_launcher_icons`, och startbilden (ikonen i mitten, litet ordmärke längst ner)

2. **Inloggning och lagring**
   - Inloggningsskärm med ikonen, ordmärket, undertexten "Justja! – och sen glömmer du det inte." och knappen "Fortsätt med Google"
   - Firestore enligt `docs/datamodell.md`, med säkerhetsreglerna i `firestore.rules`
   - Offline: appen fungerar utan nät och synkar sedan
   - Loggar man in på en ny telefon finns allt kvar, även inställningarna

3. **Första start**
   - Föreslagna kategorier, förbockade: Sysslor, Jobb, Barnen, Sambo, Jag. Man kan bocka ur och lägga till en egen
   - Övrigt och Hjärta skapas alltid

4. **Idag-listan**
   - Datumraden: "Torsdag 5 nov · 9 kvar"
   - Uppgifter med tid i tidsordning, sist de utan tid. Glömda uppgifter (datum före idag, ej klara) visas i Idag
   - Uppgiftsraden: ring i prioritetens färg (tunnare ju lägre prio), kategoriprick med bokstav, toning mot kategorifärgen till höger, Måste-markering
   - Klara uppgifter blir överstrukna och ligger kvar resten av dagen
   - Kategoriknapparna till vänster syns. Filtrering är steg 2, men Alla-knappen kan finnas
   - Periodknapparna överst syns, men bara Idag fungerar. Övriga gråas med "Senare steg"
   - Hjärtat och inköpsknappen syns men är gråade med "Senare steg"
   - Tom lista: "Allt klart för idag" med antal avbockade. Första gången visas tipset "handla mjölk imorgon 17" (själva tolkningen kommer i steg 4)

5. **Lägg till och Redigera**
   - Lägg till-knappen nere till höger
   - Bara titeln krävs. Kategori, prio (Kan vänta, Vanlig, Prio, Måste), datum och tid syns direkt. Ingen kategori = Övrigt. Standard är Vanlig och idag
   - "Fler val" kan finnas som gråad rad med "Senare steg"
   - Redigera: samma fält, plus när uppgiften skapades och antal uppskjutningar. "Ta bort uppgiften" längst ner

6. **Swipe och ångra**
   - Swipe vänster: Klar (grönt med bock). Swipe höger: Imorgon (blått). På en klar uppgift gör swipe höger den öppen igen
   - Imorgon räknas som medveten uppskjutning: `postponeCount` ökar och prion behålls
   - Ångra-raden längst ner i ca 5 sekunder efter swipe och borttagning. Lägg till-knappen flyttar upp så länge den syns

7. **Kategorier**
   - I Inställningar: lista där man drar för att ändra ordning. Ett tryck öppnar ett blad med namn, bokstav (1–2 tecken), 12 färger, Visa i flödet och Dela med sambo
   - Dela med sambo visas men är gråad till steg 7. Den visas aldrig för Hjärta
   - Övrigt kan inte tas bort eller byta namn, men färg och bokstav kan ändras
   - Ta bort kategori: dialogen Flytta till Övrigt, Ta bort uppgifterna också, Avbryt. Därefter ångra-raden

8. **Inställningar i steg 1**
   - Konto, Färgskala (Följ telefonen, Fjord, Kväll), Kategorier, Listor i flödet, Måste överst (av som standard), Logga ut
   - Inställningar för senare steg syns gråade med märket "Senare steg"
   - Litet ordmärke med versionsnummer längst ner

## Ingår inte (senare steg)

Prio som stiger av sig själv, upprepning, 3 dagar, Vecka, Månad, sortering, filter, historik (steg 2) · notiser och alarm (steg 3) · snabbinmatning, röst, delmoment (steg 4) · widget och fast notis (steg 5) · Hjärtas förslag och veckogenomgång (steg 6) · delning och inköpslista (steg 7) · platser (steg 8) · Google Kalender (steg 9).

Datamodellen ska ändå ha plats för dem enligt `docs/datamodell.md`.

## Klart när

- [ ] Appen startar på Hannes Android-telefon med rätt ikon och startbild
- [ ] Google-inloggning fungerar på telefonen och i webbläsaren (`flutter run -d chrome`)
- [ ] Första start skapar valda kategorier plus Övrigt och Hjärta
- [ ] En uppgift med bara titel hamnar idag i Övrigt med prion Vanlig
- [ ] Uppgifter sorteras: med tid i tidsordning, sist de utan tid
- [ ] Swipe vänster, swipe höger och ångra fungerar
- [ ] Redigera och ta bort fungerar, med ångra
- [ ] Kategorier kan skapas, ändras, sorteras och tas bort. Övrigt och Hjärta kan inte tas bort
- [ ] Fjord, Kväll och Följ telefonen fungerar
- [ ] Appen fungerar i flygplansläge och synkar när nätet kommer tillbaka
- [ ] Avinstallera, installera igen och logga in: allt finns kvar
- [ ] Säkerhetsreglerna är uppladdade. Ett försök att läsa en annan användares data nekas
- [ ] `flutter analyze` utan fel och testerna går igenom
- [ ] `flutter build web` fungerar

## Förslag på ordning

1. Projektgrund, tema och ikon
2. Inloggning och första start
3. Idag-listan med uppgifter från Firestore
4. Lägg till och Redigera
5. Swipe och ångra
6. Kategorier och Inställningar
7. Säkerhetsregler, offline och slutkontroll

Visa en plan, bygg en del i taget och låt Hannes testa på telefonen efter varje del.
