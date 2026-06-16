# AGENTS.md

## Projektname

**Mailvorlagen-Generator für schulische Serien-E-Mails**

## Ziel des Projekts

Dieses Projekt ist eine kleine, lokal nutzbare Web-App zur Vorbereitung standardisierter schulischer E-Mail-Texte. Lehrkräfte sollen ohne Programmierkenntnisse E-Mail-Vorlagen erstellen, speichern, ausfüllen und daraus fertige E-Mail-Texte generieren können.

Die App soll insbesondere für Windows-Schul-PCs geeignet sein und ohne Installation funktionieren.

Primäres Ziel:

* Eine einzelne lokale HTML-Datei oder eine sehr kleine statische Web-App.
* Keine Serverpflicht.
* Keine Cloud-Abhängigkeit.
* Keine automatische Versendung von E-Mails.
* Keine Verarbeitung personenbezogener Daten außerhalb des lokalen Browsers.
* Kolleg:innen sollen keine Template-Syntax lernen müssen.
* Formularfelder sollen über Buttons und Dialoge in Vorlagen eingefügt werden.

## Zielgruppe

Die Zielgruppe sind schulische Kolleg:innen ohne technische Vorkenntnisse.

Das UI muss daher extrem einfach, verständlich und fehlertolerant sein. Begriffe wie JSON, localStorage, Placeholder, Pattern oder Template-Syntax dürfen im normalen Benutzungsmodus nicht vorkommen.

## Grundidee

Die Lehrkraft erstellt oder wählt eine E-Mail-Vorlage aus. In der Vorlage können variable Felder eingefügt werden, z. B.:

* Name der Schülerin / des Schülers
* Freitextfeld
* Auswahloptionen zum Ankreuzen
* aktuelles Datum
* Name der Lehrkraft
* E-Mail-Adresse der Lehrkraft
* Signatur

Diese Felder werden im Template-Editor über Buttons erzeugt. Intern werden sie als Platzhalter gespeichert, aber die Nutzer:innen müssen diese Syntax nicht selbst schreiben.

Beispiel für sichtbaren Text im Editor:

```text
Sehr geehrte Eltern von [Name],

ich möchte Sie hiermit darauf hinweisen, dass Ihr Kind in den vergangenen Monaten eine ungewöhnlich hohe Anzahl von Fehlzeiten zu verzeichnen hat.

Dies äußert sich durch:
[Fehlzeiten]

[Signatur]
```

Intern darf daraus z. B. werden:

```text
Sehr geehrte Eltern von {{field_a1b2c3}},

ich möchte Sie hiermit darauf hinweisen, dass Ihr Kind in den vergangenen Monaten eine ungewöhnlich hohe Anzahl von Fehlzeiten zu verzeichnen hat.

Dies äußert sich durch:
{{field_d4e5f6}}

{{field_signature}}
```

Die Felddefinitionen werden getrennt vom Vorlagentext gespeichert.

## Technische Leitentscheidung

### Version 1 soll bevorzugt als einzelne HTML-Datei funktionieren

Zielartefakt:

```text
mailvorlagen-generator.html
```

Diese Datei soll per Doppelklick im Browser geöffnet werden können.

Erlaubt:

* HTML
* CSS
* JavaScript
* localStorage
* Blob-Download für Export
* FileReader für Import

Nicht verwenden in Version 1:

* Build-System
* Node.js-Pflicht
* npm-Abhängigkeiten
* Backend
* Server
* Login
* Cloudspeicher
* externe CDN-Bibliotheken
* automatische Mailversendung über SMTP/API

Optional darf die App später in mehrere Dateien aufgeteilt werden, aber die erste lauffähige Version soll möglichst als Single-File-App funktionieren.

## Datenschutzprinzipien

Die App verarbeitet potentiell personenbezogene Daten, z. B. Namen von Schüler:innen. Deshalb gelten folgende Regeln:

1. Keine Daten dürfen automatisch an externe Server gesendet werden.
2. Keine externen Analyse-Tools.
3. Keine externen Fonts, Tracker oder CDN-Abhängigkeiten.
4. Kein automatischer E-Mail-Versand.
5. Der generierte Text wird nur angezeigt und kann kopiert werden.
6. Optional darf ein `mailto:`-Link angeboten werden, aber nicht als primärer Workflow.
7. Die Lehrkraft muss den generierten Text vor dem Versand selbst prüfen.
8. Exportdateien liegen in der Verantwortung der Nutzer:innen.
9. Keine Schülerdaten in Beispiel- oder Demo-Templates verwenden.

## UX-Leitlinien

Die App muss für unbedarfte Nutzer:innen verständlich sein.

### Vermeide technische Begriffe

Nicht im UI verwenden:

* Placeholder
* Pattern
* JSON
* localStorage
* IndexedDB
* Field-ID
* Regex
* Template-Syntax

Stattdessen verwenden:

* Vorlage
* Feld
* Textfeld
* Auswahl
* Baustein
* Einstellungen
* Vorschau
* Exportieren
* Importieren

### Normaler Benutzungsmodus

Der normale Modus soll nur Folgendes zeigen:

1. Vorlage auswählen
2. Formular ausfüllen
3. E-Mail-Text generieren
4. Text kopieren

Beispiel:

```text
Vorlage:
[Viele Fehltage wegen Krankheit ▼]

Name der Schülerin / des Schülers:
[________________________]

Auffälligkeiten:
☐ gehäufte Krankheitstage
☐ wiederholtes Unterbrechen des Unterrichts am Vormittag aufgrund von Erkrankungen
☐ gehäuftes Fehlen an Prüfungstagen

[ E-Mail generieren ]

Generierter Text:
...
[ Text kopieren ]
```

### Bearbeitungsmodus

Der Bearbeitungsmodus darf komplexer sein, muss aber geführt sein.

Er soll enthalten:

* Vorlagenname
* Vorlagentext-Editor
* Button: Textfeld einfügen
* Button: Optionen einfügen
* Button: Datum einfügen
* Button: Lehrername einfügen
* Button: E-Mail einfügen
* Button: Signatur einfügen
* Button: Vorschau
* Button: Speichern
* Button: Vorlage duplizieren
* Button: Vorlage löschen

## Muss-Funktionen

### 1. Vorlagenverwaltung

Die App muss mehrere Vorlagen speichern können.

Jede Vorlage hat:

* eindeutige ID
* Titel
* Body/Text
* Felddefinitionen
* optional Betreff
* optional Beschreibung
* Erstellungsdatum
* Änderungsdatum

Minimaler Datentyp:

```js
{
  id: "template_abc123",
  title: "Viele Fehltage wegen Krankheit",
  subject: "Hinweis zu Fehlzeiten",
  body: "Sehr geehrte Eltern von {{field_name}},\n\n...",
  fields: {
    field_name: {
      id: "field_name",
      type: "text",
      label: "Name",
      rows: 1,
      required: true
    }
  },
  createdAt: "2026-06-16T10:00:00.000Z",
  updatedAt: "2026-06-16T10:00:00.000Z"
}
```

### 2. Einstellungen

Die App muss lokale Einstellungen speichern können.

Mindestens:

```js
{
  teacherName: "",
  teacherEmail: "",
  signature: "",
  dateFormat: "dd.mm.yyyy"
}
```

Optional später:

```js
{
  schoolName: "",
  defaultGreeting: "",
  defaultSubjectPrefix: ""
}
```

### 3. Template-Editor mit Buttons

Nutzer:innen sollen Formularfelder nicht manuell als Syntax schreiben müssen.

#### Button: Textfeld einfügen

Öffnet Dialog mit:

* Bezeichnung
* Anzahl Zeilen
* Pflichtfeld ja/nein

Default:

* Bezeichnung: `Name`
* Zeilen: `1`
* Pflichtfeld: ja

Erzeugt Felddefinition:

```js
{
  id: "field_xxxxx",
  type: "text",
  label: "Name",
  rows: 1,
  required: true
}
```

Fügt an Cursorposition ein:

```text
{{field_xxxxx}}
```

Im Editor soll nach Möglichkeit sichtbar sein:

```text
[Name]
```

Wenn Chips noch nicht implementiert sind, darf in Version 1 die technische Markierung sichtbar sein, aber sie sollte möglichst nutzerfreundlich dargestellt werden.

#### Button: Optionen einfügen

Öffnet Dialog mit:

* Bezeichnung

* Textarea für Optionen, eine Option pro Zeile

* Darstellung:
  
  * Liste
  * Fließtext

* Nicht gewählte Optionen:
  
  * ausblenden
  * als nicht ausgewählt anzeigen

* Optional: Bullet-Zeichen oder Checkbox-Zeichen

Default:

* Bezeichnung: `Auswahl`
* Darstellung: `Liste`
* Nicht gewählte Optionen: `ausblenden`

Beispieloptionen:

```text
gehäufte Krankheitstage
wiederholtes Unterbrechen des Unterrichts am Vormittag aufgrund von Erkrankungen
gehäuftes Fehlen an Prüfungstagen
```

Erzeugt:

```js
{
  id: "field_xxxxx",
  type: "options",
  label: "Fehlzeiten",
  options: [
    "gehäufte Krankheitstage",
    "wiederholtes Unterbrechen des Unterrichts am Vormittag aufgrund von Erkrankungen",
    "gehäuftes Fehlen an Prüfungstagen"
  ],
  display: "list",
  hideUnchecked: true
}
```

#### Button: Datum einfügen

Fügt ein Datumsfeld ein.

Dialog optional:

* Bezeichnung

* Datumstyp:
  
  * heutiges Datum
  * ausfüllbares Datum

Version 1 genügt:

```js
{
  id: "field_date",
  type: "setting",
  settingKey: "currentDate",
  label: "Datum"
}
```

Das Datum wird nach `settings.dateFormat` formatiert.

Defaultformat:

```text
dd.mm.yyyy
```

Beispiel:

```text
16.06.2026
```

#### Button: Lehrername einfügen

Fügt Feld ein, das aus den Einstellungen kommt.

```js
{
  id: "field_teacher_name",
  type: "setting",
  settingKey: "teacherName",
  label: "Lehrername"
}
```

#### Button: E-Mail einfügen

Fügt Feld ein, das aus den Einstellungen kommt.

```js
{
  id: "field_teacher_email",
  type: "setting",
  settingKey: "teacherEmail",
  label: "E-Mail"
}
```

#### Button: Signatur einfügen

Fügt Feld ein, das aus den Einstellungen kommt.

```js
{
  id: "field_signature",
  type: "setting",
  settingKey: "signature",
  label: "Signatur"
}
```

### 4. Feld erneut bearbeiten

Wenn Nutzer:innen im Template-Editor auf ein eingefügtes Feld klicken, soll sich der passende Dialog erneut öffnen.

Beispiele:

* Klick auf `[Name]` öffnet Textfeld-Dialog.
* Klick auf `[Fehlzeiten]` öffnet Optionen-Dialog.
* Klick auf `[Datum]` öffnet Datum-Dialog.

Wenn Chips in Version 1 zu aufwendig sind, darf eine einfachere Lösung gebaut werden:

* Liste der Felder unterhalb des Editors anzeigen.
* Neben jedem Feld: Button `Bearbeiten`.
* Feld im Text bleibt als `{{field_xxxxx}}` sichtbar.

Akzeptabel für Version 1, aber Ziel für Version 2 ist Chip-Bearbeitung direkt im Text.

### 5. Formular automatisch aus Vorlage erzeugen

Beim Auswählen einer Vorlage muss die App aus den Felddefinitionen automatisch ein Formular erzeugen.

Feldtypen:

#### Textfeld

`rows: 1`

```html
<input type="text">
```

`rows > 1`

```html
<textarea></textarea>
```

#### Optionen

Für jede Option eine Checkbox.

```html
<label>
  <input type="checkbox">
  gehäufte Krankheitstage
</label>
```

#### Setting-Felder

Diese erscheinen im Ausfüllformular normalerweise nicht, weil sie aus den Einstellungen stammen.

Beispiele:

* Lehrername
* E-Mail
* Signatur
* heutiges Datum

Optional kann ein Hinweis angezeigt werden:

```text
Signatur wird aus den Einstellungen eingefügt.
```

### 6. E-Mail-Text generieren

Beim Klick auf `E-Mail generieren` wird der Template-Body gerendert.

Regeln:

#### Textfelder

`{{field_xxxxx}}` wird durch den eingegebenen Wert ersetzt.

#### Optionen als Liste

Wenn `display: "list"` und `hideUnchecked: true`, dann werden nur gewählte Optionen ausgegeben:

```text
- gehäufte Krankheitstage
- gehäuftes Fehlen an Prüfungstagen
```

Wenn nichts gewählt ist:

* entweder leer lassen
* oder Hinweis anzeigen: `[keine Auswahl getroffen]`

In Version 1 besser: Im Formular eine Warnung anzeigen, wenn ein Optionsfeld als Pflichtfeld markiert ist und nichts gewählt wurde.

#### Optionen als Fließtext

Wenn `display: "inline"`:

Auswahl:

```text
gehäufte Krankheitstage, gehäuftes Fehlen an Prüfungstagen
```

Optional später grammatisch besser:

```text
gehäufte Krankheitstage und gehäuftes Fehlen an Prüfungstagen
```

#### Nicht gewählte Optionen anzeigen

Wenn `hideUnchecked: false`, dann Ausgabe z. B.:

```text
☑ gehäufte Krankheitstage
☐ wiederholtes Unterbrechen des Unterrichts am Vormittag aufgrund von Erkrankungen
☑ gehäuftes Fehlen an Prüfungstagen
```

#### Setting-Felder

* `teacherName`: aus settings.teacherName
* `teacherEmail`: aus settings.teacherEmail
* `signature`: aus settings.signature
* `currentDate`: heutiges Datum im eingestellten Format

### 7. Text kopieren

Nach dem Generieren muss es einen Button geben:

```text
Text kopieren
```

Dieser kopiert den generierten Text in die Zwischenablage.

Wenn Clipboard API nicht verfügbar ist, Fallback:

* Text automatisch markieren
* Hinweis anzeigen: `Bitte mit Strg+C kopieren.`

### 8. Vorschau im Template-Editor

Der Button `Vorschau` erzeugt eine Demo-Ausgabe.

Regeln:

* Textfelder bekommen Beispielwerte.
* Feld mit Label `Name` bekommt `Max Beispiel`.
* Mehrzeilige Textfelder bekommen `Dies ist ein Beispieltext.`
* Optionen werden alle als ausgewählt behandelt.
* Datum zeigt das aktuelle Datum.
* Lehrername/E-Mail/Signatur kommen aus den Einstellungen oder aus Demo-Werten, falls leer.

Die Vorschau darf keine Daten speichern.

### 9. Import und Export

Die App muss alle Vorlagen und Einstellungen exportieren können.

Button:

```text
Daten exportieren
```

Erzeugt JSON-Datei, z. B.:

```text
mailvorlagen-generator-backup.json
```

Die Datei enthält:

```js
{
  version: 1,
  exportedAt: "2026-06-16T10:00:00.000Z",
  settings: {...},
  templates: [...]
}
```

Button:

```text
Daten importieren
```

Importregeln:

* JSON validieren.

* Version prüfen.

* Nutzer:in fragen:
  
  * Bestehende Daten ersetzen
  * Importierte Vorlagen hinzufügen

* Bei ID-Konflikten neue IDs erzeugen.

* Fehlermeldung anzeigen, wenn Datei ungültig ist.

### 10. Beispielvorlage mitliefern

Die App soll beim ersten Start eine Beispielvorlage erzeugen:

Titel:

```text
Viele Fehltage wegen Krankheit
```

Betreff:

```text
Hinweis zu Fehlzeiten
```

Vorlagentext:

```text
Sehr geehrte Eltern von {{field_student_name}},

ich möchte Sie hiermit darauf hinweisen, dass Ihr Kind in den vergangenen Monaten eine ungewöhnlich hohe Anzahl von Fehlzeiten zu verzeichnen hat. Dies äußert sich durch:

{{field_absence_reasons}}

Ich möchte Sie darauf aufmerksam machen, dass häufige Fehlzeiten – unabhängig von der Ursache – sich nachteilig auf die Leistungsbewertung Ihres Kindes auswirken können.

Als Eltern tragen Sie die Verantwortung für die Einhaltung der Schulpflicht sowie dafür, dass versäumte Inhalte eigenständig nachgeholt werden. Ich muss Sie daher dringend bitten, die Situation mit Ihrem Kind zu besprechen und künftig verlässlich auf eine regelmäßige Teilnahme am Unterricht und an den Leistungsnachweisen zu achten.

Sollten den gehäuften Fehlzeiten medizinische Gründe oder gesundheitliche Einschränkungen zugrunde liegen, bitte ich Sie, mir diese Information zeitnah zukommen zu lassen. Dies hilft uns, die Situation Ihres Kindes richtig einzuordnen.

Bei Rückfragen kommen Sie gerne auf mich zu.

{{field_signature}}
```

Felddefinitionen:

```js
{
  field_student_name: {
    id: "field_student_name",
    type: "text",
    label: "Name der Schülerin / des Schülers",
    rows: 1,
    required: true
  },
  field_absence_reasons: {
    id: "field_absence_reasons",
    type: "options",
    label: "Auffälligkeiten",
    options: [
      "gehäufte Krankheitstage",
      "wiederholtes Unterbrechen des Unterrichts am Vormittag aufgrund von Erkrankungen",
      "gehäuftes Fehlen an Prüfungstagen"
    ],
    display: "list",
    hideUnchecked: true,
    required: false
  },
  field_signature: {
    id: "field_signature",
    type: "setting",
    settingKey: "signature",
    label: "Signatur"
  }
}
```

## Datenmodell

### AppState

```ts
type AppState = {
  version: number;
  settings: Settings;
  templates: Template[];
};
```

### Settings

```ts
type Settings = {
  teacherName: string;
  teacherEmail: string;
  signature: string;
  dateFormat: "dd.mm.yyyy" | "yyyy-mm-dd";
};
```

### Template

```ts
type Template = {
  id: string;
  title: string;
  subject?: string;
  description?: string;
  body: string;
  fields: Record<string, FieldDefinition>;
  createdAt: string;
  updatedAt: string;
};
```

### FieldDefinition

```ts
type FieldDefinition =
  | TextFieldDefinition
  | OptionsFieldDefinition
  | SettingFieldDefinition
  | DateFieldDefinition;
```

### TextFieldDefinition

```ts
type TextFieldDefinition = {
  id: string;
  type: "text";
  label: string;
  rows: number;
  required: boolean;
  placeholder?: string;
};
```

### OptionsFieldDefinition

```ts
type OptionsFieldDefinition = {
  id: string;
  type: "options";
  label: string;
  options: string[];
  display: "list" | "inline" | "checkboxes";
  hideUnchecked: boolean;
  required: boolean;
};
```

### SettingFieldDefinition

```ts
type SettingFieldDefinition = {
  id: string;
  type: "setting";
  label: string;
  settingKey: "teacherName" | "teacherEmail" | "signature";
};
```

### DateFieldDefinition

```ts
type DateFieldDefinition = {
  id: string;
  type: "date";
  label: string;
  mode: "today" | "manual";
  formatFromSettings: boolean;
};
```

## Speicherstrategie

### Version 1

Verwende `localStorage`.

Key:

```text
mailvorlagenGenerator.state.v1
```

Funktionen:

```js
loadState()
saveState(state)
resetState()
exportState()
importState(file)
```

### Wichtig

Immer defensiv laden:

* Wenn localStorage leer ist: Default-State erzeugen.
* Wenn JSON kaputt ist: Fehlermeldung anzeigen und Default-State anbieten.
* Niemals kaputte Daten stillschweigend überschreiben, ohne vorher Export/Backup anzubieten.

## Rendering-Regeln

### Platzhalter erkennen

Platzhalterformat intern:

```text
{{field_id}}
```

Regex:

```js
/\{\{(field_[a-zA-Z0-9_-]+)\}\}/g
```

### Feld-IDs

Neue IDs generieren:

```js
field_ + crypto.randomUUID()
```

Fallback, falls `crypto.randomUUID()` nicht verfügbar:

```js
field_ + Date.now() + "_" + Math.random().toString(36).slice(2)
```

### Rendering

Implementiere zentrale Funktion:

```js
renderTemplate(template, formValues, settings, mode)
```

`mode`:

* `real`
* `preview`

Rückgabe:

```js
{
  subject: string,
  body: string,
  warnings: string[]
}
```

## Validierung

Beim Speichern einer Vorlage prüfen:

1. Hat die Vorlage einen Titel?
2. Gibt es unbekannte Platzhalter im Body?
3. Gibt es Felddefinitionen, die nicht im Body verwendet werden?
4. Gibt es Body-Platzhalter ohne Felddefinition?
5. Haben Optionsfelder mindestens eine Option?
6. Haben Textfelder ein Label?
7. Sind Setting-Felder gültig?

Nicht hart blockieren, wenn ungefährlich. Lieber verständliche Warnungen anzeigen.

Beispiel:

```text
Das Feld „Fehlzeiten“ ist definiert, kommt aber im Vorlagentext nicht vor.
```

## UI-Struktur

Single-Page-App mit Tabs oder Bereichen:

### Tab 1: E-Mail erstellen

* Vorlagenauswahl
* dynamisches Formular
* Button `E-Mail generieren`
* Ausgabe
* Button `Text kopieren`
* optional Betreff anzeigen

### Tab 2: Vorlagen bearbeiten

* Vorlagenauswahl
* Button `Neue Vorlage`
* Button `Duplizieren`
* Button `Löschen`
* Feld `Vorlagenname`
* Feld `Betreff`
* Texteditor
* Toolbar mit Einfügebuttons
* Feldliste mit Bearbeiten/Löschen
* Button `Vorschau`
* Button `Speichern`

### Tab 3: Einstellungen

* Name der Lehrkraft
* E-Mail-Adresse
* Signatur
* Datumsformat
* Button `Speichern`

### Tab 4: Import/Export

* Exportieren
* Importieren
* Reset auf Beispielvorlagen
* Hinweis auf lokale Speicherung

## Dialoge

Implementiere einfache Modal-Dialoge oder native `<dialog>`-Elemente.

### Textfeld-Dialog

Felder:

* Bezeichnung
* Zeilen
* Pflichtfeld

Buttons:

* Einfügen / Speichern
* Abbrechen

### Optionen-Dialog

Felder:

* Bezeichnung
* Optionen, eine pro Zeile
* Darstellung
* Nicht gewählte Optionen ausblenden
* Pflichtfeld

Buttons:

* Einfügen / Speichern
* Abbrechen

### Datum-Dialog

Felder:

* Bezeichnung
* heutiges Datum oder manuelles Datum

Buttons:

* Einfügen / Speichern
* Abbrechen

## Beispielhafte UI-Texte

### Datenschutz-Hinweis

```text
Diese Anwendung läuft lokal in Ihrem Browser. Die eingegebenen Daten werden nicht automatisch versendet und nicht an externe Server übertragen. Prüfen Sie den generierten Text vor dem Versand über Ihr dienstliches E-Mail-Programm.
```

### Export-Hinweis

```text
Die gespeicherten Vorlagen liegen nur in diesem Browser auf diesem Gerät. Nutzen Sie den Export, um Ihre Vorlagen zu sichern oder auf einen anderen Rechner zu übertragen.
```

### Kopier-Hinweis

```text
Der Text wurde in die Zwischenablage kopiert.
```

## Styling

Die Oberfläche soll ruhig, sachlich und schulgeeignet wirken.

CSS-Anforderungen:

* responsive Grundgestaltung
* auf 1024px Breite gut nutzbar
* große klickbare Buttons
* klare Labels
* gute Kontraste
* keine verspielte Gestaltung
* keine externen Fonts
* Systemschrift verwenden

Empfohlene Schrift:

```css
font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

## Barrierearmut

Mindestanforderungen:

* Labels korrekt mit Inputs verknüpfen
* Buttons als echte `<button>`-Elemente
* ausreichender Kontrast
* Tastaturbedienung möglich
* Fokus sichtbar
* Dialoge mit Escape schließbar
* keine rein farbliche Bedeutungsanzeige

## Sicherheit

* Generierte Texte immer als Text behandeln, nicht als HTML.
* Keine unsichere HTML-Injektion über `innerHTML`, außer bei vorheriger eigener Escaping-Funktion.
* Für Nutzereingaben bevorzugt `textContent`, `value`.
* Importierte JSON-Dateien validieren.
* Keine eval-Verwendung.
* Keine externe Skriptausführung.

## Qualitätssicherung

### Manuelle Akzeptanztests

#### Test 1: Erststart

1. HTML-Datei im Browser öffnen.
2. Beispielvorlage ist vorhanden.
3. Einstellungen sind leer oder mit neutralen Demo-Werten gefüllt.
4. Datenschutz-Hinweis ist sichtbar.

Erwartung:

* App ist ohne Setup nutzbar.

#### Test 2: E-Mail generieren

1. Vorlage `Viele Fehltage wegen Krankheit` auswählen.
2. Namen eintragen.
3. Zwei Auffälligkeiten auswählen.
4. E-Mail generieren.

Erwartung:

* Name erscheint korrekt.
* Nur gewählte Auffälligkeiten erscheinen.
* Nicht gewählte Auffälligkeit wird ausgeblendet.
* Text ist kopierbar.

#### Test 3: Signatur

1. In Einstellungen Signatur speichern.
2. E-Mail neu generieren.

Erwartung:

* Signatur erscheint am Ende.

#### Test 4: Neue Vorlage

1. Neue Vorlage erstellen.
2. Textfeld einfügen.
3. Optionen einfügen.
4. Vorlage speichern.
5. In Benutzungsmodus wechseln.

Erwartung:

* Formular wird automatisch erzeugt.

#### Test 5: Vorschau

1. Vorlage im Editor öffnen.
2. Vorschau klicken.

Erwartung:

* Demo-Ausgabe wird erzeugt.
* Alle Optionen sind ausgewählt.
* Keine Daten werden dauerhaft verändert.

#### Test 6: Export/Import

1. Vorlagen exportieren.
2. App-Daten zurücksetzen.
3. Exportdatei importieren.

Erwartung:

* Vorlagen und Einstellungen sind wieder vorhanden.

#### Test 7: Ungültige Importdatei

1. Ungültige JSON-Datei importieren.

Erwartung:

* Verständliche Fehlermeldung.
* Bestehende Daten bleiben erhalten.

#### Test 8: Fehlende Felddefinition

1. Template-Body enthält unbekannten Platzhalter.
2. Speichern oder Vorschau ausführen.

Erwartung:

* Warnung wird angezeigt.
* App stürzt nicht ab.

## Umsetzungstasks für Codex

### Task 1: Projektgrundlage erstellen

Erstelle eine Single-File-App:

```text
mailvorlagen-generator.html
```

Die Datei enthält:

* HTML-Struktur
* CSS
* JavaScript
* Default-State
* localStorage-Speicherung

Akzeptanz:

* Datei lässt sich per Doppelklick im Browser öffnen.
* Beispielvorlage wird angezeigt.

### Task 2: App-State implementieren

Implementiere:

* `getDefaultState()`
* `loadState()`
* `saveState(state)`
* `validateState(raw)`
* `createId(prefix)`

Akzeptanz:

* Zustand wird nach Reload erhalten.
* Kaputte Daten führen nicht zum Absturz.

### Task 3: Tabs/Navigation implementieren

Erstelle Tabs:

* E-Mail erstellen
* Vorlagen bearbeiten
* Einstellungen
* Import/Export

Akzeptanz:

* Wechsel ohne Seitenreload.
* Aktiver Tab sichtbar.

### Task 4: Beispielvorlage implementieren

Implementiere die Beispielvorlage `Viele Fehltage wegen Krankheit`.

Akzeptanz:

* Formular mit Name und Auffälligkeiten wird automatisch erzeugt.
* Signaturfeld wird aus Einstellungen eingefügt.

### Task 5: Formularrenderer implementieren

Implementiere:

* `renderForm(template)`
* Textfelder
* Textareas
* Checkboxgruppen
* Pflichtfeldprüfung

Akzeptanz:

* Formular entsteht aus `template.fields`.
* Setting-Felder erscheinen nicht als ausfüllbare Felder.

### Task 6: Template-Renderer implementieren

Implementiere:

* `renderTemplate(template, formValues, settings, mode)`
* Ersetzung von Textfeldern
* Ersetzung von Optionsfeldern
* Ersetzung von Setting-Feldern
* Datumformatierung

Akzeptanz:

* Generierter Text ist korrekt.
* Nicht gewählte Optionen werden bei `hideUnchecked: true` nicht ausgegeben.

### Task 7: Text kopieren

Implementiere Clipboard-Button mit Fallback.

Akzeptanz:

* Text kann kopiert werden.
* Bei fehlender Clipboard API erscheint verständlicher Hinweis.

### Task 8: Einstellungen implementieren

Implementiere Formular für:

* Lehrername
* E-Mail
* Signatur
* Datumsformat

Akzeptanz:

* Einstellungen werden gespeichert.
* Signatur erscheint in generierten Texten.

### Task 9: Template-Editor implementieren

Implementiere:

* Vorlagenauswahl
* neue Vorlage
* duplizieren
* löschen
* Titel
* Betreff
* Body-Editor
* Speichern

Akzeptanz:

* Vorlagen können erstellt, geändert und gelöscht werden.
* Änderungen sind nach Reload erhalten.

### Task 10: Feld einfügen

Implementiere Toolbar-Buttons:

* Textfeld einfügen
* Optionen einfügen
* Datum einfügen
* Lehrername einfügen
* E-Mail einfügen
* Signatur einfügen

Akzeptanz:

* Feld wird an Cursorposition eingefügt.
* Felddefinition wird in der Vorlage gespeichert.
* Feld erscheint im Benutzungsformular.

### Task 11: Feld bearbeiten

Implementiere zunächst einfache Feldliste unter dem Editor.

Für jedes Feld:

* Label
* Typ
* Bearbeiten
* Entfernen

Akzeptanz:

* Felddefinitionen können geändert werden.
* Änderungen wirken sich auf Formular und Rendering aus.
* Entfernen löscht die Felddefinition und optional den Platzhalter im Body.

### Task 12: Vorschau implementieren

Implementiere Demo-Rendering.

Akzeptanz:

* Vorschau zeigt plausible Ausgabe.
* Alle Optionen sind ausgewählt.
* Keine echten Formulareingaben nötig.

### Task 13: Import/Export implementieren

Implementiere:

* Export als JSON
* Import aus JSON
* Ersetzen oder Hinzufügen
* Konfliktbehandlung bei IDs

Akzeptanz:

* Exportdatei enthält Version, Settings, Templates.
* Import stellt Daten wieder her.
* Ungültige Datei beschädigt den vorhandenen Zustand nicht.

### Task 14: Validierung und Warnungen

Implementiere Validierung:

* fehlender Titel
* unbekannte Platzhalter
* ungenutzte Felddefinitionen
* Optionsfeld ohne Optionen
* leere Labels

Akzeptanz:

* Warnungen sind verständlich.
* App bleibt nutzbar.

### Task 15: Styling und UX-Polish

Verbessere:

* Layout
* Buttons
* Formularabstände
* Hinweise
* Fehlermeldungen
* mobile / kleine Bildschirmbreiten

Akzeptanz:

* Oberfläche ist auf Windows-Schul-PCs gut lesbar.
* Keine externen Ressourcen.

### Task 16: Optional: Platzhalter-Chips

Wenn Version 1 stabil ist, implementiere im Editor klickbare Chips statt roher Platzhalter.

Ziel:

* Sichtbar: `[Name]`
* Intern: `{{field_xxxxx}}`
* Klick öffnet Bearbeitungsdialog

Akzeptanz:

* Nutzer:innen müssen keine geschweiften Klammern sehen.
* Bestehende Templates bleiben kompatibel.

## Nicht-Ziele für Version 1

Nicht implementieren:

* automatischer E-Mail-Versand
* Login
* Benutzerverwaltung
* Synchronisation zwischen Geräten
* Cloudspeicher
* PDF-Export
* Word-Export
* Anhänge
* Schülerdatenbank
* Serienversand
* Outlook-Integration über API
* Gmail-Integration über API

## Optional spätere Erweiterungen

* Betreffzeile automatisch generieren
* `mailto:`-Button
* Vorlagenpakete für Fachschaften
* Pflichtfelder
* geschützte Standardvorlagen
* Druckansicht
* Export als `.txt`
* Export als `.eml`
* Rechtschreib-Hinweise
* neutrale Anredevarianten
* Klassenfeld
* Fachfeld
* eigener Schulname
* Template-Kategorien
* Vorlagen suchen
* Dark Mode

## Wichtige fachliche Vorgabe

Die App darf keine rechtliche Beratung suggerieren. Vorlagen sind Formulierungshilfen. Die Lehrkraft bleibt verantwortlich für Prüfung, Anpassung und Versand.

Empfohlener Hinweis im UI:

```text
Hinweis: Die erzeugten Texte sind Formulierungshilfen. Bitte prüfen Sie Inhalt, Ton und schulrechtliche Angemessenheit vor dem Versand.
```

## Entwicklungsstil

* Schreibe klaren, kommentierten Vanilla-JavaScript-Code.
* Vermeide Frameworks.
* Verwende sprechende Funktionsnamen.
* Halte Rendering, State-Management und Utility-Funktionen möglichst getrennt.
* Keine unnötige Abstraktion.
* Lieber robuste, verständliche Lösung als elegante, aber schwer nachvollziehbare Architektur.
* Achte auf deutsche UI-Texte.
* Nutze UTF-8.
* Achte auf korrekte deutsche Umlaute.

## Fertigstellungskriterium für Version 1

Version 1 ist fertig, wenn eine Lehrkraft ohne technische Kenntnisse:

1. die HTML-Datei per Doppelklick öffnet,
2. eine Vorlage auswählt,
3. Name und Optionen ausfüllt,
4. eine E-Mail generiert,
5. den Text kopiert,
6. die eigene Signatur in Einstellungen speichert,
7. eine eigene Vorlage mit Textfeld und Optionen anlegt,
8. die Daten exportiert und wieder importiert.
