# Meine Nachrichten

Tägliches Börsen-Briefing – **https://nachrichten.kompassapps.de**

Die Seite wird automatisch von Claude befüllt: jeden Morgen (Mo–Fr 6:38 Uhr, Sa/So 8:36 Uhr) und zusätzlich Mo–Fr um 20 Uhr mit einer Abend-Ausgabe.
Die Seite selbst (`index.html`) bleibt gleich, jeden Tag kommt nur eine neue Datei in `data/` dazu.

## Aufbau

- `data/index.json` – Liste aller Ausgaben (neueste zuerst)
- `data/JJJJ-MM-TT.json` – Morgen-Ausgabe (bzw. Wochenend-Ausgabe)
- `data/JJJJ-MM-TT-abend.json` – Abend-Ausgabe (Mo–Fr, `"typ": "abend"`)

### data/index.json

```json
{ "ausgaben": [ { "datum": "2026-11-12", "datei": "2026-11-12.json", "schlagzeile": "…" } ] }
```

### data/JJJJ-MM-TT.json

```json
{
  "datum": "2026-11-12",
  "typ": "werktag",                 // oder "wochenende"
  "erstellt": "2026-11-12T06:41:00+01:00",
  "schlagzeile": "Ein Satz, was heute am wichtigsten ist",
  "kurz": ["5–8 kurze Sätze als Absätze"],
  "kennzahlen": [
    { "gruppe": "US-Börsen (Schluss)", "werte": [
      { "name": "S&P 500", "wert": "7.353,73", "veraenderung": -4.36, "hinweis": "schlechtester Tag seit April 2025" }
    ]}
  ],
  "maerkte": [ { "titel": "USA", "text": ["Absatz", "Absatz"] } ],
  "nachrichten": [ { "titel": "…", "text": ["…"], "quellen": [ { "name": "Reuters", "url": "https://…" } ] } ],
  "termine":  [ { "tag": "", "zeit": "14:30", "titel": "US-Arbeitsmarktbericht", "art": "Wirtschaftsdaten", "wichtig": true, "warum": "…" } ],
  "ausblick": [ { "tag": "Fr.", "zeit": "10:00", "titel": "…", "art": "…", "warum": "…" } ],
  "quellen":  [ { "name": "…", "url": "https://…" } ]
}
```

- `veraenderung` ist eine Zahl in Prozent (positiv = grün, negativ = rot), `wert` ist ein fertig formatierter Text.
- `"umgekehrt": true` dreht die Farben um (z. B. beim VIX oder bei Anleihe-Renditen: steigend = rot).
- `tag` bei Terminen nur am Wochenende bzw. im Ausblick nötig (z. B. „Mo.“).
- Links nur mit `https://`.
- Keine Kauf- oder Verkaufsempfehlungen.

### Abend-Ausgabe

- Datei `data/JJJJ-MM-TT-abend.json`, gleiches Format, aber `"typ": "abend"`.
- In `data/index.json` ein eigener Eintrag mit gleichem `datum` und `"datei": "JJJJ-MM-TT-abend.json"`.
- Morgen- und Abend-Ausgabe desselben Tages stehen beide in `index.json`; doppelt darf nur dieselbe **Datei** nicht sein.
- `termine` = heute Abend und in der Nacht (z. B. Zahlen nach US-Börsenschluss), `ausblick` = morgen (mit `"tag"`).
- Auf der Seite erscheint sie als „· Abend“; der Link lautet `?tag=JJJJ-MM-TT-abend`.
