# Skill „protokoll-artefakt“

## Wichtiger Hinweis

Ich bin kein Programmierer.
Dieser Skill wird so bereitgestellt, wie er ist, ohne Garantie, Support oder laufende Pflege.

* Keine Fehlermeldungen
* Keine Funktionswünsche
* Kein Versprechen, dass er in Zukunft weiter funktioniert

Wenn er bei dir funktioniert: schön.
Wenn nicht: Passe ihn gern für deine Zwecke an.
Nutzung auf eigene Gefahr.

## Was der Skill ist

Ein Skill ist ein Ordner mit Anweisungen, die ein KI-Assistent vor einer Aufgabe liest. Dieser Skill erklärt, wie man ein **persönliches Protokoll als einzelne Webseite** baut: ein Trainingsprotokoll, ein Ernährungsprotokoll oder ein ähnliches Logbuch (Schlaf, Lesen, Schreiben, Stimmung).

Er wurde für Claude geschrieben und setzt dort auf „Artefakte“ (Webseiten, die Claude im Chat anlegt und die eigene Daten speichern können). Die Anleitung und die Vorlage sind aber normale Textdateien und HTML, siehe Abschnitt „Verwendung mit anderen KI-Assistenten“.

## Inhalt des Ordners

| Datei | Zweck |
|---|---|
| `SKILL.md` | Die eigentliche Anleitung: Ablauf, Fragen, Anpassung, Regeln, Stolperfallen |
| `assets/trainingsprotokoll.html` | Fertige Vorlage, vollständig lauffähig |
| `references/ernaehrung.md` | Beschreibung, wie aus der Vorlage ein Ernährungsprotokoll wird |
| `README.md` | Diese Datei |

## Was der Skill kann

- Mit **Fragen, die er einzeln nacheinander stellt,** klären, was protokolliert werden soll (Arten, Felder, Auswertung, Export). Die nächste Frage kommt erst, wenn du geantwortet hast.
- Aus der Vorlage ein **fertiges Protokoll** mit vier Reitern erzeugen: Tag, Verlauf, Export, Hilfe.
- **Einträge pro Tag** erfassen, bei Kraft und Calisthenics jeden Satz einzeln, Gewicht optional, bei Ausdauer nur die Dauer.
- **Vorschläge** aus früheren Einträgen anbieten und die Sätze vom letzten Mal übernehmen lassen.
- Den **Verlauf pro Übung** als Diagramm und Tabelle zeigen (Gewicht, Wiederholungen, Volumen, Sätze, Dauer).
- **Exportieren** als CSV (Semikolon, Dezimalkomma, eine Zeile pro Übung und Tag mit Durchschnittswerten), als Markdown und als JSON-Sicherung, mit Wiedereinlesen der Sicherung.
- **Im eigenen Konto speichern**, wenn die Umgebung das erlaubt (nur du siehst die Einträge), sonst im Browser auf dem Gerät.
- Auf dem Smartphone nutzbar sein und ein helles und dunkles Erscheinungsbild haben.

## Was der Skill nicht kann

- **Keine Daten übernehmen.** Bestehende Einträge aus anderen Apps oder Tabellen importiert er nicht. Nur die eigene JSON-Sicherung lässt sich wieder einlesen.
- **Kein Trainingsplan, keine Beratung.** Er zeichnet auf und wertet aus. Er schlägt weder Übungen noch Ernährung vor und ersetzt keine ärztliche oder sportliche Beratung.
- **Keine Berechnung von Kalorien oder Nährwerten.** Das Ernährungsprotokoll erfasst Freitext und Mengen, keine Nährwertdatenbank.
- **Kein Geräteanschluss.** Uhren, Pulsgurte und Fitness-Apps lassen sich nicht anbinden.
- **Kein Teilen und keine Mehrbenutzerfunktion.** Das Protokoll ist für eine Person gedacht.
- **Kein Cloud-Abgleich.** Außerhalb von Claude werden die Einträge weder zwischen Geräten abgeglichen noch mit Cloud-Diensten wie iCloud, Dropbox oder Google Drive synchronisiert. Wer das braucht, lädt die JSON-Sicherung herunter und legt sie selbst dort ab.
- **Keine Garantie für Speichern und Download in jeder Umgebung.** Das hängt von den Fähigkeiten der Umgebung ab (siehe unten).
- **Nicht getestet** mit fremden Personen, frischen Konten oder anderen KI-Assistenten als Claude.

## Verwendung in Claude

1. Den Ordner `protokoll-artefakt` als ZIP in die Skill-Verwaltung hochladen (in den Einstellungen, Bereich Fähigkeiten bzw. Skills).
2. Im Chat sagen, was man protokollieren möchte, etwa: „Ich möchte ein Protokoll für mein Training“ oder „Baue mir ein Schlafprotokoll“.
3. Die Fragen der Reihe nach beantworten. Claude stellt immer nur eine. Kurze Stichworte genügen.
4. Claude baut die Seite und legt sie als Artefakt an. Nur du kannst sie öffnen, solange du sie nicht selbst teilst.
5. Beim ersten Eintrag prüfen, ob Speichern, Diagramm und Download funktionieren.
6. Änderungen später im selben Chat wünschen, dann bleibt die Adresse gleich.

## Verwendung mit anderen KI-Assistenten

Die Anleitung ist reines Markdown, die Vorlage eine einzelne HTML-Datei mit eingebettetem Skript. Beides lässt sich auch ohne Claude nutzen. Was dabei zu beachten ist:

**Anleitung einsetzen**
- Den Inhalt von `SKILL.md` als Systemanweisung, als Projektanweisung oder als erste Nachricht einfügen. Danach die Vorlage `assets/trainingsprotokoll.html` anhängen oder einfügen und sagen: „Folge der Anleitung. Stelle zuerst die Fragen, eine nach der anderen, und warte jeweils auf meine Antwort.“
- Assistenten, die Dateien lesen und anlegen können, etwa Claude Code oder OpenAI Codex, können den ganzen Ordner einlesen und die fertige Seite direkt als Datei speichern. Bei reinen Chat-Fenstern ohne Dateizugriff die Dateien nacheinander einfügen, die Vorlage hat rund 50 KB.
- Verweise in der Anleitung auf Claude-Werkzeuge (Artifact-Tool, die Skills `artifact-design` und `artifact-capabilities`) werden von anderen Assistenten ignoriert. Das schadet nicht. Der Assistent liefert die fertige HTML-Datei dann als Text oder Datei.
- Man kann den Assistenten auch anweisen, für Gestaltung und Vorschau seine eigenen Werkzeuge zu nutzen, zum Beispiel mit: „Gestalte die Seite mit deinen eigenen Werkzeugen und liefere eine einzelne HTML-Datei.“ Die Gestaltungsregeln von Claude fehlen dort. Die Vorlage gibt Aufbau und Aussehen aber schon weitgehend vor.

**Fertige Seite verwenden**
- Die HTML-Datei speichern und im Browser öffnen. Sie läuft ohne Server und ohne Internet, nur die Schriften kommen von Google Fonts und fallen sonst auf Systemschriften zurück.
- Einträge liegen dann im **Speicher des Browsers** (`localStorage`). Sie bleiben auf diesem Gerät und in diesem Browser, und sie gehen verloren, wenn man den Browser-Cache samt Cookies und Website-Daten löscht. Regelmäßig die JSON-Sicherung herunterladen.
- **Wichtige Einschränkung:** Die Downloadknöpfe (CSV, Markdown, JSON) hängen an einer Claude-Funktion. Ohne sie blendet die Vorlage die Knöpfe aus, übrig bleibt „Markdown kopieren“. Für den Einsatz außerhalb von Claude muss die Funktion `save()` ergänzt werden: Die Datei im Browser erzeugen und über einen unsichtbaren Download-Link zum Herunterladen anbieten. Abschnitt 3 in `SKILL.md` beschreibt das, ein anderer Assistent kann es mit dem Auftrag „Ergänze einen Download-Rückfall in save()“ erledigen.
- Wer geräteübergreifend speichern möchte, braucht eine eigene Lösung (eigener Server, Cloud-Datei). Das leistet der Skill nicht.

**Hinweis zur Prüfung**
Jede Seite, die ein KI-Assistent baut, sollte man selbst testen: einen Eintrag anlegen, die Seite neu laden, die CSV exportieren und in einem Tabellenprogramm öffnen. Prüfe dabei besonders Umlaute, Dezimalkommas und die Durchschnittswerte.

## Anpassung

Eigene Themen entstehen, indem man die Fragen beantwortet. Der Assistent ändert dann Namen, Arten, Felder, Kennzahlen und Spalten der Vorlage. Die Stellen dafür stehen in Abschnitt 4 von `SKILL.md`. Das Ernährungsprotokoll ist als Beispiel in `references/ernaehrung.md` beschrieben.

## Datenschutz

Trainings- und Ernährungsdaten sind persönlich. In Claude liegen sie in deinem Konto und sind nur für dich sichtbar. Andere können die Seite nur öffnen, wenn du sie selbst teilst. Im Browser-Speicher liegen die Einträge nur auf dem eigenen Gerät. Das Protokoll dient der Selbstbeobachtung und ersetzt keine ärztliche Beratung.
