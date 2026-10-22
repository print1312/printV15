# Niimbot Druckstudio V14 – Vorlagen und freier Bearbeitungsbereich

Die Web-App baut auf V13 und auf der ursprünglichen [iscarelli/niimbot-web-bluetooth](https://github.com/iscarelli/niimbot-web-bluetooth)-Demo auf. Die Original-Demo wird zur Laufzeit über HTTPS geladen, sodass die Modell-/Bluetooth-Auswahl und die vorhandene Rollenverwaltung weiterverwendet werden.

## Neu in V14

### Roter Druckrahmen um 90° drehen

Unter **⌖ Ausrichten → Roten Druckrahmen 90° drehen** wechselt die Vorschau zwischen Hoch- und Querformat. Diese Einstellung betrifft den **gesamten Etiketten-/Druckbereich**, nicht nur ein Bild oder ein Textfeld. Die Bild- und Textobjekte bleiben individuell bearbeitbar. Beim Drucken wird das Bild wieder passend zu den vom Treiber erwarteten physischen Abmessungen der gewählten Rolle gerastert und ausgerichtet.

### Inhalte außerhalb des Druckbereichs

Mit **Außen zeigen** direkt über der Vorschau (oder dem Kontrollkästchen im Tab **Ausrichten**) werden Bilder und Texte auch außerhalb der gestrichelten roten Grenze dargestellt. Die Umrisse nicht ausgewählter Ebenen werden dezent gestrichelt gezeigt. So lassen sich überstehende Bereiche auswählen und verschieben. **Gedruckt wird ausschließlich, was sich im roten Rahmen befindet.** „Außen ausblenden“ zeigt wieder nur den bedruckbaren Bereich. Der seitliche Ansichts-Zoom skaliert ausschließlich die Ansicht, nicht die Druckdaten.

### Vorlagen speichern und wiederverwenden

Unten auf **💾 Save** oder auf den Tab **💾 Vorlagen** tippen. Du kannst:

- einen Vorlagennamen und Ordner eingeben,
- mit **Speichern** die aktuelle Vorlage neu speichern oder ihre frühere Version überschreiben,
- mit **Speichern unter …** eine eigenständige Kopie anlegen,
- mit **↓ Als Datei** ein vollständiges Backup als `.niimbot-label.json` herunterladen,
- exportierte Vorlagen mit **↑ Datei öffnen** wieder importieren,
- gespeicherte Vorlagen nach Name oder Ordner suchen,
- über die Vorlagenliste **Bearbeiten**, **Kopie**, **+ Warteschlange**, **🖨 Drucken**, **↓ Datei** und **Löschen** verwenden.

Bei **🖨 Drucken** wird nur die ausgewählte gespeicherte Vorlage an den verbundenen Drucker geschickt; bereits vorhandene Aufträge in der Warteschlange bleiben unverändert. Vor dem Druck bitte die eingelegte Etikettenrolle mit den oben gewählten Abmessungen abgleichen.

**Wichtig zur Speicherung:** Die Vorlagen werden in **IndexedDB des jeweiligen Browsers unter genau dieser Website-Adresse** gespeichert. Damit sind sie bei späteren Besuchen derselben Website im selben Browserprofil wieder verfügbar, solange die Browserdaten nicht entfernt werden. Es handelt sich **nicht um einen Cloud-Server mit Benutzerkonten**: Ein anderes iPhone, ein anderer Browser oder ein neues GitHub-Pages-Repository hat einen getrennten Speicher. Verwende JSON-Export/-Import für Übertragung und Backups. Für eine echte browserübergreifende Cloud-Synchronisation wäre ein zusätzlicher Server mit Nutzeranmeldung notwendig.

### Gespeicherte Etiketten auf neuen Rollengrößen

Beispiel: Eine Vorlage wurde auf **50 × 30 mm** gestaltet, im oberen Druckermenü wird jetzt **80 × 50 mm** eingestellt.

Beim Öffnen der gespeicherten Vorlage mit abweichender Rollengröße wird das gesamte ursprüngliche Etikett zu einer **zusammenhängenden Bilddatei**. Diese wird im neuen roten Rahmen wie beim Bildimport behandelt: Du kannst sie verschieben, skalieren, rotieren und zuschneiden. Der alte Entwurf bleibt unverändert im Vorlagenspeicher. Bei **gleicher Rollengröße** werden die einzelnen Bild- und Textebenen zum Weiterbearbeiten geladen. Wird eine bereits geöffnete editierbare gespeicherte Vorlage auf eine andere Rollengröße umgestellt, wird sie ebenfalls als Gesamtbild übernommen.

## Installation in GitHub Pages

1. Die ZIP entpacken. Darin liegen `index.html`, `addon.js`, `.nojekyll` und diese `README.md`.
2. In einem **neuen GitHub-Repository** die Dateien ins **Hauptverzeichnis** laden. In einem vorhandenen Repository `index.html` und `addon.js` durch diese Version ersetzen. Bestehende Dateien vorher sichern.
3. **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main → Folder: /(root) → Save** wählen.
4. GitHub veröffentlicht die Website unter `https://BENUTZERNAME.github.io/REPOSITORYNAME/`.
5. Auf dem iPhone diese **HTTPS-Adresse** mit einem Browser öffnen, der Web Bluetooth für das jeweilige Gerät bereitstellt (z. B. Bluefy, soweit dort unterstützt); auf Desktop Chromium/Chrome verwenden.
6. Oben Druckermodell, Etikettengröße und Dichte einstellen, **Drucker verbinden**, vorhandene RFID-/Rolleneinstellungen verwenden und zunächst nur **ein Testetikett** drucken.

Die Anwendung benötigt beim Aufruf Internet, um die ursprüngliche Niimbot-Demo (GitHub/jsDelivr) zu laden. Ein lokales Öffnen der HTML-Datei ist für Web-Bluetooth-Druck nicht vorgesehen; nutze GitHub Pages oder eine andere HTTPS-Website.

## Bisherige Funktionen

Die zuvor vorhandenen Funktionen bleiben angebunden: PDF/PNG/JPG-Dateiimport mit DPI, mehrere Bilder und Textfelder, Ebenenreihenfolge und Ebenensperren, freie Zuschnitte einschließlich Kreis und Seitenverhältnis-Vorgaben, Bildkorrekturen mit Slidern und Zahlenfeldern, Touch-Gesten, Elementrotation, Schriftarten-Upload, invertierte Textfelder, Rundtext/Kreisbogen, Rückgängig/Wiederholen, Stapeldruck, Rollenverwaltung und Debug-Log.

## Technische Prüfung

- JS-Syntax mit Node.js geprüft.
- Simulierter mobiler Chromium-DOM-Test: Text hinzufügen, Vorlage speichern, Kopie öffnen, eigene Vorlage erneut drucken, Save As, 90°-Druckrahmen, neue Etikettengröße als Gesamtbild, Vorschau außerhalb des Druckbereichs, simulierten Stapeldruck. Es wurden keine JavaScript-Laufzeitfehler gemeldet.
- Die Pixelkontrolle für ein außerhalb des roten Rahmens platziertes schwarzes Bild war erfolgreich.
- Der **echte Druck mit Hardware und iPhone/Bluefy ist nicht getestet**. Die Original-Verbindungslogik bleibt unverändert; unbekannte Niimbot-Modelle können Einschränkungen haben.
