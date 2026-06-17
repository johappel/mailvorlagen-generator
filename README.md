# Mailvorlagen-Generator

Eine kleine lokale Web-App für schulische Serien-E-Mails.

Die Anwendung läuft als einzelne HTML-Datei im Browser und ist für Windows-Schul-PCs ohne Installation gedacht. Vorlagen, Einstellungen und Exporte bleiben lokal im Browser, bis sie bewusst exportiert werden.

## Funktionen

- Vorlagen für E-Mail-Texte anlegen, bearbeiten, duplizieren und löschen
- Felder per Dialog in Vorlagen einfügen
- Dynamische Formulare aus Vorlagen erzeugen
- E-Mail-Texte ausfüllen, generieren und kopieren
- Vorschau mit Beispieldaten
- Lokale Einstellungen für Lehrername, Schulname, E-Mail, Signatur und Datumsformat
- Export und Import der kompletten Daten als JSON
- Einzelne Vorlagen als JSON teilen

## Dateien

- `mailvorlagen-generator.html` - die eigentliche Anwendung
- `index.html` - Einstieg für GitHub Pages
- `README.md` - diese Dokumentation

## Direkt starten

1. `mailvorlagen-generator.html` im Datei-Explorer doppelklicken.
2. Die App öffnet sich im Browser.
3. Eine vorhandene Vorlage auswählen oder direkt eine neue anlegen.

Es ist kein Build-Schritt, kein Server und keine Installation nötig.

## Quickstart

Für später gehört hier noch eine ausführlichere Anleitung zur Inbetriebnahme hinein. Zum schnellen Testen reicht dieser Ablauf:

1. `Vorlagen bearbeiten` öffnen und `Neue Vorlage` anklicken.
2. Als Vorlagenname `Unerlaubt Unterricht verlassen` eintragen, als Betreff `Verweis für unerlaubtes Verlassen des Unterrichts` und als Beschreibung `Benachrichtigung der Eltern, dass ein Schüler unerlaubt den Unterricht verlassen hat`.
3. Im Vorlagentext mit `Sehr geehrte Eltern von ` beginnen und dann unter `Bausteine` auf `Schüler(in)name` klicken. Dadurch wird im Text ein Platzhalter eingefügt, der später unter `E-Mail erstellen` automatisch ersetzt wird. Danach den Vorlagentext fertig schreiben und die Vorlage speichern.
4. Auf `E-Mail erstellen` wechseln, die Felder ausfüllen und `E-Mail generieren` anklicken. Der generierte Text wird danach automatisch in die Zwischenablage kopiert und kann direkt an anderer Stelle eingefügt werden.

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

Über den Bereich `Import/Export` können alle Vorlagen und Einstellungen gesichert werden.

- `Daten exportieren` erzeugt eine JSON-Datei mit allen Vorlagen und Einstellungen
- `Vorlage exportieren` speichert nur die aktuell ausgewählte Vorlage
- `Daten importieren` stellt Sicherungen wieder her oder fügt Vorlagen hinzu
- Beim Import können bestehende Daten ersetzt oder importierte Vorlagen hinzugefügt werden

Sicherheits- und Reputationshinweis: Exportdateien können personenbezogene oder sensible schulische Formulierungen enthalten. Vor einer Weitergabe sollte geprüft werden, ob das wirklich erforderlich und zulässig ist.

## GitHub Pages

Die App kann statisch über GitHub Pages veröffentlicht werden.

1. Änderungen auf den Branch `gh-pages` committen.
2. Den Branch mit `git push origin gh-pages` nach GitHub pushen.
3. In den Repository-Einstellungen unter `Pages` den Branch `gh-pages` als Quelle auswählen.

Für GitHub Pages liegt mit `index.html` bereits ein Einstieg im Repository, der auf `mailvorlagen-generator.html` weiterleitet.

## Technische Hinweise

- Vanilla HTML, CSS und JavaScript
- Keine Frameworks
- Keine Build-Tools
- Keine externen Bibliotheken
- Single-File-App mit lokaler Speicherung im Browser

## Lokale Entwicklung

Für Änderungen genügt es, `mailvorlagen-generator.html` in einem Editor zu bearbeiten und die Datei im Browser neu zu laden.

## Status

Das Projekt ist bewusst als einzelne, portable Browser-App aufgebaut. Der Schwerpunkt liegt auf einfacher Bedienung und lokaler Nutzung ohne Cloud-Abhängigkeit.
