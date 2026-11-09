# Skisser för byggsteg 1

Skärmdumpar från designytan, tagna 9 nov 2026. Den här filen ersätter tidigare versioner av `docs/design/LASMIG.md`, och filnamnen nedan är de som gäller.

Varje skärm finns i två versioner: `-fjord.png` (ljus) och `-kvall.png` (mörk). Bilderna visar layouten. Exakta färger, mått och texter står i `docs/spec.md`, och vad som ingår i steg 1 står i `docs/steg-1.md`. Säger en bild något annat än de två filerna, så gäller filerna.

| Filnamn (utan -fjord/-kvall) | Skärm |
| --- | --- |
| 01-inloggning | Inloggning: ikon, ordmärke, undertext och "Fortsätt med Google" |
| 02-startbild | Startbild (splash): ikonen i mitten, litet ordmärke längst ner |
| 03-forsta-start-kategorier | Första start: föreslagna kategorier, Egen kategori, Övrigt och Hjärta |
| 04-idag | Idag-listan, scrollad |
| 05-tom-lista-allt-klart | Tom lista när allt är avbockat |
| 06-tom-lista-forsta-gangen | Tom lista första gången, med tipset |
| 07-lagg-till | Lägg till, bladet med ifyllt fält |
| 08-lagg-till-tomt-falt | Lägg till, bladet med tomt fält ("Justja! Vad kom du på?") |
| 09-lagg-till-alla-val | Lägg till med alla val, scrollad |
| 10-redigera-uppgift | Redigera uppgift, med Ta bort uppgiften längst ner |
| 11-swipe-och-angra | Swipe vänster (Klar), swipe höger (Imorgon) och ångra-raden |
| 12-kategorier | Kategorier i Inställningar |
| 13-redigera-kategori | Bladet Redigera kategori |
| 14-ta-bort-kategori | Dialogen Ta bort kategori |
| 15-installningar | Inställningar för steg 1, scrollad |

## Sådant i bilderna som INTE byggs i steg 1

Bilderna visar ibland mer än steg 1. Följ `docs/steg-1.md`:

- **04-idag:** Hjärta-förslaget, märkena "5 dagar" och "3 dagar" (prio som stiger, steg 2) och "Dubbelt påmind" (upprepning, steg 2) byggs inte än. Sorteringsknappen "Tid" och filtreringen med kategoriknapparna är steg 2. Periodknapparna syns, men bara Idag fungerar. Övriga, Hjärtat och inköpsknappen gråas med "Senare steg"
- **05-tom-lista-allt-klart:** knappen "Visa imorgon" kräver vyn 3 dagar (steg 2). Den kan utelämnas eller gråas
- **07-lagg-till:** raden "Appen förstod" med etiketterna (Imorgon, 17:00, Vid Mataffär) är snabbinmatning, steg 4. I steg 1 sparas texten som titel. "Fler val" gråas med "Senare steg"
- **09-lagg-till-alla-val:** i steg 1 används bara titel, kategori, prio, datum och tid. Upprepning, påminnelse, plats, delmoment, kalender och delning kommer senare
- **10-redigera-uppgift:** upprepning är steg 2. "Fler val" gråas
- **13-redigera-kategori:** "Dela med sambo" visas gråad till steg 7, och den visas aldrig för Hjärta
- **01, 02, 15:** ordmärket "justja" är ritat med ett reservtypsnitt i bilderna. I appen ska det vara Baloo 2, fetstil, enligt specen
- Bladen i 07, 08, 13 och 14 ligger över en förenklad bakgrund. I appen ligger de över den riktiga skärmen
