# Kassebog

En enkel kassebog til en dansk enkeltmandsvirksomhed, samlet i én HTML-fil. Den holder styr på indtægter, udgifter, kørsel, moms, løn til dig selv, årsresultat og frister, og den kender de danske satser og regler.

Alle data ligger som almindelige Markdown-filer i en mappe, du selv vælger. HTML-filen indeholder ingen data, og intet sendes til en server. Du kan åbne og rette filerne i Obsidian eller en anden teksteditor, og appen læser dem igen.

> **Bemærk:** Kassebog giver et overblik og et overslag. Den erstatter ikke en revisor, og den er ikke et godkendt digitalt bogføringssystem efter bogføringsloven.

---

## Indhold

- [Funktioner](#funktioner)
- [Kom i gang](#kom-i-gang)
- [Filerne i mappen](#filerne-i-mappen)
- [Ret direkte i filerne](#ret-direkte-i-filerne)
- [Satser og opdateringskilde](#satser-og-opdateringskilde)
- [Sådan regner appen](#sådan-regner-appen)
- [Begrænsninger](#begrænsninger)
- [Privatliv](#privatliv)

---

## Funktioner

| Fane              | Hvad den gør                                                                                                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Overblik**      | Omsætning, fradrag, overskud, anslået skat, løn til dig selv og moms for den aktuelle periode. Søjlediagram måned for måned og de næste fem frister. Advarsler om momsgrænse, digital bogføring, foreløbige satser og overskredne frister. |
| **Indtægter**     | Dansk salg med 25 % moms, ydelser til EU-firmaer (rubrik B) og momsfrit salg (rubrik C). Beløb kan indtastes inkl. eller ekskl. moms.                                                                                                      |
| **Udgifter**      | 14 kategorier med automatisk momsbehandling, erhvervsandel i procent, omvendt betalingspligt for køb i EU og uden for EU, og særregel for repræsentation. Markerer udstyr over småaktivgrænsen.                                            |
| **Kørsel**        | Kørselsbog med fra, til, formål og km. Regner fradrag med høj og lav sats ud fra de kørte km i året.                                                                                                                                       |
| **Løn til mig**   | Registrerer private hævninger, skat betalt fra virksomhedens konto og indskud. Viser hvor meget du stadig kan hæve, når skatten er sat til side.                                                                                           |
| **Moms**          | Momsangivelse pr. halvår eller kvartal med salgsmoms, købsmoms, momstilsvar og rubrik A, B og C. Tallene kan kopieres til TastSelv, perioden kan markeres som indberettet, og rapporten kan gemmes som Markdown.                           |
| **Årsresultat**   | Skattemæssigt resultat fordelt på kategorier, tal til oplysningsskemaet og et overslag over skatten af overskuddet. Kan gemmes som Markdown.                                                                                               |
| **Frister**       | Momsfrister, B-skatterater og fristen for oplysningsskemaet for det valgte år.                                                                                                                                                             |
| **Indstillinger** | Virksomhedens navn og CVR, momsregistrering og -periode, kommune- og kirkeskat, løn fra job ved siden af, satser og eksempeldata.                                                                                                          |

Desuden:

- Skift mellem regnskabsår i toppen.
- Lyst og mørkt tema efter systemets indstilling.
- Eksempeldata kan indlæses og fjernes igen med ét klik. De står med «Eksempel:» foran teksten.
- Rækker med en dato, et beløb eller km, appen ikke kan læse, markeres med «tjek».

---

## Kom i gang

1. Download `Kassebog.html`.
2. Åbn filen i **Chrome, Edge eller Brave** på en computer. Appen bruger [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_API), som Firefox og Safari ikke understøtter.
3. Tryk **Vælg mappe**, og vælg eller opret en mappe til dine regnskabsdata, fx i din Obsidian-vault eller en mappe, der synkroniseres til skyen.
4. Giv browseren lov til at læse og skrive i mappen.
5. Udfyld virksomhedsoplysninger og skatteprocenter under **Indstillinger**.

Appen husker mappen til næste gang. Browseren kan bede dig bekræfte adgangen igen, når du åbner filen.

Der er intet at installere og intet at bygge. Hele appen er én fil med HTML, CSS og JavaScript.

---

## Filerne i mappen

Første gang opretter appen indstillinger, satser og tomme filer for det aktuelle år:

```
Regnskab/
├── Kassebog indstillinger.md
├── Kassebog satser.md
├── 2026 Indtægter.md
├── 2026 Udgifter.md
├── 2026 Kørsel.md
├── 2026 Hævninger.md
├── 2026 Momsrapport.md      ← når du gemmer den
└── 2026 Årsresultat.md      ← når du gemmer den
```

Andre filer i mappen bliver ikke rørt. Rapporterne genereres ud fra kildefilerne, så ret i kildefilerne og ikke i rapporterne.

Hver datafil har frontmatter, en kort forklaring og en Markdown-tabel:

```markdown
---
kassebog: indtægter
aar: 2026
---
# Indtægter 2026

Kildedata til Kassebog. Beløb skrives som 1250,00. Moms er inkl. eller ekskl. Type er DK, EU eller Momsfri.

| Dato       | Bilag | Tekst               | Beløb    | Moms  | Type | ID       |
| ---------- | ----- | ------------------- | -------- | ----- | ---- | -------- |
| 2026-01-22 | 1     | Workshop, Firma A/S | 18750,00 | inkl. | DK   | mk2x9a1b |
```

Indstillingerne ligger i frontmatter i `Kassebog indstillinger.md`, herunder hvilke momsperioder der er markeret som indberettet (fx `2026-H1` eller `2026-Q3`).

---

## Ret direkte i filerne

Du kan tilføje, rette og slette rækker i Obsidian eller en anden editor:

- Behold kolonnenavnene i tabellens første linje. Rækkefølgen må gerne ændres, og ekstra kolonner bevares.
- Datoer skrives som `2026-03-15`. Beløb som `1250,00` eller `1250`.
- **Indtægter:** Moms er `inkl.` eller `ekskl.`. Type er `DK`, `EU` eller `Momsfri`.
- **Udgifter:** Beløb skrives inkl. moms, som på bilaget. Moms er `Auto`, `25 %`, `Ingen`, `Omvendt EU` eller `Omvendt udland`. Kategori skal være et af navnene fra appens liste.
- **Kørsel:** Km er én vej. Retur er `ja` eller `nej`.
- **Hævninger:** Type er `Løn til mig selv`, `Skat betalt` eller `Indskud`.
- ID-kolonnen må være tom i nye rækker. Appen udfylder den, næste gang den skriver filen.
- Tekst over og under tabellen bliver stående, når appen gemmer.
- Tryk **Genindlæs**, eller skift tilbage til browserfanen, efter du har rettet i en fil.

Appen læser altid filen frisk, før den skriver, så ændringer fra en editor bliver ikke overskrevet.

### Udgiftskategorier

| Kategori                      | Moms som standard                                |
| ----------------------------- | ------------------------------------------------ |
| Varekøb og materialer         | 25 %                                             |
| Kontorartikler og tryk        | 25 %                                             |
| Software og abonnementer      | 25 %                                             |
| Telefon og internet           | 25 %, erhvervsandel 50 % som standard            |
| Markedsføring og annoncer     | 25 %                                             |
| Kurser og faglitteratur       | 25 %                                             |
| Udstyr og småaktiver          | 25 %                                             |
| Lokaler og husleje            | 25 %                                             |
| Rejser og offentlig transport | Ingen                                            |
| Repræsentation og restaurant  | 25 %, men kun 25 % af moms og udgift trækkes fra |
| Forsikring                    | Ingen                                            |
| Bank og gebyrer               | Ingen                                            |
| Revisor og rådgivning         | 25 %                                             |
| Andet                         | 25 %                                             |

---

## Satser og opdateringskilde

Satserne står i `Kassebog satser.md` som en tabel med én kolonne pr. år:

```markdown
---
sidst_tjekket: 2026-11-20
opdateringskilde: ""
---
| Nøgle         | Sats                                |    2026 |      2027 | Kilde                 |
| ------------- | ----------------------------------- | ------: | --------: | --------------------- |
| status        | Status (endelig eller foreløbig)    | endelig | foreløbig | skat.dk/hjaelp/satser |
| kmHoj         | Kørsel op til 20.000 km, kr. pr. km |    3,94 |      4,13 | Skatterådet           |
| personfradrag | Personfradrag, kr.                  |   54100 |     55700 | skat.dk               |
| ...           |                                     |         |           |                       |
```

- Procenter skrives som `12,01`, beløb som `54100`.
- En tom celle betyder samme værdi som året før.
- Et nyt år tilføjes som en ny kolonne, fx `2028`.
- Mangler et år helt, regner appen med det seneste år og viser en advarsel.

Filen indeholder kørselssatser, personfradrag, AM-bidrag, bund-, mellem-, top- og toptopskat med grænser, skatteloft, beskæftigelses- og jobfradrag, småaktivgrænsen, grænsen for momsregistrering og grænsen for digital bogføring.

### Automatisk opdatering

Under **Indstillinger → Satser** kan du angive en opdateringskilde: en `https://`-adresse på en anden `satser.md` i samme format, fx en rå fil i et GitHub-repo:

```
https://raw.githubusercontent.com/<bruger>/<repo>/main/satser.md
```

Appen tjekker kilden, hver gang den åbnes. Finder den forskelle, viser den hver ændring, og du godkender, før din satsfil bliver opdateret. Uden opdateringskilde minder appen dig om at tjekke [skat.dk/hjaelp/satser](https://skat.dk/hjaelp/satser), når der er gået mere end 90 dage.

---

## Sådan regner appen

**Moms**
- Dansk salg: 25 % moms. Beløb inkl. moms divideres med 1,25.
- Køb med dansk moms: købsmomsen er 20 % af beløbet inkl. moms, ganget med erhvervsandelen.
- Omvendt betalingspligt: 25 % beregnes som både salgsmoms og købsmoms. Køb af ydelser fra EU går i rubrik A.
- Ikke momsregistreret: alle beløb regnes uden moms, og appen følger omsætningen op mod momsgrænsen.

**Kørsel**
- Høj sats op til km-grænsen (20.000 km), lav sats derover, regnet løbende gennem året i datoorden.

**Skat**
- Overslaget er forskellen mellem skatten med og uden virksomhedens overskud. Løn fra et job ved siden af kan indtastes, så marginalskatten bliver mere præcis.
- Med i beregningen: AM-bidrag, kommune- og kirkeskat, bund-, mellem-, top- og toptopskat, skatteloft, beskæftigelsesfradrag og jobfradrag.
- Beregnet efter personskattelovens almindelige regler, ikke virksomhedsordningen.

**Løn til dig selv**
- Hævninger er ikke en udgift og ændrer ikke overskuddet.
- «Kan stadig hæves» = overskud + indskud − hævet løn − den største af anslået skat og betalt skat.

**Frister**
- Moms: halvårligt (1. september og 1. marts) eller kvartalsvis.
- B-skat og AM-bidrag: den 20. i 10 måneder (ikke juni og december).
- Oplysningsskema: 1. juli året efter.
- Frister i en weekend flyttes til næste hverdag. Helligdage er ikke medregnet.

---

## Begrænsninger

- Afskrivninger på aktiver over småaktivgrænsen regnes ikke med. Appen markerer dem, så du kan håndtere dem selv.
- Kapitalindkomst, pension og andre fradrag er ikke med i skatteberegningen.
- Virksomhedsordningen og kapitalafkastordningen understøttes ikke.
- Helligdage er ikke med i fristberegningen. Tjek [skat.dk/frister](https://skat.dk/frister), hvis en frist ligger tæt på en helligdag.
- Har virksomheden over 300.000 kr. i omsætning to år i træk, skal du bogføre i et digitalt bogføringssystem, der lever op til bogføringsloven. Kassebog er ikke et sådant system.
- Kræver en Chromium-baseret browser på en computer.

---

## Privatliv

- HTML-filen indeholder ingen data. Alt ligger i mappen, du vælger.
- Mappens adgang huskes lokalt i browseren (IndexedDB).
- Siden henter kun skrifttyperne IBM Plex fra Google Fonts og, hvis du angiver en, din opdateringskilde for satser. Dine regnskabsdata sendes ingen steder hen.
- Tag backup af mappen sammen med dine øvrige filer, fx via cloud-synkronisering eller Git.
