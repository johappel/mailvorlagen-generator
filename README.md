# Mailvorlagen-Generator

Eine kleine lokale Web-App für schulische Serien-E-Mails.

Die Anwendung läuft als einzelne HTML-Datei im Browser und ist für Windows-Schul-PCs ohne Installation gedacht. Vorlagen, Einstellungen und Exporte bleiben lokal im Browser, bis sie bewusst exportiert werden.

## Funktionen

- Vorlagen für E-Mail-Texte anlegen, bearbeiten, duplizieren und löschen
- Felder per Dialog in Vorlagen einfügen
- Dynamische Formulare aus Vorlagen erzeugen
- E-Mail-Texte ausfüllen, generieren und kopieren
- Vorschau mit Beispieldaten
- Lokale Einstellungen für Lehrername, E-Mail, Signatur und Datumsformat
- Export und Import der kompletten Daten als JSON
- Beispielvorlage für Fehlzeiten direkt beim ersten Start

## Dateien

- `mailvorlagen-generator.html` - die eigentliche Anwendung
- `README.md` - diese Dokumentation

## Direkt starten

1. `mailvorlagen-generator.html` im Datei-Explorer doppelklicken.
2. Die App öffnet sich im Browser.
3. Beispielvorlage auswählen und direkt loslegen.

Es ist kein Build-Schritt, kein Server und keine Installation nötig.

## Datenschutz

Die Anwendung arbeitet lokal im Browser.

- Keine automatische Übertragung an externe Server
- Keine externen Fonts, Tracker oder CDN-Abhängigkeiten
- Keine automatische E-Mail-Versendung
- Generierte Texte werden nur angezeigt und können kopiert werden

Hinweis: Die erzeugten Texte sind Formulierungshilfen. Bitte Inhalt, Ton und schulrechtliche Angemessenheit vor dem Versand prüfen.

## Speicherung

Die App speichert Daten lokal im Browser über `localStorage`.

- Vorlagen werden im Browser dieses Geräts gespeichert
- Einstellungen werden im Browser dieses Geräts gespeichert
- Ein Export ist sinnvoll, wenn Daten gesichert oder auf einen anderen Rechner übertragen werden sollen

## Export und Import

Über den Bereich **Import/Export** können alle Vorlagen und Einstellungen gesichert werden.

- **Daten exportieren** erzeugt eine JSON-Datei mit allen Vorlagen und Einstellungen
- **Daten importieren** stellt diese Daten wieder her
- Bei einem Import können bestehende Daten ersetzt oder importierte Vorlagen hinzugefügt werden

## GitHub Pages veröffentlichen

Die App ist für eine statische Veröffentlichung geeignet. Wenn du sie auf GitHub Pages bereitstellen willst, ist der einfachste Weg:

1. Das Repository nach GitHub pushen.
2. In den Repository-Einstellungen unter **Pages** als Quelle den Branch `gh-pages` wählen.
3. Die Datei `mailvorlagen-generator.html` im Root des Branches ablegen.
4. Optional eine `index.html` im Root anlegen, die auf die App-Datei verweist oder die App direkt als Startseite verwendet.

Wenn du die App direkt als Startseite veröffentlichen willst, ist es praktisch, die Datei im `gh-pages`-Branch zusätzlich als `index.html` bereitzustellen.

## Technische Hinweise

- Vanilla HTML, CSS und JavaScript
- Keine Frameworks
- Keine Build-Tools
- Keine externen Bibliotheken

## Lokale Entwicklung

Für Änderungen genügt es, `mailvorlagen-generator.html` in einem Editor zu bearbeiten und die Datei im Browser neu zu laden.

## Status

Das Projekt ist bewusst als einzelne, portable Browser-App aufgebaut. Der Schwerpunkt liegt auf einfacher Bedienung und lokaler Nutzung ohne Cloud-Abhängigkeit.
