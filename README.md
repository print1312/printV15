# Niimbot Druckstudio V15 – geprüfte Überarbeitung

Überarbeitung der hochgeladenen V14-App. 86 automatisierte Prüfungen sind
bestanden. Die einzelnen Ergebnisse und die Grenzen der Prüfung stehen in
`TESTBERICHT.md`. Echte Ausdrucke und die Bedienung auf iPhone/Bluefy wurden
in dieser Umgebung nicht geprüft.

## Bestehende Website aktualisieren

1. Bisherige App-Dateien sichern. Wichtige Vorlagen in V14 zusätzlich als JSON exportieren.
2. Die ZIP entpacken. `index.html`, `addon.js`, `.nojekyll` und den **vollständigen
   Ordner `vendor`** in dasselbe Hauptverzeichnis des bisherigen GitHub-Pages-
   Repositories bzw. HTTPS-Webservers übertragen. Vorhandene App-Dateien ersetzen.
3. Veröffentlichung abwarten und die bisherige HTTPS-Adresse neu laden. Im Kopf
   der App muss **V15** stehen. Ein erneutes Laden kann bei altem Browsercache nötig sein.
4. Druckermodell, Rolle und Dichte prüfen, verbinden und zuerst ein einzelnes
   Testetikett ausgeben. Danach 90°-Ausrichtung, Kopien und Stopp prüfen.

Die Ordnerstruktur unbedingt erhalten: Neben `index.html` liegt `addon.js`;
darunter liegen `vendor/niimbot` und `vendor/pdfjs`. Nur die beiden JavaScript-/
HTML-Dateien hochzuladen reicht bei V15 nicht mehr. `pruefung` enthält die
reproduzierbaren Entwicklertests und wird für den Websitebetrieb nicht benötigt.

Für eine neue GitHub-Pages-Website die Dateien ins Repository-Hauptverzeichnis
laden und dort Pages aus dem gewünschten Branch und `/(root)` veröffentlichen.
Die App muss über HTTPS oder eine geeignete lokale Entwicklungsadresse laufen.
Das direkte Öffnen per `file://` ist kein unterstützter Betriebsweg.

## Behobene Fehler und verbesserte Abläufe

- **Vorschau und Gesten:** tatsächliche Canvas-Abmessungen, passende Touch-
  Koordinaten, serielles Neuzeichnen, keine veralteten Auswahlgriffe nach dem Leeren,
  zuverlässigeres Verschieben kleiner Texte und Begrenzung auf zwei aktive Finger.
- **Rundtext und Schrift:** Vollkreis mit 360°, gerader Text bei 0°, ausreichend
  großer Rahmen für manuelle Radien, korrekte generische Schriftfamilien und
  durchgängiger Schutz gesperrter Ebenen, auch im Rundtext-Tab.
- **Bilder und Beschnitt:** gleichartige Bildkorrektur für Ansicht und Druck,
  Wiederverwendung berechneter Filter, Filtercache bis zwölf Millionen Pixel,
  Freigabe dekodierter Bilder inaktiver Etiketten, Erhalt von Position/Rotation/Zoom
  beim Zuschneiden. Der Import-Beschnitt wird anschließend passend eingepasst.
- **Rückgängig/Wiederholen:** einzelne schnelle Klicks bleiben einzelne Schritte;
  Loslassen eines Reglers außerhalb schließt die Geste; verschiedene Binärdateien
  werden zuverlässig unterschieden. Änderungen an Druckgröße und Modell können
  zusammen mit den betroffenen Vorlagen zurückgenommen werden.
- **Vorlagen:** Name und Ordner folgen dem ausgewählten Etikett; unabhängige
  Speicherkopien und konsistente Exporte; eigene Schriftdateien in neuen Vorlagen
  und JSON-Backups enthalten; fehlerhafte Importe werden vor dem Speichern
  abgewiesen. Mehrfachimporte sind atomar.
- **Rollengrößen:** alle geöffneten gespeicherten Vorlagen werden bei einem Wechsel
  berücksichtigt. Gleiche physische Maße unter anderem Größenschlüssel behalten
  ihr Layout. Andere Maße führen weiterhin zur Übernahme als ein Gesamtbild;
  das gespeicherte Original bleibt erhalten.
- **PDF und Dateiimport:** enthaltene PDF-Schriften und Zeichentabellen,
  deaktivierte Eval-Auswertung, Ressourcenfreigabe nach PDF-Verarbeitung,
  nachvollziehbare Angaben zu übersprungenen Dateien, Begrenzung der Warteschlange
  und Schutz gegen überlappende Importe.
- **Druck:** fester Auftrag mit festgehaltenen Daten und Einstellungen; währenddessen
  keine Bearbeitung; sichtbarer Stopp; ganze Kopienzahlen von 1 bis 30;
  Abbruch vor der nächsten Kopie. Ein laufendes Etikett kann noch ausgegeben
  werden. Fehler lösen keine automatische Wiederholung aus.
- **Auslieferung:** Druckertreiber, Registry und PDF-Ressourcen sind mitgeliefert.
  Beim normalen Start wird kein veränderlicher externer `main`-Zweig geladen.

## Vorlagen und Schriftarten behalten

Die bestehenden IndexedDB-Namen aus V14 bleiben unverändert. Daten gehören zum
Browserprofil und zur Website-Origin (Protokoll, Hostname, Port). Verschiedene
Repository-Pfade unter derselben `BENUTZERNAME.github.io`-Domain teilen diesen
Speicher; eine andere Domain oder ein anderes Browserprofil besitzt einen
anderen Speicher. Das Löschen von Browserdaten kann Vorlagen und Fonts entfernen.

Es gibt keine Cloud-Synchronisation. JSON-Export/-Import dient als Backup und
zur Übertragung. Frühere V14-Exporte enthalten keine Schriftdateien; die damals
verwendeten eigenen Fonts gegebenenfalls zusätzlich hochladen. Neue V15-Exporte
enthalten die verwendeten, verfügbaren eigenen Schriftarten.

## Prüfung und Drittanbieter

`TESTBERICHT.md` enthält die Prüfungsergebnisse, `pruefung/` die Tests und
maschinenlesbaren Resultate, `DRITTANBIETER.md` die Versions- und Lizenzangaben.
`PRUEFSUMMEN.sha256` enthält SHA-256-Prüfsummen aller ausgelieferten Dateien
außer der Prüfsummendatei selbst.

Die App verwendet weiterhin den Niimbot-Web-Bluetooth-Treiber des ursprünglichen
Projekts. Modell-, Firmware- und Browserkompatibilität müssen mit dem tatsächlich
eingesetzten Gerät geprüft werden. Dieses Paket ist keine Offline-PWA.
