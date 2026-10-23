# Drittanbieter und Versionen

## Niimbot-Web-Bluetooth

- Projekt: https://github.com/iscarelli/niimbot-web-bluetooth
- Fester Quellstand: `f20bb90175bb44413e0f37aab0d49ad910668661`
- Treiberversion laut enthaltenem Modul: `2.6.0`
- Enthalten: Demo, Registry, Niimbot-Treiber, Label-Memory und Label-Size.
- Lizenz: MIT, siehe `vendor/niimbot/LICENSE`.

Die enthaltenen Originaldateien wurden unverändert übernommen. Der Druckstudio-
Loader setzt bei der Einbindung Sprache, Titel, lokale Basisadresse, eine feste
Versionskennung für den Scriptcache sowie die Druckstudio-Oberfläche.

## PDF.js

- Projekt: https://github.com/mozilla/pdf.js
- Eingesetzte Version: `3.11.174`, entsprechend dem bisherigen klassischen
  Script-Format der App; keine Behauptung, dies sei die aktuelle PDF.js-Version.
- Enthalten: Hauptmodul, Worker, Standardschriften und komprimierte CMaps.
- PDF.js-Lizenz: Apache 2.0, siehe `vendor/pdfjs/LICENSE`.
- Weitere Ressourcenlizenzen liegen in `vendor/pdfjs/standard_fonts/` und
  `vendor/pdfjs/cmaps/`; sie wurden mitgeliefert.

Die Dokumentverarbeitung setzt ausdrücklich `isEvalSupported: false`.
Dies entspricht dem von Mozilla dokumentierten Workaround zu
CVE-2024-4367 / GHSA-wgrm-67xf-hhpq:
https://github.com/mozilla/pdf.js/security/advisories/GHSA-wgrm-67xf-hhpq

Die ursprüngliche 3.x-Bibliothek wurde zur Bewahrung des bisherigen Ladeformats
beibehalten. Der genannte Workaround ist keine vollständige Sicherheitszertifizierung
dieser älteren Bibliothek. Ein Wechsel auf einen aktuellen Modul-Build sollte
zusammen mit Tests im eingesetzten Bluefy-/iOS-Browser erfolgen.

## Nur für Entwicklertests

Die Testquellen verwenden jsdom 26.1.0, fake-indexeddb 6.2.4 und
@napi-rs/canvas 0.1.100. Diese npm-Pakete werden nicht mit der Website ausgeliefert;
ihre Installation erfolgt nur beim optionalen Ausführen der Tests. Der Font-Test
verwendet die enthaltene Liberation Sans. Die beiden Test-PDF-Seiten und die
Rasterbilder bestehen ausschließlich aus synthetischen Testinhalten.
