# Justja – instruktioner för Claude Code

Justja är en privat påminnelseapp för Hannes och hans sambo. Den byggs i Flutter med Firebase, i små steg som testas på riktigt mellan varje steg.

## Läs först

- `docs/spec.md` – hela specen. Den gäller. Är något oklart eller saknas: fråga, gissa inte.
- `docs/datamodell.md` – Firestore-strukturen och säkerhetsreglerna.
- `docs/steg-N.md` – briefen för byggsteget som pågår. Bygg bara det som står där.
- `docs/design/` – skärmbilder för byggsteg 1, i Fjord (`-fjord.png`) och Kväll (`-kvall.png`), t.ex. `04-idag-fjord.png`. `docs/design/LASMIG.md` listar vad varje bild visar.
  - Specen och steg-briefen gäller före bilderna. Bilderna visar ibland saker från senare steg, t.ex. Hjärta-förslag, "Dubbelt påmind" och upprepning. Bygg dem inte förrän briefen säger det (LASMIG.md pekar ut dem).
  - Ordmärket justja är ritat med ett reservtypsnitt i bilderna. I appen ska det vara Baloo 2, fetstil.

## Grundregler (från specen)

1. **Android först**, med alla funktioner inklusive alarm. iPhone och Windows får samma app som webbapp, utan alarm, widget och platspåminnelser.
2. **Gratis som utgångspunkt.** Lägg inte till betaltjänster, betal-API:er eller Firebase Blaze utan att fråga först och förklara kostnaden.
3. **Ingen AI-API i appen.** Snabbinmatning, förslag och taggar görs med regler och ordlistor i appen.
4. **Hjärta är privat och delas aldrig** med sambon, varken som lista eller uppgift. Det ska vara omöjligt även i databasens säkerhetsregler, inte bara i gränssnittet.
5. **Nya funktioner ska gå att stänga av i Inställningar.**
6. **Inget tas bort automatiskt.** Glömda uppgifter flyttas vidare till idag.

## Så jobbar vi

- **Hannes är inte programmerare.** Förklara kort och enkelt på svenska vad du gör och varför. Undvik jargong, eller förklara den.
- **Gör en plan innan du kodar** och visa den. Vänta på ett ok innan större ändringar.
- **Små delsteg.** Efter varje delsteg: kör appen, berätta exakt vad Hannes ska testa på telefonen, och committa när det fungerar.
- **Fråga hellre än att gissa** när specen inte räcker. Föreslå gärna ett standardval.
- **Nya beslut** som tas under bygget skrivs in i `docs/beslut.md` (datum + beslut), så att de kan föras in i specen efteråt.
- **Lägg inte till stora paket** utan att nämna dem först. Välj väl underhållna, vanliga paket.

## Språk

- Allt i appen (texter, knappar, notiser) är på **svenska**.
- Kod, variabelnamn och kodkommentarer på **engelska**.
- Commit-meddelanden och förklaringar till Hannes på **svenska**.

## Teknik

- Flutter, plattformar: `android` och `web`. App-id: `se.justja.justja`.
- Firebase: Auth (Google-inloggning), Cloud Firestore (databas-id `(default)`, plats Europa). Projektet ligger på gratisplanen Spark.
- Offline: Firestore ska fungera utan nät och synka när nätet kommer tillbaka (påslaget som standard på Android, slå på för webben).
- Typsnitt: Inter i appen, Baloo 2 bara i ordmärket justja. Bunta typsnittsfilerna i appen så att de fungerar offline.
- Logga: `assets/brand/justja-ikon.svg`. Appikonen tas fram med `flutter_launcher_icons`.
- Färgskalor: Fjord (ljus) och Kväll (mörk), se tabellerna i specen under Utseende.

## Vanliga kommandon

```
flutter pub get          # hämta paket
flutter run              # kör på inkopplad telefon
flutter run -d chrome    # kör webbversionen
flutter analyze          # hitta fel i koden
flutter test             # kör testerna
flutter build apk        # bygg en APK att installera
flutter build web        # bygg webbversionen
```

## Testning

- Skriv enhetstester för logik som är lätt att få fel: datum, sortering, prio som stiger, Övrigt när kategori saknas.
- `flutter analyze` ska vara utan fel innan commit.
- Varje byggsteg avslutas med att Hannes använder appen på riktigt några dagar.
