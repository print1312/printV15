# Niimbot Druckstudio V6 – identische Gesten für Bild und Textfeld

Diese Version korrigiert gezielt die Text-Bedienung von V5. Die Original-Niimbot-Web-Demo, die Bluetooth-Funktionen, Rollen/RFID, PDF/Bildimport, Ebenen, Schwarz-Weiß-Bildkorrekturen und Font-Upload bleiben bestehen.

## Neuer Texteditor: dasselbe Verhalten wie beim Bild

1. Datei auswählen oder über **Leeres Etikett** ein leeres Label öffnen.
2. Auf **+ Textfeld** tippen und Text eingeben.
3. Textfeld in der Vorschau antippen, um es auszuwählen. Der Hinweis *Aktiv: Textfeld* erscheint. **Nur der Text** zeigt jetzt blaue Bearbeitungsgriffe.
4. **Ein Finger:** Textfeld verschieben.
5. **Zwei Finger:** Text samt Rahmen skalieren, drehen und verschieben.
6. **Blauer Griff oben links (↻):** Textfeld stufenlos drehen.
7. **Blauer Griff rechts (↔):** Textfeldbreite ändern.
8. **Blauer Griff unten (↕):** Textfeldhöhe ändern.
9. **Blauer Griff unten rechts (⤡):** Text und Rahmen gemeinsam proportional skalieren.
10. **Rotation, Grad-Eingabe, 90°-Taste, Zoom-Prozent und Pfeile über der Vorschau** wirken beim ausgewählten Textfeld auf den Text, bei ausgewähltem Bild auf das Bild.
11. **Ausrichten** (links, mittig, rechts, oben, vertikal mittig, unten) berücksichtigt auch gedrehte Textfelder. **Einpassen** und **Füllen** wirken ebenfalls auf die aktive Auswahl.
12. Unter *Schrift / Text hinzufügen* gibt es weiterhin die direkte Eingabe der Textfeldbreite und -höhe sowie neu die **Textfeld-Zoom-%-Eingabe**.
13. Über **Bild auswählen** das Bild wieder aktivieren; alternativ außerhalb des Textfelds tippen. Die blauen Bild-Griffe erscheinen wieder.

Der **rote gestrichelte Rahmen** markiert den tatsächlichen Druckbereich, unabhängig davon, welches Element bearbeitet wird. Das erzeugte Druckbild übernimmt Texttransformation, Bildkorrekturen und die gewählte Ebenenreihenfolge.

## Veröffentlichung – neues Repository

1. ZIP entpacken und die Dateien `index.html`, `addon.js`, `.nojekyll`, `README.md` direkt in ein öffentliches GitHub-Repository hochladen.
2. GitHub: **Settings → Pages → Deploy from a branch → main → /(root) → Save**.
3. Die HTTPS-Webadresse auf dem iPhone in Bluefy öffnen.

## Vorhandenes Repository aktualisieren

Nur `index.html` und `addon.js` müssen ersetzt werden. Die Adresse und normalerweise gespeicherte Browser-Rollen/Fonts bleiben unverändert, sofern dasselbe Browserprofil und dieselbe Internetadresse weiterverwendet werden.

## Grenzen

- Die App lädt die originale Demo von GitHub/CDN zur Laufzeit und benötigt deshalb Internet.
- Web Bluetooth muss vom Browser unterstützt werden; auf dem iPhone mit Bluefy über HTTPS testen.
- Die Gesten und die Druckbild-Erzeugung wurden in einem simulierten Chromium-Test geprüft. Ein echter Niimbot-/Bluefy-Hardwaredruck ist noch nicht verifiziert.
- Die gespeicherten Fonts werden pro Browserprofil und HTTPS-Domain in IndexedDB gespeichert. Beim Löschen von Website-Daten gehen sie verloren.
