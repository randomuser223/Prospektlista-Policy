# Intresseavvägning – berättigat intresse (GDPR art. 6.1 f) – Prospektlista

Senast uppdaterad: 2026-07-25.

## Syfte med behandlingen

Prospektlista sammanställer och levererar en månatlig lista över nyregistrerade aktiebolag inom en avgränsad stad/zon till betalande redovisningsbyråer, i syfte att hjälpa dem hitta nya potentiella kunder i ett tidigt skede.

## Vilka personuppgifter behandlas

Vi behandlar namn på styrelseledamot/verkställande direktör för nyregistrerade aktiebolag – en fysisk person i en offentlig, lagstadgad roll. Uppgifterna hämtas ursprungligen från Bolagsverkets och SCB:s offentliga register (se `src/bolagsverket_kalla.py` för teknisk källa, inklusive en dokumenterad osäkerhet kring om det fältet faktiskt finns i den avgiftsfria datan i dagsläget). Ingen kontaktinformation (telefon/e-post) samlas in i det här steget – kontaktberikning är explicit pausad tills den validerats separat (se `src/contact_enrichment.py`, som just nu bara är en stub).

## Rättslig grund

Behandlingen stödjer sig på berättigat intresse (artikel 6.1 f). Nedan görs balanseringen enligt trestegstestet.

### 1. Legitimt intresse

Prospektlista och dess kunder (redovisningsbyråer) har ett legitimt affärsintresse av att identifiera nystartade aktiebolag i sitt geografiska verksamhetsområde. Det är etablerad B2B-marknadsföringspraxis, och uppgifterna är redan offentliga.

### 2. Nödvändighet

Det finns ingen mindre integritetskänslig metod att uppnå samma resultat. Registreringsdatum och bolagsform måste hämtas löpande från de officiella registren, och styrelseledamot/VD är den kontaktpunkt lagstiftaren redan kräver ska vara offentlig – bland annat för att bolaget ska gå att nå.

### 3. Balansering mot den registrerades intressen

Uppgifterna är redan offentliga och lagstadgat publicerade av Bolagsverket i just det syftet: transparens kring vem som företräder ett bolag. Ingen känslig data enligt artikel 9 behandlas, och ingen automatiserad profilering eller automatiserat beslutsfattande sker. Den registrerade kan rimligen förvänta sig att uppgifter om ett styrelseuppdrag används i näringslivssammanhang. Rätt att invända hanteras aktivt genom två nivåer av "Spärrlista"-flikar: en per kund-Sheet (exkluderar bara från den kundens leveranser) och en global, i ett separat dedikerat Sheet (exkluderar från samtliga kunders/städers leveranser) – en riktig art. 21-invändning ska föras in i den globala listan, inte bara den lokala, så att den registrerade slipper invända hos varje enskild kund för sig (se `pipeline.py` och `sheets_delivery.get_sparrlista`). Dataminimering sker genom att rader äldre än 13 månader raderas automatiskt (se `src/retention.py`). Retentionstiden är fast och gäller lika för alla kunder - kunden kan inte förlänga den och därigenom behålla uppgifterna längre än vad som bedömts nödvändigt.

### Slutsats

Sammantaget bedöms det legitima intresset väga tyngre än den registrerades intresse av att uppgifterna inte behandlas, givet att uppgifterna redan är offentliga, begränsade till namn och uppdrag, och att en enkel invändningsmekanism finns.

## Ansvarig och uppdatering

Prospektlista drivs för närvarande av en privatperson, inte ett aktiebolag - personuppgiftsansvarig är alltså den fysiska personen bakom Prospektlista, inte en juridisk person. Det här dokumentet ska uppdateras av den personen vid förändringar i behandlingen – till exempel om kontaktberikning (telefon/e-post) aktiveras. Den behandlingen kräver en egen, reviderad intresseavvägning eftersom den utökar vilka uppgifter som samlas in och hur de kan användas.
