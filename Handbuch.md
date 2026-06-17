# Handbuch für den Mailvorlagen-Generator

Dieses Handbuch erklärt die Bedienung der lokalen Browser-App Schritt für Schritt.

Die Anwendung ist für schulische E-Mails gedacht und läuft ohne Installation als einzelne HTML-Datei im Browser. Alle Daten bleiben lokal im Browser, bis sie bewusst exportiert werden.

## 1. Überblick

Die App besteht aus vier Bereichen:

- `E-Mail erstellen`
- `Vorlagen bearbeiten`
- `Einstellungen`
- `Import/Export`

Der typische Ablauf ist:

1. Vorlage auswählen oder anlegen
2. Felder in der Vorlage definieren
3. Einstellungen ergänzen
4. Im Bereich `E-Mail erstellen` die Felder ausfüllen
5. `E-Mail generieren` klicken
6. Den Text mit `Text kopieren` in die Zwischenablage übernehmen

## 2. Starten der Anwendung

Die App wird direkt über die Datei `mailvorlagen-generator.html` geöffnet.

So starten Sie die Anwendung:

1. Die Datei `mailvorlagen-generator.html` im Explorer doppelklicken.
2. Der Browser öffnet sich mit der Anwendung.
3. Eine vorhandene Vorlage auswählen oder direkt eine neue anlegen.

Es ist kein Server, kein Login und keine Installation nötig.

## 3. Bereich `E-Mail erstellen`

In diesem Bereich erzeugen Sie aus einer Vorlage den fertigen E-Mail-Text.

### 3.1 Vorlage auswählen

Oben sehen Sie das Dropdown `Vorlage auswählen`.

Wählen Sie dort die Vorlage aus, die Sie gerade verwenden möchten.

Nach der Auswahl erscheint darunter automatisch das passende Formular mit den Feldern der Vorlage.

### 3.2 Felder ausfüllen

Je nach Vorlage sehen Sie:

- Textfelder
- Auswahlfelder mit mehreren oder nur einer Auswahl
- Datumsfelder, falls sie manuell ausfüllbar sind

Felder, die automatisch aus den Einstellungen übernommen werden, erscheinen hier nicht.

### 3.3 E-Mail generieren

Wenn alle Angaben eingetragen sind:

1. Klicken Sie auf `E-Mail generieren`.
2. Der fertige Text erscheint im Ausgabebereich darunter.
3. Wenn keine Warnungen vorliegen, wird der Text automatisch in die Zwischenablage kopiert.

Falls Pflichtangaben fehlen oder ein Feld nicht sauber verwendet wurde, zeigt die App Hinweise an.

### 3.4 Text kopieren

Mit `Text kopieren` übernehmen Sie den erzeugten Text manuell in die Zwischenablage.

Wenn das automatische Kopieren im Browser nicht funktioniert, wird ein Hinweis angezeigt.

## 4. Bereich `Vorlagen bearbeiten`

In diesem Bereich erstellen und pflegen Sie Vorlagen.

### 4.1 Vorlagen auswählen

Oben wählen Sie die Vorlage aus, die Sie bearbeiten möchten.

Die zuletzt geänderten Vorlagen erscheinen in der Regel zuerst.

### 4.2 Neue Vorlage anlegen

Klicken Sie auf `Neue Vorlage`, wenn Sie mit einer leeren Vorlage beginnen möchten.

Danach können Sie einen Titel, einen Betreff, eine Beschreibung und den Vorlagentext anlegen.

### 4.3 Vorlagen duplizieren

Mit `Duplizieren` erstellen Sie eine Kopie der aktuell ausgewählten Vorlage.

Das ist praktisch, wenn Sie eine vorhandene Vorlage nur leicht abwandeln möchten.

### 4.4 Vorlage löschen

Mit `Löschen` entfernen Sie die aktuell ausgewählte Vorlage.

Die App fragt vor dem Löschen nach einer Bestätigung.

### 4.5 Vorlagenname, Betreff und Beschreibung

Die wichtigsten Felder sind:

- `Vorlagenname`
- `Betreff`
- `Beschreibung`

Der Vorlagenname erscheint in den Auswahlfeldern der App.
Der Betreff wird beim Erzeugen der E-Mail ebenfalls berücksichtigt, wenn er benutzt wird.
Die Beschreibung hilft beim schnellen Wiedererkennen der Vorlage.

### 4.6 Vorlagentext schreiben

Der große Textbereich ist der eigentliche Vorlagentext.

Hier schreiben Sie den Text, aus dem später die E-Mail erzeugt wird.

Platzhalter werden nicht von Hand geschrieben, sondern über die Bausteine eingefügt.

Beispiel:

```text
Sehr geehrte Eltern von
```

Danach können Sie über `Schüler(in)name` den passenden Platzhalter einfügen.

### 4.7 Bausteine einfügen

Unter `Bausteine` können Sie Platzhalter direkt in den Vorlagentext einfügen.

Verfügbar sind:

- `Schüler(in)name`
- `Eigene Auswahl-Texte`
- `Schulname`
- `Lehrername`
- `Signatur`

Die Bausteine werden an der Cursorposition im Text eingefügt.

## 5. Platzhalter und Felder

Ein eingefügter Baustein wird intern als Platzhalter gespeichert.

Sie müssen die Platzhalter nicht von Hand schreiben.

Beispiele:

- `Schüler(in)name` wird später als Name ausgefüllt
- `Eigene Auswahl-Texte` werden als Checkboxen oder Einzelauswahl dargestellt
- `Lehrername`, `Schulname` und `Signatur` kommen aus den Einstellungen

### 5.1 Textfeld einfügen

Mit dem Dialog `Textfeld einfügen` legen Sie ein freies Eingabefeld an.

Typische Angaben:

- Bezeichnung
- Zeilen
- Pflichtfeld

Das Feld erscheint danach sowohl im Editor als auch im Bereich `E-Mail erstellen`.

### 5.2 Auswahl-Texte einfügen

Mit `Auswahl-Texte einfügen` legen Sie ein Auswahlfeld an.

Hier geben Sie die einzelnen Auswahltexte ein, einen pro Block.

Sie können festlegen:

- Bezeichnung
- Darstellung als `Liste` oder `Fließtext`
- `Nur eine Option` oder `Mehrere Optionen`
- Nicht gewählte Optionen ausblenden
- Pflichtfeld

Wenn nur eine Auswahl erlaubt ist, zeigt die App im Formular Radiobuttons an.
Wenn mehrere Auswahlen erlaubt sind, zeigt die App Checkboxen an.

### 5.3 Datum einfügen

Mit `Datum einfügen` legen Sie ein Datumsfeld an.

Je nach Einstellung kann das Datum:

- als heutiges Datum automatisch eingesetzt werden
- manuell im Formular ausgefüllt werden
- als bestimmtes Datum in der Vorlage festgelegt sein

### 5.4 Schulname, Lehrername und Signatur

Diese Bausteine kommen aus den `Einstellungen`.

Sie müssen diese Werte daher nicht jedes Mal in der Vorlage neu schreiben.

## 6. Feldliste im Editor

Unter dem Vorlagentext sehen Sie die Feldliste der aktuellen Vorlage.

Dort können Sie:

- einzelne Felder erneut bearbeiten
- die Reihenfolge der ausfüllbaren Felder mit den Pfeilbuttons verändern
- Felder entfernen

Die Reihenfolge in dieser Liste bestimmt auch die Reihenfolge der Eingabefelder im Bereich `E-Mail erstellen`.
Felder aus den Einstellungen, zum Beispiel `Schulname`, `Lehrername` und `Signatur`, bleiben unten in der Liste, weil sie im Formular nicht ausgefüllt werden müssen.

Wenn Sie `Entfernen` klicken, fragt die App nach einer Bestätigung.

Wichtig:

- Wenn Sie bestätigen, wird das Feld gelöscht und der zugehörige Platzhalter aus dem Text entfernt.
- Wenn Sie abbrechen, bleibt alles unverändert.

## 7. Vorschau

Mit `Vorschau` sehen Sie eine Testausgabe der aktuellen Vorlage.

Die Vorschau ist hilfreich, um zu prüfen, ob:

- die Platzhalter korrekt gesetzt sind
- die Auswahlfelder sinnvoll aussehen
- die Einstellungen richtig übernommen werden

Die Vorschau verwendet Beispieldaten und verändert keine gespeicherten Inhalte.

## 8. Bereich `Einstellungen`

Hier tragen Sie die allgemeinen Werte ein, die in mehreren Vorlagen verwendet werden.

Verfügbar sind:

- `Name der Lehrkraft`
- `E-Mail-Adresse`
- `Name der Schule`
- `Signatur`
- `Datumsformat`

### 8.1 Schulname

Der `Name der Schule` wird in Vorlagen über den Baustein `Schulname` verwendet.

Wenn in der Vorlage `{{schulname}}` eingefügt wurde, erscheint dort später der gespeicherte Schulname.

### 8.2 Signatur

Die `Signatur` wird in Vorlagen über den Baustein `Signatur` eingefügt.

Sie können hier zum Beispiel den Namen, die Funktion und weitere Kontaktdaten eintragen.

### 8.3 Datumsformat

Sie können zwischen folgenden Formaten wählen:

- `dd.mm.yyyy`
- `yyyy-mm-dd`

Das wirkt sich auf Datumsfelder und automatisch erzeugte Datumsangaben aus.

### 8.4 Einstellungen speichern

Klicken Sie auf `Einstellungen speichern`, damit die Werte übernommen werden.

## 9. Bereich `Import/Export`

Hier sichern Sie Daten oder spielen Sicherungen wieder ein.

### 9.1 Alle Daten exportieren

Mit `Alle Daten exportieren (Backup)` speichern Sie alle Vorlagen und Einstellungen in einer JSON-Datei.

Diese Datei eignet sich als vollständige Sicherung.

### 9.2 Vorlage exportieren

Mit `Vorlage exportieren` speichern Sie nur die aktuell ausgewählte Vorlage als einzelne JSON-Datei.

Das ist praktisch, wenn Sie eine Vorlage zwischen Browsern oder Geräten austauschen möchten.

### 9.3 Daten importieren

Mit `Daten wiederherstellen oder Vorlage importieren` wählen Sie eine JSON-Datei aus.

Die App erkennt:

- ein vollständiges Backup
- eine einzelne Vorlage

Beim Import werden Sie gefragt, ob bestehende Daten ersetzt oder importierte Vorlagen hinzugefügt werden sollen.

Wenn es Namenskonflikte gibt, wird nicht stillschweigend überschrieben.

### 9.4 Alle Daten löschen

Mit `Alle Daten löschen` entfernen Sie alle lokal gespeicherten Vorlagen und Einstellungen.

Die App fragt vor dem Löschen nach einer Bestätigung.

## 10. Empfohlener Arbeitsablauf

Für den Alltag hat sich dieser Ablauf bewährt:

1. Vorlage in `Vorlagen bearbeiten` auswählen.
2. Falls nötig Vorlagentext anpassen.
3. In `Einstellungen` Lehrkraftdaten, Schulnamen und Signatur pflegen.
4. In `E-Mail erstellen` die Felder ausfüllen.
5. `E-Mail generieren` klicken.
6. Text prüfen.
7. Mit `Text kopieren` in die Zwischenablage übernehmen.

## 11. Beispiel für eine neue Vorlage

Ein typischer Startpunkt ist eine Vorlage mit:

- Titel
- Betreff
- kurzer Beschreibung
- Vorlagentext mit Bausteinen

So gehen Sie vor:

1. `Vorlagen bearbeiten` öffnen.
2. `Neue Vorlage` anklicken.
3. Titel, Betreff und Beschreibung eintragen.
4. Im Vorlagentext den ersten Satz schreiben.
5. Unter `Bausteine` den passenden Platzhalter einfügen.
6. Den restlichen Text ergänzen.
7. Mit `Speichern` sichern.

## 12. Hinweise zur sicheren Nutzung

- Generierte Texte immer vor dem Versand lesen.
- Vorlagen sind Formulierungshilfen, keine rechtliche Beratung.
- Exportdateien können personenbezogene Inhalte enthalten.
- Keine Daten werden automatisch an externe Server gesendet.

## 13. Fehler und Lösungen

### 13.1 Vorlage erscheint doppelt

Wenn nach einem Import doppelte Vorlagen auftauchen, prüfen Sie die Importdatei und wiederholen Sie den Import nur mit der gewünschten Sicherung.

### 13.2 Platzhalter kann nicht entfernt werden

Laden Sie die Seite neu und versuchen Sie es erneut.

Wenn die Vorlage aus einer älteren Sicherung stammt, kann ein veralteter Zustand im Browser gespeichert sein.

### 13.3 Text wird nicht automatisch kopiert

In manchen Browsern ist die Zwischenablage eingeschränkt.

In diesem Fall zeigt die App einen Hinweis an und Sie können den Text manuell kopieren.

## 14. Technischer Rahmen

Die App ist bewusst einfach gehalten:

- eine einzelne HTML-Datei
- keine Cloud
- keine Installation
- lokale Speicherung im Browser

Das macht die Anwendung auch auf Dienstrechnern gut portierbar und wartbar.
