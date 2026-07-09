# Eesti isikukoodi generaator

Lihtne veebipõhine tööriist Eesti isikukoodide genereerimiseks **testimise eesmärgil**.
Loodud koodidel on kehtiv mooduli-11 kontrollnumber ja juurde käib fiktiivne eesti nimi.

> Kõik koodid ja nimed on juhuslikult loodud ega vasta ühelegi tegelikule isikule.

## Võimalused

- Kehtiva kontrollnumbriga koodide genereerimine
- Soo valik (juhuslik / mees / naine) ja sünniaasta vahemik (1800–2199)
- Koodi ülesehituse visuaalne selgitus (`G YY MM DD SSS C`)
- Fiktiivne eesti nimi iga koodi juurde
- Kopeerimine ükshaaval või kõik korraga TSV-formaadis (`kood⇥nimi`)
- Sisseehitatud valideerija olemasoleva koodi kontrollimiseks

## Kasutamine

Ava `index.html` brauseris. Muid sõltuvusi pole.

## Koodi struktuur

| Osa | Tähendus |
|-----|----------|
| `G` | sajand ja sugu (1–8) |
| `YY MM DD` | sünnikuupäev |
| `SSS` | järjekorranumber (000–999) |
| `C` | mooduli-11 kontrollnumber |

## Litsents

Vaba kasutus testimiseks.
