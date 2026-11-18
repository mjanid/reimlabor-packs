# reimlabor-packs

Öffentliche Seite zur iOS-App Reimlabor (GitHub Pages): Datenschutzerklärung und die signierten
Wörterbuchpakete, die die App auf Wunsch lädt.

```
datenschutz.html, index.html, style.css   Website
v1/manifest.json, v1/manifest.sig         Paketliste mit Prüfsummen und ihre Ed25519-Signatur
releases/<Version>/                       Pakete (SQLite, xz-komprimiert) und LICENSES.txt
```

Die App lädt `v1/manifest.json`, prüft die Signatur gegen einen in der App hinterlegten öffentlichen
Schlüssel und danach Größe und SHA-256 jedes Pakets. Songtexte werden dabei nicht übertragen.

## Pakete 2026.11.0

| Paket | Inhalt | Lizenz |
|---|---|---|
| `de-core` | 220 496 deutsche Wörter mit Aussprache, Reimschlüsseln und Häufigkeitsrang | CC BY-SA 4.0 |
| `en-core` | 20 000 englische Wörter mit Aussprache | BSD-2-Clause (CMU) |

### Quellen

- **Deutsches Wiktionary** (CC BY-SA 4.0, https://de.wiktionary.org), Aussprachen in der Aufbereitung von
  [german-ipa-dict](https://github.com/devio-at/german-ipa-dict), Stand
  [`a08113e`](https://raw.githubusercontent.com/devio-at/german-ipa-dict/a08113e0ab80f049b625fc360196491f56243ca1/de_dewikt.csv)
  (SHA-256 `1021fa07108658e4837388229d1e9b3e12a2d88e9a4009fcb548aa3d60daa699`).
- **FrequencyWords / OpenSubtitles 2018** (CC BY-SA 4.0), Worthäufigkeiten, Stand
  [`525f9b5`](https://raw.githubusercontent.com/hermitdave/FrequencyWords/525f9b560de45753a5ea01069454e72e9aa541c6/content/2018/de/de_full.txt)
  (SHA-256 `a5fc13f4efaaf70fd9226d11295fd3cd4c2264852ee1fad22c0abaf64acec8dc`).
- **CMU Pronouncing Dictionary** (BSD-2-Clause, https://github.com/cmusphinx/cmudict), englische Aussprachen.
  Copyright (C) 1993-2015 Carnegie Mellon University. Der vollständige Lizenztext steht in
  `releases/2026.11.0/LICENSES.txt`.

### Änderungen gegenüber den Quellen

- Die IPA-Aussprachen aus Wiktionary sind in eine kompakte Lautschrift mit einem Zeichen je Laut
  umgeschrieben. 24 Zeilen ließen sich nicht umschreiben und fehlen.
- Aufgenommen sind Wörter mit einem Häufigkeitseintrag. Hat ein Wort mehrere Aussprachen, steht eine
  als Hauptaussprache, die übrigen als Varianten.
- Zu jedem Wort sind Silbenzahl, Vokalfolge und Reimschlüssel vorberechnet; der Rang folgt der Häufigkeit.
- Eine kleine kuratierte Liste (Umgangssprache, Marken, Rap-Vokabular) ergänzt das Paket.
- Die englischen Aussprachen sind für deutsche Ohren in dieselbe Lautschrift umgeschrieben.

### Lizenz der Pakete

`de-core` ist eine Bearbeitung von CC-BY-SA-Daten und steht selbst unter
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de). Du darfst das Paket nutzen,
weitergeben und bearbeiten, wenn du die Quellen nennst und Bearbeitungen unter derselben Lizenz
weitergibst. `en-core` steht unter der BSD-2-Clause-Lizenz des CMU Pronouncing Dictionary.

Die Pakete sind SQLite-Dateien: `xz -d de-core.sqlite.xz`, dann mit jedem SQLite-Werkzeug lesbar
(Tabellen `word` und `meta`).
