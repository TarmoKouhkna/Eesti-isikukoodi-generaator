# Eesti isikukoodi generaator

Veebipõhine tööriist Eesti isikukoodide ja fiktiivsete testidentiteetide loomiseks ning kontrollimiseks **testimise eesmärgil**. Loodud koodidel on kehtiv mooduli-11 kontrollnumber.

> Kõik koodid, nimed ja IBAN-id on juhuslikult loodud ega vasta ühelegi tegelikule isikule ega kontole.

## Võimalused

- **Isikukoodid** kehtiva kontrollnumbriga; soo valik ja sünniaasta vahemik (1800–2199)
- **Koodi ülesehituse selgitus** (`G YY MM DD SSS C`)
- **Fiktiivsed eesti nimed** vastavalt soole
- **Test-IBAN** iga isiku juurde (kehtiv mod-97 kontrollnumber, tegelikud pangaprefiksid)
- **Deterministlik seeme** — sama seeme annab alati sama komplekti (korratavad testid)
- **Eksport** — CSV ja JSON allalaadimine, `INSERT`-lause kopeerimine
- **Isikukoodi valideerija** — kontrolli üht koodi või kleebi terve loend korraga (pass/fail + põhjus)
- **IBAN-i kontroll** — mod-97 valideerimine ning riigi, panga, BIC-i ja kontonumbri tuletamine

## Kasutamine

Ava `index.html` brauseris. Sõltuvusi pole.

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

## Litsents

Vaba kasutus testimiseks.
