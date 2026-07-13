# Eesti isikukoodi generaator

Veebipõhine tööriist Eesti isikukoodide ja fiktiivsete testidentiteetide loomiseks ning kontrollimiseks **testimise eesmärgil**. Loodud koodidel on kehtiv mooduli-11 kontrollnumber.

**Proovi järele:** https://tarmokouhkna.github.io/Eesti-isikukoodi-generaator/

> Kõik koodid, nimed ja IBAN-id on juhuslikult loodud ega vasta ühelegi tegelikule isikule ega kontole.

## Võimalused

- **Kolm režiimi**:
  - *Kehtivad* — terviklikud fiktiivsed identiteedid kehtiva kontrollnumbriga
  - *Vigased* — sihilikult katkised koodid (vale kontrollnumber, olematu kuupäev, vale sugu-number, vale pikkus jm), valideerimise veaharude testimiseks
  - *Piiripealsed* — keerulised kehtivad juhud (29. veebruar liigaastal, sajandivahetus, järjekord 000/999, vanim/tulevikusajand, täna sündinu)
- **ID-kaardi vaade** — esiletõstetud isik stiliseeritud isikutunnistusena (NÄIDIS-vesimärgiga)
- **Isikukoodid** kehtiva kontrollnumbriga; soo valik ja sünniaasta vahemik (1800–2199)
- **Koodi ülesehituse selgitus** (`G YY MM DD SSS C`)
- **Fiktiivsed eesti nimed** vastavalt soole
- **Lisaväljad** (valitavad): vanus, nimest tuletatud e-post, aadress (tänav, sihtnumber, linn) ja test-IBAN
- **Test-IBAN** kehtiva mod-97 kontrollnumbriga, tegelike pangaprefiksitega
- **Deterministlik seeme** — sama seeme annab alati sama komplekti (korratavad testid)
- **Eksport** — CSV ja JSON allalaadimine, `INSERT`-lause kopeerimine
- **Isikukoodi valideerija** — kontrolli üht koodi või kleebi terve loend korraga (pass/fail + põhjus)
- **IBAN-i kontroll** — mod-97 valideerimine ning riigi, panga, BIC-i ja kontonumbri tuletamine
- **Telefoninumbri kontroll** — formaadi ja numbritüübi tuvastus (mobiil, lauatelefon, 800/900 teenusnumber, lühinumber, hädaabi) ning E.164 vorming
- **Sisseehitatud kasutusjuhend** lehel

## Kasutamine

Ava veebiversioon [siit](https://tarmokouhkna.github.io/Eesti-isikukoodi-generaator/) või lae repo alla ja ava `index.html` brauseris. Sõltuvusi pole.

## Isikukoodi struktuur

| Osa | Tähendus |
|-----|----------|
| `G` | sajand ja sugu (1–8) |
| `YY MM DD` | sünnikuupäev |
| `SSS` | järjekorranumber (000–999) |
| `C` | mooduli-11 kontrollnumber |

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

- **Isikut ei saa numbri järgi tuvastada.** Elektroonilise side seadus ja GDPR keelavad sideettevõtjal abonendi andmete avaldamist kolmandale isikule; neid saavad välja nõuda vaid politsei, prokuratuur või kohus.
- **Operaatorit ei saa prefiksist järeldada**, sest numbriliikuvus lubab abonendil operaatorit vahetades numbri kaasa võtta. Numbri tegeliku kuuluvuse saab kontrollida [TTJA numbrikuuluvuse päringust](https://nba.ttja.ee/numbriparing.aspx).
- Ahistamise või kelmuse korral tee avaldus politseile (politsei.ee).

Eesti numbriseeriad: mobiil 50–59 ja 81–84 (7–8 numbrit), lauatelefon 32–33, 35, 38–39, 43–48, 60–68, 71–79, 88 (7 numbrit), teenusnumbrid 800 (tasuta) ja 900 (tasuline), riigikood +372.

## Litsents

Vaba kasutus testimiseks.
