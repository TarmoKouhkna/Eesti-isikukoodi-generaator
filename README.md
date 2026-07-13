# Eesti isikukoodi generaator

Veebipõhine tööriist Eesti isikukoodide, ettevõtte registrikoodide ja fiktiivsete testidentiteetide loomiseks ning kontrollimiseks **testimise eesmärgil**.

**Proovi järele:** https://tarmokouhkna.github.io/Eesti-isikukoodi-generaator/

> Kõik genereeritud koodid, nimed, aadressid ja IBAN-id on juhuslikud ega vasta ühelegi tegelikule isikule, ettevõttele ega kontole.

## Võimalused

### Generaator
- **Neli režiimi**:
  - *Kehtivad* — terviklikud fiktiivsed identiteedid kehtiva kontrollnumbriga
  - *Vigased* — sihilikult katkised koodid (vale kontrollnumber, olematu kuupäev, vale pikkus jm) valideerimise veaharude testimiseks
  - *Piiripealsed* — keerulised kehtivad juhud, sh **18+ piiri off-by-one** (täpselt 18 täna vs. saab 18 homme), 29. veebruar liigaastal, sajandivahetus, järjekord 000/999
  - *Ettevõtted* — registrikood, KMKR number, ärinimi, IBAN, aadress
- **Vanusefilter** — genereeri sihilikult alaealisi (<18) või täisealisi (18+)
- **Lisaväljad** — vanus, nimest tuletatud e-post, aadress, test-IBAN
- **Deterministlik seeme** — sama seeme annab alati sama komplekti (korratavad testid)
- **Eksport** — CSV, JSON, `INSERT`-lause, TSV
- **Jagatav link** — konfiguratsioon URL-is (`?mode=&seed=&count=&age=`), sobib vearaportisse või CI-sse
- **ID-kaardi vaade** — esiletõstetud isik stiliseeritud isikutunnistusena (NÄIDIS-vesimärgiga)

### Valideerijad
- **Isikukood** — üks kood või terve loend. Näitab sugu, sünniaega, **vanust ja 18+ staatust**. Toetab ka sertifikaadi vormi `PNOEE-60001019906`
- **Registrikood ja KMKR** — tüüp tuvastatakse automaatselt
- **IBAN** — mod-97 kontroll, riik, pank, BIC, kontonumber
- **Telefoninumber** — formaat ja numbritüüp

### e-ID arendajale
- **SK DEMO testkontod** — kureeritud Mobiil-ID ja Smart-ID testnumbrid koos stsenaariumitega (OK, USER_CANCELLED, TIMEOUT, alla 18 jne)
- **Valideerija kood** — kopeeritav JavaScript, Python, SQL (PostgreSQL) ja Java
- **`window.EEID`** — kõik valideerimisfunktsioonid on brauserikonsoolist kättesaadavad

## Oluline: genereeritud kood ≠ töötav e-ID konto

Siin loodud koodid on **matemaatiliselt kehtivad** — need läbivad vormivalideerimise. Aga **nendega ei saa sisse logida**. Mobiil-ID või Smart-ID autentimisvoo testimiseks kasuta SK ID Solutionsi DEMO-keskkonna kontosid:

- [SK-EID/MID wiki — Mobiil-ID testnumbrid](https://github.com/SK-EID/MID/wiki/Test-number-for-automated-testing-in-DEMO)
- [SK-EID Smart-ID wiki — testkontod](https://github.com/SK-EID/smart-id-documentation/wiki/Environment-technical-parameters)
- [id.ee — teenuste testimine](https://www.id.ee/artikkel/teenuste-testimine/)

Sertifikaadi väljal `SERIALNUMBER` on isikukood riigi prefiksiga (`PNOEE-60001019906`) — levinud integratsioonivea allikas. Siinne valideerija arvestab sellega.

## Isikukoodi struktuur

| Osa | Tähendus |
|-----|----------|
| `G` | sajand ja sugu (1–8) |
| `YY MM DD` | sünnikuupäev |
| `SSS` | järjekorranumber (000–999) |
| `C` | mooduli-11 kontrollnumber |

## Kontrollnumbri algoritmid

| Kood | Pikkus | Algoritm |
|------|--------|----------|
| Isikukood | 11 numbrit | mod 11, kaalud 1–9,1 / 3–9,1,2,3 |
| Registrikood | 8 numbrit | mod 11, kaalud 1–7 / 3–9 |
| KMKR | EE + 9 numbrit | kaalud 3,7,1 kordusena; kontroll = (10 − summa mod 10) mod 10 |
| IBAN | 20 märki (EE) | ISO 13616 mod-97 |

## Eesti pangakoodid (IBAN-i 5.–6. number)

| Kood | Pank | BIC / SWIFT |
|------|------|-------------|
| 10 | SEB Pank | EEUHEE2X |
| 17 | Luminor Bank | RIKOEE22 |
| 22 | Swedbank | HABAEE2X |
| 42 | Coop Pank | EKRDEE22 |
| 77 | LHV Pank | LHVBEE22 |

## Telefoninumbri kontroll — mida saab ja mida ei saa

Tööriist kontrollib **formaati ja numbritüüpi**. Ta **ei tuvasta isikut ega operaatorit**:

- **Isikut ei saa numbri järgi tuvastada.** Elektroonilise side seadus ja GDPR keelavad sideettevõtjal abonendi andmete avaldamist; neid saavad välja nõuda vaid politsei, prokuratuur või kohus.
- **Operaatorit ei saa prefiksist järeldada**, sest numbriliikuvus lubab numbri operaatorite vahel kaasa võtta.

| Allikas | Mida annab |
|---------|-----------|
| [TTJA numbrikuuluvuse päring](https://nba.ttja.ee/numbriparing.aspx) | Millisele sideettevõtjale number kuulub |
| [Äriregister](https://ariregister.rik.ee/) | Kontakt, kui number kuulub ettevõttele |
| [1182 kataloog](https://www.1182.ee/) | Avalikustamisega nõustunud kontaktid |
| [Avaldus politseile](https://www.politsei.ee/et/avaldus-politseile) | Ahistamise või kelmuse korral |

Hädaabi **112** · Riigiinfo **1247**

## Kasutamine

Ava [veebiversioon](https://tarmokouhkna.github.io/Eesti-isikukoodi-generaator/) või lae repo alla ja ava `index.html` brauseris. Sõltuvusi pole.

## Litsents

Vaba kasutus testimiseks.
