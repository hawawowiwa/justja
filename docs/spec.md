# Justja – idé

Nov 3, 2026 · @Hannes

## Syfte

En påminnelseapp för mig och min sambo. Viktigast: det ska vara **lätt att se vad som ska göras** och man ska **bli påmind**. Inget ska försvinna av sig självt.

**Grundregel:** nya funktioner ska alltid gå att stänga av i Inställningar. Det gäller även funktioner som läggs till senare.

## Namn och logga

Appen heter **Justja**, från "just ja!", det man säger när man plötsligt kommer på något. I loggan skrivs det **justja** med små bokstäver. I löptext skrivs namnet alltid ihop, även som utrop, t.ex. "Justja! Vad kom du på?" (beslutat 8 nov). Ingen app med namnet Justja eller "Just ja" hittades vid en koll 8 nov 2026. Närmast är engelska appar som "Just Reminder", där "just" betyder "endast", så de är inte förväxlingsbara.

Vald logga (8 nov 2026): **"Baloo 2 · ljus med ram"** på [designytan för loggan](https://claude.ai/artifact/Fy78cgeGbCRxqZbfbeCUtU). Övriga förslag ligger kvar där som historik.

### Appikon

- Vit bakgrund (#FFFFFF), rundad kvadrat
- **Smal mörkblå ram** längs kanten (#121A24)
- Ett litet **j** i mörkblått (#1B2733) med rundade ändar
- **Pricken på j:et är en stor orange ring** (#F08A3E, samma orange som prionivån Prio). Ringen är det man ska känna igen loggan på, även i små storlekar

### Namnet (ordmärket)

- **justja** i typsnittet **Baloo 2**, fetstil (700)
- **Det första j:et har den orange ringen** i stället för prick, ritad som i ikonen. Det andra j:et har vanlig prick
- Mörkblått (#1B2733) på ljus bakgrund, ljust (#F3F6F8) på mörk bakgrund. Ringen är orange i båda
- Baloo 2 är gratis (Google Fonts, SIL Open Font License)

### Ikonen som SVG

```svg
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <rect x="1.5" y="1.5" width="97" height="97" rx="21" fill="#FFFFFF" stroke="#121A24" stroke-width="3"/>
  <path d="M56 46 V68 Q56 84 40 84" fill="none" stroke="#1B2733" stroke-width="13" stroke-linecap="round"/>
  <circle cx="56" cy="24" r="10" fill="none" stroke="#F08A3E" stroke-width="6.5"/>
</svg>
```

### I bygget

- Appikonen för Android tas fram från SVG:n, t.ex. med flutter_launcher_icons. Samma bild används som hemskärmsikon för webbappen på iPhone. Görs i **byggsteg 1**
- Var loggan syns i appen (beslutat 8 nov): ikonen och ordmärket centrerade på inloggningsskärmen, med undertexten "Justja! – och sen glömmer du det inte.". Startbilden visar ikonen i mitten och ett litet ordmärke längst ner. Notisikonen är ett vitt j med den orange ringen, och avsändaren i notiser heter Justja. Längst ner i Inställningar sitter ett litet ordmärke med versionen under. Namnet används i texter, t.ex. "Justja! Vad kom du på?" i fältet i Lägg till och i tipset första gången. Loggan och ringen används inte i listorna, eftersom en orange ring redan betyder glömd i vecko- och månadsöversikten

## Kategorier

- Egna kategorier som man lägger till själv, t.ex. **Sysslor** (städ, handla), **Jobb**, **Barnen**, **Sambo**, **Jag**
- Kategorin syns som färg/ikon på varje uppgift
- Varje kategori har en **bokstav** i en helfärgad prick med vit text. Förvalet är första bokstäven i namnet, men man kan välja själv när kategorin skapas. Krockar bokstäven med en annan kategori blir det **två bokstäver**, t.ex. "Sa" för Sambo och "Ja" för Jag. Pricken använder en lite mörkare nyans av kategorifärgen så att den vita bokstaven syns
- **Övrigt:** väljer man **ingen kategori** hamnar uppgiften i Övrigt. Det gäller alla uppgifter, oavsett hur de skapas (Lägg till, snabbinmatning, röst eller import)
- Övrigt är en **fast kategori** som alltid finns och inte kan tas bort. Den **kan inte byta namn**, men **färgen och bokstaven kan ändras** (förval "Ö")
- **Ta bort en kategori:** har kategorin uppgifter frågar appen om man vill **ta bort alla uppgifter i kategorin** eller **flytta dem till Övrigt**. Saknar den uppgifter tas den bort direkt. Efter borttagningen visas ångra-raden längst ner, som efter en swipe

## Listor

Varje kategori är en lista, t.ex. Sysslor, Jobb och Hjärta. Delning och kalender kan väljas både för en enskild uppgift och för en hel lista.

- **En uppgift:** man kan välja att lägga den i **Google Kalender** och att **skicka den till sambon** (dela den)
- **En hel lista:** man kan välja att **dela hela listan** med sambon och att **synka hela listan** till Google Kalender. Då gör **allt nytt** i listan det automatiskt. En enskild uppgift i listan kan ändå stängas av
- När man slår på delning eller kalender för en lista som redan har uppgifter frågar appen om de befintliga också ska med
- **Hjärta** kan aldrig delas med sambon, varken som lista eller uppgift. Den kan synkas till kalendern med neutral titel
- **Listor i flödet:** i Inställningar väljer man vilka listor som visas i flödet (Idag, 3 dagar och Vecka). **Alla visas som standard**, och man bockar ur de man inte vill ha där, t.ex. Hjärta. En urbockad lista nås fortfarande via sin kategoriknapp, och Hjärta via hjärtat

## Hjärta

Hjärta är en egen kategori för att ta hand om sig själv och sin relation. Den ger **förslag, inte måsten**.

Hjärta är **privat** och delas aldrig med sambon.

- **Blått hjärta:** jag och mitt eget välmående
- **Rött hjärta:** henne och relationen
- Man kan lägga in **specifika saker med datum**
- Man kan också lägga in saker som appen **sätter ut slumpmässigt**, t.ex. "överraska med blommor"
- Gör man inte en Hjärta-uppgift **flyttas den inte vidare** till nästa dag och stiger inte i prio
- I listan har Hjärta-förslag en **pulserande bakgrund som ett hjärtslag**. Den ska vara subtil och inte ta fokus från de viktiga uppgifterna
- I Inställningar kan man välja att **inte visa Hjärta i listan**. Då ser man förslagen bara i Hjärta-menyn
- **Må bra i vardagen** är en del av blått hjärta, inte en egen funktion. Idébanken fylls på med vardagsförslag, t.ex. sträcka på benen, dricka vatten och en kort promenad
- **Små vardagspåminnelser:** blått hjärta kan också ge en liten påminnelse under dagen, t.ex. en bensträckare på eftermiddagen, utöver de slumpade förslagen. Slås på i Inställningar och är **avslaget som standard**

### Slumpade förslag

- **Frekvens:** 1–2 förslag i veckan
- **Nivå 1–3** efter hur lätt förslaget är att göra:
  - **1** = lätt och kan göras ofta, t.ex. säga "Jag älskar dig"
  - **2** = kräver lite planering
  - **3** = svårt att ordna, t.ex. överraska med restaurangbesök
- **Källor:** egna förslag plus en färdig idébank från Claude, anpassad efter vad vi gillar. Idébanken byggs in i appen och fylls på via chatten med Claude, så det kostar inget extra. Automatiska AI-förslag via API kan läggas till senare
- **Livssituation att ta hänsyn till:** ett barn på 8 år och ett på 11 veckor
- **Upprepning:** samma förslag får komma igen, men man kan ta bort ett förslag så att det aldrig kommer tillbaka

Forskningen stödjer upplägget: små saker som görs ofta betyder mest för en relation, och de flesta par blir mindre nöjda med relationen de första åren efter ett barn ([Gottman](https://www.gottman.com/blog/the-little-things-that-keep-love-strong/), [Psychology Today](https://psychologytoday.com/sg/blog/couples-thrive/202109/research-shows-these-two-things-keep-new-parents-happy)).

### Idébank (start)

| Förslag | Hjärta | Nivå |
| --- | --- | --- |
| Säg "Jag älskar dig" utan anledning | Rött | 1 |
| Skicka ett kärleksfullt sms mitt på dagen | Rött | 1 |
| En lång kram eller kyss när ni ses efter jobbet | Rött | 1 |
| Ta nattmatningen eller morgonen så hon får sova | Rött | 1 |
| Fråga hur hon mår, och lyssna utan att lösa | Rött | 1 |
| Gör en syssla hon brukar göra, utan att säga något | Rött | 1 |
| Ta med henne på en promenad med vagnen, bara ni | Rött | 2 |
| Ge henne en egen kväll eller förmiddag för sig själv | Rött | 2 |
| Hemmadejt efter att barnen somnat, telefonerna undan | Rött | 2 |
| Överraska med blommor | Rött | 2 |
| Ordna barnvakt och överraska med restaurang | Rött | 3 |
| Gå och lägg dig i tid | Blått | 1 |
| Tio minuter ute i dagsljus | Blått | 1 |
| Träna eller rör på dig en stund | Blått | 2 |
| Egen tid med 8-åringen, bara ni två | Blått | 2 |
| En halvdag för en egen hobby, t.ex. fiske | Blått | 3 |
| Sträck på benen en stund | Blått | 1 |
| Drick ett glas vatten | Blått | 1 |
| En kort promenad | Blått | 1 |

## Startvy: Idag

- En lista med det som ska göras idag, sorterad efter tid och datum (se Sortering nedan)
- Klara uppgifter blir **överstrukna** och ligger kvar resten av dagen
- Klara uppgifter följer **inte** med till nästa dag, men allt sparas i en **historik** man kan kolla tillbaka i
- Ordningen i Idag: uppgifter **med tid** i tidsordning och sist de **utan tid**

### Sortering och hur långt fram

- **Standard: sorterat efter tid och datum.** Man kan välja att sortera efter kategori eller prio i stället. Måste ligger inte först som standard
- **Prion syns snyggt** på varje uppgift, t.ex. med färg eller markering
- Man väljer **hur många dagar framåt** startvyn visar, t.ex. idag, 3 dagar eller hela veckan
- Visas flera dagar får **varje dag en rubrik** med dag och datum, t.ex. "Imorgon" eller "Lördag 7 nov"

### Kalendervy

- En längre översikt i en kalendervy som visar **hela veckor eller månader**
- **Veckonummer** står utskrivna
- Varje dag visar **prickar i kategorifärgerna**. Dagar med Prio eller Måste får **bakgrunden tonad i prioritetens färg** längst upp. En **orange ring** sitter bara på idag, när dagen har glömda uppgifter (de flyttas ju alltid vidare till idag), och en **ljusblå ring** betyder en delad uppgift. Har dagen både och syns den blå ringen innanför den orange
- **Trycker man på en dag** visas dagens uppgifter i en lista under kalendern. Därifrån kan man lägga till en ny uppgift på den dagen

### Historik

- **I vecko- och månadsöversikten:** sveper man bakåt i tiden ser man vilka uppgifter som gjordes. Det är det enklaste sättet att titta tillbaka
- **Min historik** i Inställningar: alla gjorda uppgifter i en lista, ordnade efter datum

## Prioritet

- **Tre nivåer plus Måste.** Man väljer mellan Kan vänta, Vanlig, Prio och Måste direkt när uppgiften skapas. Standard är Vanlig. Sänk till Kan vänta om det inte spelar så stor roll, höj till Prio om det är viktigt och välj Måste om det är ett måste
- En **glömd** uppgift ligger kvar till nästa dag och går upp en nivå per dag, som mest till Prio. Priohöjningen kan stängas av i Inställningar. Då behåller glömda uppgifter sin prio men flyttas fortfarande vidare till idag
- På högsta nivån visar uppgiften **hur länge den legat**, t.ex. "5 dagar"
- En **medvetet uppskjuten** uppgift (swipe höger eller nytt datum) behåller sin prio
- Inget tas någonsin bort automatiskt

## Måste

En uppgift kan markeras som **Måste**. Den ska verkligen göras samma dag.

- Måste är en **egen markering ovanpå prion**. Den väljs i samma prioval som Kan vänta, Vanlig och Prio, men fungerar som en egen markering: glömda uppgifter stiger som mest till Prio och blir aldrig Måste av sig själva. Som standard sorteras Måste som andra uppgifter. Med valet Måste överst i Inställningar läggs de först i listorna
- Görs den inte flyttas den vidare till nästa dag, som andra glömda uppgifter
- **Påminnelser som standard, och både hur ofta och när kan ändras i Inställningar:**
  - **Utan tid:** kl. 09, 12, 15 och 18.30
  - **Med tid:** 1 timme före, 10 minuter före, 10 minuter efter och kl. 18.30
- **Sen tid:** är tiden satt senare än 18.30 följer alla påminnelser tiden, och 18.30 hoppas över
- **Nästa dag:** en Måste-uppgift som flyttas vidare är fortfarande Måste
- **Vid upplåsning:** en notis ligger kvar på låsskärmen tills uppgiften är gjord, och uppgiften visas direkt när man låser upp. Båda kan stängas av och sättas på i Inställningar
- **Sambon (pausad):** sambon får en påminnelse kl. 18.30 om uppgiften inte är gjord. Det kräver troligen Firebase Blaze (betalkort, i praktiken 0 kr). Beslut tas vid byggsteg 7

## Återkommande uppgifter

- Uppgifter kan upprepas med intervall, t.ex. "tvätta varje söndag"
- Ligger den kvar när nästa tillfälle kommer markeras den tydligt som **dubbelt påmind**
- När man gör den försvinner alla missade tillfällen samtidigt (gäller bara uppgifter med intervall)
- **Upprepning väljs väldigt fritt**, t.ex.:
  - varje dag, varannan dag eller var X:e dag
  - varje vardag eller varje helg
  - vissa veckodagar, t.ex. onsdag och fredag, varje vecka, varannan vecka osv.
  - varje månad
  - **helt egna dagar** som man sätter ut i en kalendervy
- **Ta bort ett enskilt tillfälle:** är uppgiften satt till varje torsdag kan man gå in och ta bort en specifik torsdag, t.ex. vecka 51, utan att resten påverkas

## Delmoment

En uppgift kan ha en checklista med delmoment, t.ex. "Packa till BVC" med blöjor, extrakläder och journal.

### Klar

- **När sista delmomentet bockas av blir uppgiften klar automatiskt**, utan fråga. Ångra-raden ("Klar · Ångra") visas längst ner som vanligt
- **Swipe vänster** på en uppgift med delmoment som inte är klara **bockar av alla delmoment** och markerar uppgiften klar. Ångra-raden tar tillbaka allt

### I listan

- **Räknare på raden**, t.ex. "2/5"
- **Ett tryck på räknaren fäller ut delmomenten** under uppgiften, så man kan bocka av direkt i listan
- **Prio-ringen fylls** som en tårtbit i takt med att delmomenten bockas av, och behåller prioritetens färg och tjocklek. Ringen och räknaren visas tillsammans (beslutat 7 nov, variant 3 på designytan). I veckoöversikten visas en liten fylld ring och t.ex. "2/3"

### Lägga till

- Under "Fler val" i Lägg till: skriv ett delmoment, tryck Enter, och nästa rad kommer direkt
- Ordningen ändras genom att dra delmomenten
- **Inget eget datum eller tid på delmoment.** Behöver ett delmoment en egen tid är det en egen uppgift

### Samverkan med resten

- **Glömd uppgift** följer med till nästa dag, och det som redan är avbockat förblir avbockat
- **Återkommande uppgift:** delmomenten nollställs vid varje nytt tillfälle
- **Delad uppgift:** delmomenten delas, och båda kan bocka av

### Mallar

- Man kan spara en checklista som mall, t.ex. "Träningsväska" eller "Packa till BVC", och välja den när man skapar en uppgift
- Mallar är **avstängda och dolda som standard**. De slås på i **Inställningar**, och först då syns de i appen
- När mallar är påslagna kan en mall kopplas till en **aktivitetstyp** från en kalenderprenumeration, t.ex. Träning → Träningsväska (se Barnens aktiviteter)

### Inställningar

- Delmoment går att **stänga av i Inställningar**, enligt grundregeln

Delmoment och mallar byggs i **byggsteg 4**, tillsammans med snabbinmatningen. Kopplingen till aktivitetstyper kommer i byggsteg 9.

## Lägg till

- **Bara titeln krävs.** Allt annat är frivilligt, så en enkel uppgift läggs in med titel och ett tryck på Spara
- De vanligaste valen syns direkt: kategori, prio, datum och tid
- Resten ligger under **Fler val**: upprepning, typ av påminnelse, plats, delmoment, Google Kalender och delning

## Snabbinmatning

Man skriver uppgiften som en vanlig mening i ett enda fält, och appen fyller själv i datum, tid och annat. "handla mjölk imorgon 17" blir uppgiften "Handla mjölk", imorgon kl. 17.00.

### Vad den förstår

- **Dagar:** "idag", "imorgon", "på fredag", "nästa vecka", "14 nov"
- **Tid:** "17", "kl 9", "halv 8", "på kvällen"
- **Upprepning:** "varje söndag", "varannan vecka"
- **Prio:** "!" för Prio och "!!" för Måste, eller orden "viktigt" och "måste"
- **Kategori:** "#jobb", "#barnen". Utan kategori hamnar uppgiften i Övrigt
- **Plats:** "vid affären", "efter jobbet" (se Platspåminnelser)

### Så fungerar det

- Medan man skriver visar appen vad den har förstått som små etiketter under fältet, t.ex. "Imorgon 17.00 · Vanlig"
- Har den tolkat fel trycker man bort etiketten, och ordet blir kvar i titeln i stället
- Allt görs med enkla regler och ordlistor i appen. Ingen AI, gratis och fungerar utan nät
- **Kan stängas av i Inställningar.** Avstängd tolkas inget, och det man skriver blir bara titeln
- Röstinmatning tolkas på samma sätt (se Röstinmatning)

Snabbinmatning byggs i **byggsteg 4**.

## Röstinmatning

Man lägger till uppgifter med rösten. Det man säger tolkas på samma sätt som snabbinmatning: datum, tid, prio, kategori och plats.

### Var mikrofonen finns

- I fältet i **Lägg till**
- Direkt från **widgeten** och **snabbinställningsrutan**, utan att öppna appen
- Via **långt tryck på appikonen**: genvägen "Ny uppgift med röst"

### Så fungerar det

- **Granska först:** texten och etiketterna från tolkningen visas, och man trycker Spara. Man kan rätta innan
- **Spara direkt:** ett val i Inställningar för den som vill hoppa över granskningen. Avslaget som standard. Ångra-raden visas efter att uppgiften sparats
- **En uppgift i taget.** Ingen uppdelning i flera uppgifter
- **Undantag: inköpslistan.** "Lägg till gurka, mjölk och blöjor på inköpslistan" blir tre varor, var och en med föreslagen platstagg. Appen känner igen det på orden "inköpslistan" eller "handlalistan". Annars blir det en vanlig uppgift, så att t.ex. "köp blöjor vid affären" fortfarande blir en platsuppgift
- **Kan stängas av i Inställningar**, enligt grundregeln

### Teknik och kostnad

- **Android:** inbyggd tal-till-text på svenska. Gratis, och fungerar utan nät om det svenska språkpaketet är nedladdat
- **iPhone (webbapp):** tangentbordets inbyggda diktering fungerar redan i textfältet. Ingen extra utveckling behövs

Mikrofonen i Lägg till byggs i **byggsteg 4** med snabbinmatningen. Mikrofonen i widgeten, snabbinställningsrutan och genvägen på appikonen byggs i **byggsteg 5** med Synlighet. Delningen till inköpslistan kommer i **byggsteg 7**.

## Swipe och redigering

| Gest | Öppen uppgift | Klar uppgift |
| --- | --- | --- |
| Swipe vänster | Klar (överstruken) | – |
| Swipe höger | Skjut upp till imorgon | Öppen igen |
| Tryck | Ändra, t.ex. välja valfritt datum | Ändra |

- **Ta bort:** man trycker på uppgiften och går in på Redigera. Där kan man också ändra allt annat
- **Ångra:** efter varje swipe och borttagning visas en rad längst ner i ca 5 sekunder, t.ex. "Klar · Ångra". Ett tryck tar tillbaka det. Ingen "Är du säker?"-fråga behövs
- **Ångra i efterhand:** en klar uppgift blir öppen igen med swipe höger. En uppskjuten uppgift flyttas tillbaka från flerdagsvyn eller kalendern

## Påminnelser

- I Inställningar kan man slå på och av och välja tid för påminnelsen om att **titta på listan**
- Enskilda uppgifter kan få egen tid med **tyst notis, notis med ljud eller alarm**

## Synlighet

Man glömmer lätt att titta på listan, så appen ska synas när man använder eller ser telefonen. Alla sätt bygger på dagens lista och slås på och av var för sig under **Inställningar → Synlighet**:

- **Fast notis i notisfältet:** på/av. Visar antingen bara antal ("Idag: 4 kvar · 1 Måste") eller de tre viktigaste uppgifterna med knappen Klar. Syns också på låsskärmen. Sveps den bort läggs den tillbaka vid nästa upplåsning
- **Ikon i statusfältet:** följer med den fasta notisen och syns uppe till vänster bredvid klockan, även inne i andra appar. Ikonen ritas om när listan ändras och visar antal kvar idag, med ett "!" bredvid när det finns en Måste-uppgift. Den är vit och enfärgad (Android tillåter inga färger där) och kan ersättas av en prick om många notiser ligger samtidigt
- **Siffra på appikonen:** på/av. Räknar antingen alla kvar idag eller bara Måste och glömda
- **Påminnelse vid upplåsning:** av, första upplåsningen på morgonen ("God morgon, 5 saker idag, 1 måste") eller efter en längre paus, med ett max antal per dag
- **Lista som låsskärmsbild:** på/av. Appen ritar dagens lista som en bild och sätter den som låsskärmsbakgrund, ovanpå den vanliga bakgrundsbilden om man vill. Uppdateras när listan ändras
- **Upptrappning:** på/av. Appen blir mer synlig när det finns glömda uppgifter eller Måste, och mer diskret när allt är lugnt

Utan inställning i appen, läggs till från telefonen som för andra appar:

- **Widget på hemskärmen:** liten (bara antal, med prick i prioritetsfärg) och stor (listan, bocka av direkt). Storlek och hur många dagar den visar väljs när widgeten placeras
- **Snabbinställningsruta** i notisfältet som öppnar Lägg till direkt

**Påslaget från början:** fast notis, siffra på ikonen och påminnelse vid första upplåsningen på morgonen. Övriga är avslagna.

**iPhone (webbapp):** bara notiser och siffra på ikonen. Inga widgets, fast notis eller låsskärmsbild.

**Förhållande till andra påminnelser:**

- Den inställbara tiden för att **titta på listan** (Påminnelser) finns kvar som en vanlig notis vid en fast tid. Synlighet kompletterar den
- **Måste-notisen vid upplåsning** (Måste) gäller bara Måste-uppgifter och har egna inställningar. Skulle den och påminnelsen vid upplåsning komma samtidigt slås de ihop till en notis

Synlighet byggs i **byggsteg 5**.

## Veckogenomgång

En kort stund en gång i veckan där man går igenom det som har samlats i Idag och tittar på veckan som kommer. Tar några minuter.

### När

- **Söndag kl. 19 som förval.** Dag och tid väljs i Inställningar
- En notis: "Veckogenomgång – 3 minuter?" med valen **Senare** och **Hoppa över veckan**
- Genomgången är **ingen uppgift**: hoppar man över den blir den inte glömd och stiger inte i prio

### Stegen

1. **Förra veckan:** antal klara uppgifter, t.ex. "14 klara", så att det börjar positivt
2. **Glömda i Idag:** uppgifter som har legat kvar och stigit i prio. En i taget med valen **Gör idag**, **Välj dag**, **Sänk prio** och **Ta bort**
3. **Uppskjutna gång på gång:** uppgifter som har skjutits upp **3 gånger eller fler** (swipe höger eller nytt datum), t.ex. "Uppskjuten 6 gånger – fortfarande aktuell?". Samma val som i steg 2. De blir aldrig glömda eftersom de behåller sin prio, så annars kan de skjutas upp i veckor utan att någon märker det
4. **Veckan som kommer:** en rad per dag med Måste, tider och barnens aktiviteter. Tunga dagar markeras, så man ser om något borde flyttas
5. **Lägg till:** ett fält med snabbinmatning för det man kommer på
6. **Hjärta:** ett förslag att planera något för veckan, för sig själv (blått) eller relationen (rött)

Steg som är tomma hoppas över, så genomgången blir kort när allt är under kontroll.

### Delning och inställningar

- **Ingen gemensam genomgång** med sambon. Var och en gör sin egen
- **Delade uppgifter** finns med i den egna genomgången, som vilka uppgifter som helst
- Hjärta är privat och syns bara i den egna genomgången
- Appen **räknar hur många gånger en uppgift har skjutits upp**. Räknaren nollställs när uppgiften görs
- Veckogenomgången går att **stänga av i Inställningar**, enligt grundregeln

Veckogenomgången byggs i **byggsteg 6**, tillsammans med Hjärta. Barnens aktiviteter kommer med i byggsteg 9.

## Platspåminnelser

Plats är alltid ett **frivilligt** val, precis som tid. Uppgifter och inköp utan plats fungerar som vanligt.

### Platser

- Man sparar egna platser i **Inställningar**, t.ex. Hem, Jobb, Skola, Förskola och Stan. En plats kan också läggas till direkt via "+ Ny plats" när man skapar en uppgift
- En plats väljs på en karta eller med "Spara platsen där jag står"
- **Radie per plats:** större för områden som Stan och köpcentrum (t.ex. 500 m), mindre för en enskild butik (minst ca 150 m)
- **En plats kan vara en grupp**, t.ex. Mataffär för alla matbutiker man brukar handla i
- **Sätt att känna av platsen**, valbart per plats:
  - GPS (standard)
  - Wifi, t.ex. Hem när telefonen kopplar upp mot hemmanätet. Träffsäkert och drar nästan inget batteri
  - Bilens Bluetooth, t.ex. Efter jobbet när telefonen kopplar ihop sig med bilen

### I uppgiften

- Man väljer plats med platsknappar i Lägg till. Formuleringen blir naturlig: **"Vid Stan"**, **"Efter Jobbet"** (när man lämnar) och **"Hemma"** (när man kommer hem)
- Snabbinmatning kan tolka t.ex. "köp blöjor vid affären"
- **Datum, tid och plats tillsammans:**
  - Datum = när uppgiften börjar gälla och syns i Idag
  - Tid = vanlig påminnelse
  - Plats = extra påminnelse när man är där, från datumet och framåt
  - När uppgiften görs stängs alla påminnelser av, oavsett vilken som kom först
- **Platsuppgifter i Idag:** de ligger i Idag med en platssymbol, bland uppgifterna utan tid. Saknas datum gäller de från idag
- **Ingen priohöjning:** en platsuppgift blir inte glömd och stiger inte i prio, eftersom den väntar på att man kommer till platsen. Har den både plats och tid gäller tiden som vanligt

### Begränsningar

- **Bara Android.** Webbappen på iPhone kan inte känna av platser i bakgrunden
- Kräver platsbehörighet "hela tiden". Notisen kan komma några minuter sent
- Gratis: Androids platstjänst och en gratiskarta som OpenStreetMap

Platspåminnelser byggs i **byggsteg 8**.

## Google Kalender

Synken går bara **från appen till Google Kalender**. Google Kalenders API är gratis.

- En uppgift kan ha rutan **"Lägg i Google Kalender"**. Man loggar in med sitt Google-konto en gång
- **Hämta från kalendern:** en knapp visar kommande händelser. Man bockar i det man vill ha som uppgifter och väljer kategori och prio
- Hämtade händelser blir vanliga uppgifter, en kopia och ingen synk. Ändringar i kalendern efteråt påverkar inte appen
- Appen kommer ihåg vad den redan har hämtat och visar inte sina egna händelser, så det blir inga dubbletter
- **Glömda eller flyttade uppgifter** som är synkade flyttas med i kalendern, så att kalendern alltid visar samma datum som appen
- **Uppgifter utan tid** blir heldagshändelser i kalendern
- **Klar uppgift** ligger kvar i kalendern med en ✓ i namnet
- **Hjärta-uppgifter** kan också synkas om man bockar i rutan. Eftersom våra kalendrar är synkade kan sambon då se dem
- Synkade Hjärta-uppgifter får en **neutral titel** i kalendern, t.ex. "Planerat". Hela texten syns bara i appen
- **Delade uppgifter** synkas bara till kalendern hos den som bockade i rutan, så att de inte syns dubbelt
- **Inget synkas som förinställt.** Man bockar i rutan på varje uppgift man vill ha i kalendern, eller slår på kalender för en hel lista (se Listor)
- **Sambon** kan koppla sin egen Google-kalender från webbappen. Våra kalendrar är redan synkade med varandra

## Barnens aktiviteter (kalenderprenumeration)

Sonens träningar, matcher och andra aktiviteter finns i SportAdmin. Appen hämtar dem automatiskt via SportAdmins kalenderlänk (iCal) och visar dem i en **egen lista**, t.ex. "Barnens träningar".

### Så fungerar det

- Man klistrar in kalenderlänken under **Inställningar → Kalenderprenumerationer** och väljer namn och färg för listan. Länken finns i SportAdmin-appen under Aktiviteter → Prenumerera, eller på föreningens hemsida (Prenumerera >> → länken under "Google & Android")
- Appen hämtar länken några gånger om dagen. Gratis, utan API eller konto hos SportAdmin
- Det går att lägga till **flera prenumerationer**, t.ex. ett lag per barn eller skolans och förskolans kalender om de har en
- **Android-appen hämtar** länken och synkar via Firebase. Webbappen på iPhone kan troligen inte hämta länken själv, men ser listan via Firebase om den delas
- **Länken är privat:** den sparas under det egna kontot och visas inte för andra
- **Ändringar följer med:** flyttas en aktivitet flyttas den i appen. Varje aktivitet har ett fast id, så det blir aldrig dubbletter

### Aktiviteter och föräldrauppgifter

- **Aktiviteter** (träning, match) **behöver inte bockas av**. De följer inte med till nästa dag, blir aldrig glömda och stiger inte i prio. När de har passerat hamnar de i historiken
- **Föräldrauppgifter** (t.ex. Kioskjobb, sådant man själv ska göra) blir **vanliga uppgifter**: de bockas av, följer med till nästa dag om de glöms och stiger i prio
- **Så känns typen igen:** typen står först i titeln ("Träning – …", "Match: …", "Kioskjobb – …"). Kända ord som Kioskjobb blir föräldrauppgifter direkt. Gör appen fel kan man ändra typen en gång, så kommer appen ihåg det för den titeln
- **I listorna:** aktiviteterna visas i listans egen färg och bokstav, som andra listor, och filtreras med sin kategoriknapp. Aktiviteter har ingen ring att bocka av utan en liten kalendersymbol. I Månad och Vecka syns de som prickar i listans färg

### Inställningar för listan

- **Visa i flödet:** som för andra listor kan man välja att inte visa listan i flödet (Idag, 3 dagar, Vecka). Här finns också valet att **bara visa föräldrauppgifter** i flödet, medan träningar och matcher bara syns i listan
- **Delning med sambon:** ett val för listan, **avslaget som standard**
- **Google Kalender:** listan synkas **inte** dit som standard, men kan slås på som för andra listor (se Listor). Prenumererar man redan på samma kalender i Google Kalender **varnar appen** för att det blir dubbelt

### Vad länken innehåller (testat 7 nov 2026)

- Ca 105 aktiviteter med tid, plats, beskrivning, fast id och datum för senaste ändring
- **Samlingstiden står i beskrivningen**, t.ex. "Samling: 12:00" för en match som börjar 12.30
- **Inga svar på kallelser** finns med, alltså inte vad man har svarat Ja eller Nej
- **Inställda aktiviteter markeras inte.** De försvinner troligen bara ur flödet

### Möjliga tillägg (inte bestämda)

- **Inställd?:** försvinner en kommande aktivitet ur flödet markeras den "Inställd?" i stället för att tas bort i tysthet
- **Olika inställningar per typ** (Träning, Match, föräldrauppgift): visa/dölj och vilken påminnelse den får
- **Påminnelse utifrån samlingstiden**, inte starttiden, t.ex. "Packa träningsväskan" en stund innan och "Åk nu"
- **Svar på kallelser i appen:** knapparna Ja och Nej på varje aktivitet. Nej blir nedtonad eller döljs, obesvarad får en markering. En knapp kan öppna SportAdmin-appen så man svarar där. Svaret kan inte skickas till SportAdmin, som saknar öppet gränssnitt
- **Skjuts:** om listan delas kan en aktivitet tilldelas mig eller sambon ("Vem kör?")
- **Packlista** med fasta delmoment per typ, t.ex. vattenflaska och benskydd. Görs med en mall kopplad till typen (se Delmoment)

Kalenderprenumerationer byggs i **byggsteg 9**, tillsammans med Google Kalender.

## Delning med sambo

- Man väljer själv vilka **listor eller enskilda uppgifter** som delas. Delas en hel lista delas allt nytt i den automatiskt (se Listor). Resten är privat
- Det som är delat syns för båda och synkas mellan telefonerna
- En delad uppgift är **klar för båda** när en av oss har gjort den
- En delad uppgift kan **tilldelas** en av oss
- Den andra får en **notis när uppgiften är gjord**. Det kräver troligen Firebase Blaze, precis som Måste-påminnelsen till sambon. Beslut tas vid byggsteg 7. Utan Blaze syns det i stället när man öppnar appen

## Delad inköpslista

- **En lista** med allt som ska handlas: mat, apotek, stan, köpcentrum osv.
- **Delad med sambon** och synkad direkt via Firebase, inom gratisnivån. Sambon kan fylla på från iPhone
- Varje vara kan **taggas med en eller flera platser**. Taggarna är samma platser som i Inställningar
- **Förslag på tagg:** "gurka" ger Mataffär, "Alvedon" ger Apotek, "skruv" ger Byggvaruhus. Ordlistan byggs in i appen och fylls på via chatten med Claude, som idébanken. Ingen AI i appen
- **Appen lär sig:** ändrar man taggen på en vara kommer den ihåg valet för det ordet
- Förslagen är bara förslag och kan stängas av i Inställningar
- **Varor utan tagg** hamnar under **"Var som helst"**. De ger ingen platsnotis men syns i listan
- **En notis per plats, inte per vara:** "Du är på stan – 3 saker att handla". Ett tryck öppnar listan filtrerad på platsen. Platsnotiser finns bara på Android
- Man bockar av medan man handlar. Avbockat sjunker till botten och rensas när man är klar, men sparas i historiken
- **Ofta köpta varor** föreslås när man lägger till
- **Från Lägg till:** man kan välja att lägga något som en vara i inköpslistan i stället för som en uppgift. Inköpslistan är skild från Idag-listan, så varor stiger inte i prio
- Möjligt tillägg senare: gruppering efter avdelning (frukt, mejeri, frys)

Den delade inköpslistan byggs i **byggsteg 7** (delning). Platsnotiserna för inköpslistan kommer i byggsteg 8.

## Lagring och inloggning

- **Allt sparas i molnet** i Firebase (Firestore): uppgifter, historik, kategorier, Hjärta och inställningar. Gratisnivån räcker för två personer
- **Inloggning med Google-kontot**, samma konto som för Google Kalender. Byter man telefon installerar man appen, loggar in och allt är tillbaka
- **Alla inställningar följer med** till en ny telefon
- **Fungerar utan nät:** appen sparar även lokalt och synkar när den är uppkopplad igen
- **Hjärta är privat även i molnet:** datan ligger under det egna kontot, och databasens regler gör att bara man själv kan läsa den

## Plattform och teknik

- **Fokus:** i huvudsak görs en Android-version av appen. Därefter görs en version för iPhone med de funktioner som fungerar där
- **Krav:** alla funktioner ska fungera på Android. Det ska inte kosta något. Undantag: appen får kosta lite om en funktion är värd det, men Claude frågar alltid först
- **Android (jag):** riktig app med alla funktioner inklusive alarm. Installeras själv, utan Play Butik
- **iPhone (sambo):** samma app som webbapp på hemskärmen. Listor, delning och notiser fungerar, men inte alarm (behövs inte). Om Hjärta ska finnas i iPhone-versionen bestäms senare
- **Ramverk:** Flutter (beslutat), så att Android-appen och webbversionen byggs från samma kod
- **Synk:** Firebase (beslutat), inom gratisnivån

## Utseende

Designen bygger på förslag 1, en lista, i färgskalorna Fjord (ljus) och Kväll (mörk). Skisserna finns på [designytan](https://claude.ai/artifact/Xzqk3ZiNDbtk1oPoh4FaLT).

- **Idag-skärmen:** kategoriknappar i kategorins färg till vänster för att filtrera, hjärtat längst ner med en knapp till inköpslistan (med antal varor) direkt ovanför, inställningar uppe till höger och val av period överst: Idag, 3 dagar och Vecka som listor, samt Vecka och Månad som översikt (markerade med en översiktssymbol). Månad finns bara som översikt. Alla fem ryms på en rad som lika breda knappar
- **Lägg till-knappen** sitter nere i högra hörnet, där tummen når
- **Måste överst:** ett val i Inställningar som lägger Måste-uppgifter först i Idag, 3 dagar och Vecka. Det är **avstängt som standard**
- **Datumraden:** under rubriken står hela veckodagen, datum och antal kvar, t.ex. "Torsdag 5 nov · 9 kvar". Blir det trångt döljs månaden först
- **Sorteringsknappen** sitter direkt efter datumraden och visar vald sortering (Tid, Kategori eller Prio). Den bryts aldrig till en ny rad. Ett tryck öppnar ett blad med Tid och datum (standard), Kategori och Prio. Valet sparas och gäller i Idag, 3 dagar och Vecka
- **Alla-knappen** överst bland kategoriknapparna visar alla kategorier igen
- **Uppgiftsraden:** ringen har prioritetens färg och är tunnare ju lägre prio och tjockare ju högre. Rutan tonar subtilt mot kategorifärgen längst till höger
- **Månadsvyn:** kalender med veckonummer, och man sveper för att byta månad
- **Kategorifilter:** ett tryck på en kategoriknapp visar bara den kategorin. Knappen ser intryckt ut och överst står "Visar bara" med kategorin och ett kryss för att ta bort filtret. Man kan välja **flera kategorier** samtidigt, ett **nytt tryck** på en vald kategori tar bort den, och filtret **följer med** till 3 dagar, Vecka och Månad
- **Veckoöversikten:** en rad per dag med upp till tre uppgifter (tid, titel och kategori) och "+2 till" om det finns fler. Man sveper vecka för vecka. Samma markeringar som i månadsvyn: tonad bakgrund för Prio och Måste, orange ring för glömd, ljusblå ring för delad
- **Förklaring:** både vecko- och månadsöversikten har längst ner en förklaring av markeringarna: Prio (tonad bakgrund), Måste, Glömd och Delad

| Prio | Färg | Hex |
| --- | --- | --- |
| Kan vänta | Grå | #7D8594 |
| Vanlig (standard) | Guld | #E3B341 |
| Prio | Orange | #F08A3E |
| Måste | Röd | #F2555A |

Prioritetsfärgerna är desamma i Fjord och Kväll. Färgskalan Sand används inte, åtminstone inte till en början (beslutat 8 nov).

### Färger och typsnitt

- **Typsnitt:** Inter i hela appen. Baloo 2 används bara i ordmärket justja

| Färg | Fjord | Kväll |
| --- | --- | --- |
| Bakgrund | #F4F6F9 | #111318 |
| Yta (kort, rader) | #FFFFFF | #1C1F27 |
| Yta 2 (knappar, val) | #E8ECF2 | #272B35 |
| Linje | #E3E7EE | #2C313C |
| Text | #1A1F29 | #ECEEF2 |
| Dämpad text | #5B6372 | #A0A7B4 |
| Rött hjärta | #D0435A | #F06C7D |
| Blått hjärta | #3A76C6 | #72A6EE |
| Glömd-märke (text / bakgrund) | #B0401C / #FBE8E0 | #F4A27E / #3B2620 |
| Delad (ljusblå ring) | #2F96D6 | #7CC4F5 |
| Swipe Klar (grön) | #2E8B57 | #6FCF97 |
| Swipe Imorgon (blå) | #2F7FC1 | #7CC4F5 |

| Kategori (förval) | Bokstav | Färg Fjord | Färg Kväll | Prick (båda) |
| --- | --- | --- | --- | --- |
| Sysslor | S | #2A8C7B | #5CC3AE | #23786A |
| Jobb | J | #4C5B78 | #A3AEC8 | #4C5B78 |
| Barnen | B | #C47A1F | #E8A85A | #9C5E17 |
| Sambo | Sa | #8A4FA8 | #BC93E6 | #8A4FA8 |
| Jag | Ja | #5E8F3A | #97C66E | #507A31 |
| Övrigt | Ö | #6B7280 | #6B7280 | #6B7280 |
| Hjärta | H | #D0435A | #F06C7D | #C23B52 |

- **De 12 färgerna** att välja bland för en kategori (pricken): #23786A, #4C5B78, #9C5E17, #8A4FA8, #507A31, #B83A3A, #2F7FC1, #C2558C, #0F7C8C, #7A6A2E, #5B4BB7, #6B7280
- **Radens toning** mot kategorifärgen längst till höger har 18 % täckning i Fjord och 24 % i Kväll
- **Idag och vald dag i kalendern:** idag har datumet i en fylld cirkel i textfärgen. En vald dag får en smal ram i textfärgen och bakgrunden Yta 2. Inga understrykningar

### Skärmar för byggsteg 1 (godkända 8 nov)

- **Första start:** en skärm med "Fortsätt med Google". Därefter föreslagna kategorier, förbockade (Sysslor, Jobb, Barnen, Sambo, Jag), som man kan bocka ur eller komplettera med en egen. Man börjar alltså inte helt tomt. Övrigt och Hjärta finns alltid
- **Kategorier i Inställningar:** en lista där man drar för att ändra ordningen i menyn till vänster. Ett tryck öppnar ett blad med namn, bokstav (ett eller två tecken), 12 färger, Visa i flödet och Dela med sambo. För Hjärta visas inte Dela med sambo, eftersom Hjärta aldrig delas
- **Ta bort kategori:** en dialog med Flytta till Övrigt, Ta bort uppgifterna också och Avbryt
- **Redigera uppgift:** samma fält som Lägg till, plus när uppgiften skapades och hur många gånger den skjutits upp. Ta bort uppgiften ligger längst ner
- **Swipe:** under fingret syns grönt med bock och Klar vid swipe vänster, och blått med Imorgon vid swipe höger. Ångra-raden är mörk och ligger längst ner med knappen Ångra, och Lägg till-knappen flyttar upp så länge den syns
- **Tom lista:** "Allt klart för idag" med antal avbockade, en knapp till imorgon och de klara uppgifterna under. Första gången visas i stället ett tips om att skriva som man pratar, t.ex. "handla mjölk imorgon 17"
- **Inställningar i steg 1:** konto, Färgskala (Följ telefonen som standard, där Kväll används när telefonen är i mörkt läge, eller fast Fjord eller Kväll), Kategorier, Listor i flödet, Måste överst och Logga ut. Inställningar för senare byggsteg syns gråade med märket "Senare steg" tills de byggs

## Garmin-urtavla

En egen urtavla till min Forerunner 935 som visar dagens läge från appen. Den byggs **separat**, som ett eget litet projekt i Garmins Connect IQ, efter byggsteg 7. Skisserna finns på [designytan för urtavlan](https://claude.ai/artifact/9Y8BNWNMYf3pcK1AN2iG2o).

- **Från klockan:** tid, dag, veckonummer, batteri %, puls, antal notiser och steg om det ryms
- **Bluetooth överst:** blå = kopplad till mobilen, grå med streck = inte kopplad
- **Raden från appen:** antal kvar och Måste eller glömda, med en prick i prioritetsfärgen, t.ex. "4 kvar · 1 Måste". Under den visas den viktigaste uppgiften
- **Påminnelsebricka** framför uppgiften: vit ram med tiden = påminnelse kommer, röd "NU" = påminnelse nu, orange med tiden = påminnelsen har gått men uppgiften är inte avbockad
- **Missad påminnelse först:** en missad påminnelse som inte är avbockad går före allt annat på raden
- **Inte kopplad:** raden från appen blir grå och visar när den senast hämtades, tills mobilen är kopplad igen
- **Hjärta visas aldrig** på urtavlan
- **Uppdatering:** Android-appen skickar listan till klockan när den ändras, och urtavlan hämtar i bakgrunden ungefär var 5:e minut. Bara det viktigaste skickas, eftersom klockan har lite minne
- **Notiser:** appens vanliga notiser speglas redan till klockan via Garmin Connect från byggsteg 3. Klockan vibrerar men kan inte ringa som ett alarm. Knappar som Klar i notisen stöds troligen inte på 935:an, så det testas i byggsteg 3. Hjärta-notiser visas med sin vanliga text på klockan
- **Logga:** den orange ringen från Justjas logga sitter som en liten symbol längst ner på urtavlan, under stegen. Den testas så. Blandas den ihop med orange för missad påminnelse görs den grå eller vit

## Idéer för senare

- **Träning:** påminnelser, träningsschema, mål och tips på schema för att nå målet. **Parkerad till efter byggsteg 9**, eftersom den är stor nog att nästan vara en egen app

## Projektplan

Appen byggs i fyra faser. Den här texten är projektets underlag, och allt som bestäms förs in här.

1. **Idé och anteckningar:** ett eget chattflöde. Detta dokument hålls uppdaterat
2. **Design:** ett eget chattflöde där skärmarna skissas (Idag, uppgift, kategorier, Hjärta, inställningar). Klar för byggsteg 1 den 8 nov, och uppdateras när det behövs
3. **Bygg:** i Claude Code, kopplat till ett GitHub-repo, i den här ordningen:
   1. Grund: inloggning med Google och molnlagring i Firebase (med en datamodell som klarar delning och privat Hjärta från start), appikonen, Idag-listan, Lägg till och Redigera, kategorier med Övrigt, prio och Måste, swipe och ångra samt Inställningar för steg 1. Webbversionen ska gå att bygga redan här, även om den inte används än
   2. Flöde och vyer: glömda uppgifter som stiger i prio, räknare för uppskjutningar, återkommande uppgifter, historik, sortering, 3 dagar, Vecka och Månad med veckonummer samt kategorifilter
   3. Påminnelser: notiser, alarm, Måste-påminnelser och påminnelsen om att titta på listan
   4. Snabbare inmatning: snabbinmatning, mikrofon i Lägg till, delmoment och mallar
   5. Synlighet: fast notis, statusikon, siffra på appikonen, upplåsning, låsskärmsbild, widget, snabbinställningsruta och röstgenvägar
   6. Hjärta: idébanken, Må bra och veckogenomgången
   7. Delning: delning med sambon, den delade inköpslistan och webbappen för iPhone. Ta här upp om sambon ska få Måste-påminnelser kl. 18.30 och notis när en delad uppgift är gjord (kräver troligen Firebase Blaze)
   8. Platspåminnelser, inklusive platsnotiser för inköpslistan
   9. Google Kalender och kalenderprenumerationer, t.ex. barnens aktiviteter från SportAdmin
4. **Testning:** efter varje byggsteg. Appen används på riktigt några dagar innan nästa steg. Steg 7 testas tillsammans med sambon

- [x] Idé klar
- [x] Design klar
- [ ] Byggsteg 1
- [ ] Byggsteg 2
- [ ] Byggsteg 3
- [ ] Byggsteg 4
- [ ] Byggsteg 5
- [ ] Byggsteg 6
- [ ] Byggsteg 7
- [ ] Garmin-urtavla (separat, efter byggsteg 7)
- [ ] Byggsteg 8
- [ ] Byggsteg 9
