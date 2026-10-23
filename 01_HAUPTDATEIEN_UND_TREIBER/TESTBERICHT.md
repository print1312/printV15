# Testbericht – Niimbot Druckstudio V15

Stand: 23. Oktober 2026. Grundlage: die erneut bereitgestellte Datei
`niimbot-druckstudio-v14-vorlagen-hochkant(1).zip`.

**Ergebnis: 86 von 86 automatisierten Prüfungen bestanden.**
Die final ausgelieferten App-Dateien wurden mit den im Paket enthaltenen Tests
ausgeführt. Es gab keine unerwarteten DOM-Ausnahmen oder Vorschaufehler.

## Was tatsächlich geprüft wurde

Der echte Druckstudio-Code startet zusammen mit der Original-Demo und den
mitgelieferten Niimbot-Modulen in jsdom. Canvas-Bilder und PNG/JPEG-Dateien werden
mit einer nativen Rasterbibliothek verarbeitet. IndexedDB wird durch
fake-indexeddb simuliert. Die PDF-Prüfung verwendet die enthaltene PDF.js-Version
mit einem echten zweiseitigen PDF. Vorlagen werden gespeichert, exportiert,
importiert und in einer neuen DOM-Instanz wieder geöffnet. Echte TTF-Fontbytes
werden geladen und in Vorlagen eingebettet.

Die Tests verwenden sichtbare Bedienelemente, DOM-Ereignisse und gezielte direkte
Aufrufe der App-Funktionen. Bei Drucktests wird die Druckerschnittstelle simuliert;
Auftragsdaten, Anzahl, Stopp, Fehlerbehandlung und Sperrzustände werden geprüft.
Es werden weder Bluetooth-Pakete an Hardware gesendet noch reale Etiketten gedruckt.

## Vorher reproduzierte Fehler

| V14-Situation | Beobachtung | V15-Korrektur |
| --- | --- | --- |
| Vorschaufläche mit 225 × 150 CSS-Pixeln | Berechnung mit 260 × 240 Pixeln | Tatsächliche Maße und skalierte Zeigerkoordinaten |
| Vollkreis bei bisherigem 180°-Wert | Identische Rasterung wie Halbkreis | Vollkreis fest mit 360° |
| Bogenwinkel 0° | Identische Rasterung wie 180° | Nullwert bleibt erhalten |

Diese V14-Beobachtungen stehen zusätzlich in `pruefung/v14-baseline.json`.
Im PDF-Test wurden zunächst fehlende Standardschrift-Ressourcen sichtbar.
Nach Ergänzung der Fonts wird Text in der oberen Seitenhälfte anhand schwarzer
Pixel geprüft; das resultierende Rasterbild wurde zusätzlich visuell kontrolliert.
Auch das Rasterbild eines invertierten Textfelds wurde visuell kontrolliert.

## Grenzen und Prüfung auf dem Zielgerät

Dies sind **keine Tests in einer echten Browser-Layoutengine**. jsdom berechnet
kein CSS-Layout; Canvas-Maße und Pointer-Ereignisse werden als Testwerte vorgegeben.
Chromium war in dieser Umgebung nicht installiert. iOS, Bluefy, native
Bildschirmtastatur, tatsächliche Finger-Gesten, Betriebssystem-Speicherbereinigung,
Bluetooth-Verbindungsaufbau, RFID-Rollenlesung und physische Druckqualität wurden
nicht verifiziert. Die Ergebnisse sind daher keine Garantie für jeden Browser,
jede Firmware oder jedes Druckermodell.

Nach dem Hochladen auf dem tatsächlich verwendeten Gerät prüfen:

1. V15-Anzeige, Vorschau und Werkzeugbereich bei Hoch-/Querformat sowie geöffneter Tastatur.
2. Bild- und Textebenen verschieben, mit zwei Fingern skalieren, zuschneiden und sperren.
3. Vorlage mit eigener Schrift speichern, Browser schließen, erneut öffnen und JSON-Backup testen.
4. Rollengröße wechseln, gespeicherte Vorlage übernehmen und per Undo zurückkehren.
5. Ein einzelnes Etikett drucken; anschließend 90°-Ausrichtung, mehrere Kopien und Stopp testen.

## Einzelprüfungen

| Nr. | Prüfung | Ergebnis |
| ---: | --- | --- |
| 1 | Start mit mitgeliefertem Treiber und acht Werkzeug-Tabs | Bestanden |
| 2 | Alle DOM-IDs eindeutig | Bestanden |
| 3 | Leere Warteschlange deaktiviert Drucken und Textbearbeitung | Bestanden |
| 4 | Vorschau nutzt tatsächliche 225 × 150 CSS-Pixel | Bestanden |
| 5 | Koordinaten bei CSS-Skalierung korrekt | Bestanden |
| 6 | Leeres Etikett und editierbares Textfeld erstellen | Bestanden |
| 7 | Schnelle Klicks bleiben getrennte Undo-Schritte | Bestanden |
| 8 | Neue Bearbeitung verwirft Redo-Zweig | Bestanden |
| 9 | Textformatierung, Inversdruck und Zahlenlimits | Bestanden |
| 10 | Generische Schriftfamilien werden korrekt gesetzt | Bestanden |
| 11 | Vollkreis verwendet 360° und unterscheidet sich vom Halbkreis | Bestanden |
| 12 | 0°-Bogen bleibt gerade statt auf 180° zurückzufallen | Bestanden |
| 13 | Manueller Radius erweitert den Text-Rahmen | Bestanden |
| 14 | Gegenüberliegenden Rundtext kopieren | Bestanden |
| 15 | Gesperrte Ebene schützt auch Rundtext-Steuerung | Bestanden |
| 16 | Verschieben eines kleinen Textfeldes greift nicht versehentlich den Rahmen | Bestanden |
| 17 | Zweifinger-Geste skaliert Text und ignoriert dritten Finger | Bestanden |
| 18 | Ausrichten und Rotation verändern das gewählte Element | Bestanden |
| 19 | Ansichts-Zoom verändert keine Druckpixel | Bestanden |
| 20 | 90°-Etikett wird auf physische Druckmaße zurückgerastert | Bestanden |
| 21 | Invertierter Text enthält schwarze Fläche und weiße Schrift | Bestanden |
| 22 | PNG als Etikett und JPEG als zusätzliche Ebene | Bestanden |
| 23 | Beschnitt-Presets halten alle vorgegebenen Seitenverhältnisse | Bestanden |
| 24 | Beschnitt abbrechen lässt Bild unverändert | Bestanden |
| 25 | Beschnitt bewahrt vorhandene Rotation und Zoom | Bestanden |
| 26 | Beschnitt ist rückgängig zu machen | Bestanden |
| 27 | Ungültige Beschnittwerte werden auf gültige Fläche begrenzt | Bestanden |
| 28 | Bildkorrekturen und Gamma bleiben innerhalb ihrer Grenzen | Bestanden |
| 29 | Pixelkorrekturen werden zwischen Gesten wiederverwendet | Bestanden |
| 30 | Ebenenreihenfolge und Sperre funktionieren | Bestanden |
| 31 | Entfernen des Hauptbildes erhält zusätzliche Bildebenen | Bestanden |
| 32 | Entfernen früherer Etiketten bewahrt die ausgewählte Seite | Bestanden |
| 33 | Außenansicht beeinflusst Druckpixel nicht | Bestanden |
| 34 | Regler-Loslassen außerhalb beendet History-Geste | Bestanden |
| 35 | Gleich große verschiedene Blobs ergeben verschiedene History-Zustände | Bestanden |
| 36 | Vorlage mit Name und Ordner dauerhaft speichern | Bestanden |
| 37 | Gespeicherte Vorlage ist unabhängig von weiteren Änderungen | Bestanden |
| 38 | Vorlagenkopie wird als unabhängiges Etikett geöffnet | Bestanden |
| 39 | Speichern unter legt eine neue Vorlage an | Bestanden |
| 40 | Bearbeiten aktualisiert dieselbe gespeicherte Vorlage | Bestanden |
| 41 | Etikettenwechsel synchronisiert Vorlagennamen | Bestanden |
| 42 | Vorlagen-JSON lässt sich exportieren und wieder importieren | Bestanden |
| 43 | Beschädigte oder fremde JSON-Datei verändert keine Vorlagen | Bestanden |
| 44 | Manipulierte Proto-Felder werden abgelehnt | Bestanden |
| 45 | Mehrfachimport ist bei ungültigem zweiten Datensatz atomar | Bestanden |
| 46 | Überdimensionierte Vorlage wird vor dem Rendern zurückgewiesen | Bestanden |
| 47 | TTF wird in Vorlagen und JSON eingebettet | Bestanden |
| 48 | Neue Rollengröße wandelt alle geöffneten gespeicherten Vorlagen um | Bestanden |
| 49 | Undo nach Größenwechsel stellt Rolle und editierbare Texte wieder her | Bestanden |
| 50 | Gleiche physische Größe unter anderem Schlüssel behält Layout | Bestanden |
| 51 | Druckkopien werden auf ganze Werte zwischen 1 und 30 begrenzt | Bestanden |
| 52 | Fehlende Verbindung löst keinen Druck aus und entsperrt Editor | Bestanden |
| 53 | Falsches Druckermodell wird vor Ausgabe zurückgewiesen | Bestanden |
| 54 | Druckauftrag friert Modell, Größe und Bearbeitung ein | Bestanden |
| 55 | Stopp ist sichtbar und hält vor der nächsten Kopie an | Bestanden |
| 56 | Druckfehler erhält Warteschlange und versucht nicht automatisch erneut | Bestanden |
| 57 | Gespeicherte Vorlage drucken lässt aktuelle Warteschlange unverändert | Bestanden |
| 58 | Tab-Tastaturbedienung mit Pfeiltasten und Home/End | Bestanden |
| 59 | History bleibt auf 55 Bearbeitungsschritte begrenzt | Bestanden |
| 60 | Ungültige Bilddateien und Dateitypen werden gezählt | Bestanden |
| 61 | Gleichzeitige Imports erzeugen keine doppelten Etiketten | Bestanden |
| 62 | Beschnitt beim Import beendet den Import erst nach Dialogschluss | Bestanden |
| 63 | Echtes zweiseitiges PDF wird mit deaktivierter Eval-Auswertung gerastert | Bestanden |
| 64 | Beschädigtes PDF blockiert folgende gültige Datei nicht | Bestanden |
| 65 | Neuladen erhält Vorlagen und hochgeladene Schriftarten | Bestanden |
| 66 | Mitgelieferte Boot-, Treiber- und PDF-Pfade sind vollständig | Bestanden |
| 67 | Keine unerwarteten DOM-Laufzeitfehler | Bestanden |
| 68 | Echter Schriftdatei-Upload speichert Font und aktualisiert Text | Bestanden |
| 69 | Ungültige Schriftdatei entsperrt den Editor | Bestanden |
| 70 | Schrift-Upload verändert gesperrten Text nicht | Bestanden |
| 71 | Leerer Zoom-Eintrag verändert die Skalierung nicht | Bestanden |
| 72 | Mehrere gleichzeitige Vorschauen führen zum letzten Zustand | Bestanden |
| 73 | Vorlagensuche filtert nach Ordner und Name | Bestanden |
| 74 | Export bleibt während gleichzeitiger Bearbeitung konsistent | Bestanden |
| 75 | Export enthält ein unabhängig wieder öffnbares PNG | Bestanden |
| 76 | Ungültige Text-Schriftreferenz wird beim Import abgelehnt | Bestanden |
| 77 | Ungültige Ebenenliste wird beim Import abgelehnt | Bestanden |
| 78 | Ungültige eingebettete Schrift wird vor Speicherung abgelehnt | Bestanden |
| 79 | Leeres Etikett nach 100 Einträgen wird begrenzt | Bestanden |
| 80 | Druck ohne Web-Bluetooth-Unterstützung bleibt ohne Ausgabe | Bestanden |
| 81 | Zwei Etiketten mit zwei Kopien erzeugen vier einzelne Ausgaben | Bestanden |
| 82 | Vorschau nach Warteschlange leeren entfernt alte Griffe | Bestanden |
| 83 | PDF-Zeichentabellen und Standardschriften sind mitgeliefert | Bestanden |
| 84 | Etikettenwechsel gibt dekodierte Bilder inaktiver Seiten frei | Bestanden |
| 85 | Bildzwischenspeicher bleibt bei großen Bildern unter zwölf Millionen Pixeln | Bestanden |
| 86 | Keine unbehandelten DOM-Fehler oder Vorschaufehler | Bestanden |

Die Rohdaten liegen in `pruefung/results.json` und `pruefung/edge-results.json`.
Zum Wiederholen siehe `pruefung/README.md`. Diese Zahlen zählen funktionale
Testfälle, nicht verschiedene reale Geräte oder Browser.
