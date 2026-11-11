---
name: protokoll-artefakt
description: Baut ein persönliches Protokoll als Artefakt, zum Beispiel Trainings- oder Ernährungsprotokoll, mit Reitern Tag, Verlauf, Export und Hilfe, privater Speicherung und CSV-Export. Nutzen, wenn jemand ein Protokoll, einen Tracker oder ein Logbuch zum täglichen Eintragen und Auswerten haben möchte.
---

# Protokoll-Artefakt

Dieser Skill baut ein Protokoll, in das man täglich Einträge macht, später auswertet und exportiert. Er enthält eine fertige Vorlage (Trainingsprotokoll) und eine Anleitung für ein Ernährungsprotokoll. Beides lässt sich auf andere Themen übertragen, etwa Schlaf, Lesen, Schreiben, Stimmung oder Medikamente.

Der Skill braucht keine bestehenden Artefakte. Alles Nötige liegt im Skill-Ordner:

- `assets/trainingsprotokoll.html`: vollständige Vorlage, die als Ausgangspunkt dient.
- `references/ernaehrung.md`: Beschreibung des Ernährungsprotokolls zum Anpassen der Vorlage.

Sprache der Oberfläche: Deutsch, Du-Form. Wer eine andere Sprache wünscht, bekommt die Texte der Vorlage übersetzt.

## 1. Ablauf

1. **Fragen stellen, bevor gebaut wird.** Die Fragen aus Abschnitt 2 einzeln stellen, eine pro Nachricht, und die nächste erst nach der Antwort. Unklare Stichworte nicht raten.
2. **Umgebung prüfen** (Abschnitt 3).
3. **Vorlage lesen.** `assets/trainingsprotokoll.html` vollständig lesen. Sie enthält Speicherlogik, Reiter, Diagramm und Export, die für jedes Protokoll gleich bleiben.
4. **Anpassen** (Abschnitt 4). Die Vorlage nur dort ändern, wo die Antworten es verlangen.
5. **Veröffentlichen und prüfen** (Abschnitt 6).
6. **Abschluss:** ein bis zwei Sätze zum Ergebnis, was geprüft wurde und was nicht. Bei Aufgabenlisten die letzte Aufgabe erst nach der Prüfung abhaken.

## 2. Fragen: eine nach der anderen

**Regeln**

- Immer nur eine Frage pro Nachricht. Die nächste Frage erst stellen, wenn die Antwort da ist. Nicht auf Vorrat fragen und keine Fragenliste ankündigen.
- Jede Frage kurz halten und mit ein oder zwei Beispielen versehen, damit niemand bei null anfangen muss. Keine Doppelfragen in einem Satz („Was, wie und wozu?“).
- Die nächste Frage aus der letzten Antwort ableiten. Was schon beantwortet ist, nicht erneut fragen. Fragen überspringen, die für dieses Protokoll nicht zutreffen.
- Ist eine Antwort unklar oder mehrdeutig, zuerst sie klären, bevor es weitergeht. Nicht raten. Die vermutete Lesart nennen und fragen („Meinst du …?“).
- Macht jemand von sich aus mehrere Angaben auf einmal, diese übernehmen und nur offene Punkte nachfragen, wieder einzeln.
- Zwischen den Fragen keine Zusammenfassungen und kein Lob. Eine Bestätigung ist höchstens ein halber Satz.
- Nach der letzten Antwort in einem Satz sagen, was gebaut wird, und mit dem Bauen beginnen (Abschnitt 3).

**Reihenfolge** (Vorschlag, bei Bedarf umstellen)

1. Was wird protokolliert? Welche Arten oder Kategorien gibt es?
2. Welche Angaben gehören zu einem Eintrag?
3. Welche davon sind optional?
4. Wozu dient das Protokoll: Dokumentation, Auswertung, Planung, Termin bei Arzt oder Coach?
5. Welche Entwicklung über die Zeit soll sichtbar sein (z. B. Gewicht pro Übung, Mittelwerte pro Woche, Bestwerte)?
6. Sollen Namen frei eingegeben werden (mit Vorschlägen aus früheren Einträgen) oder aus einer festen Liste kommen?
7. Export: CSV, Markdown oder beides?
8. Nur wenn CSV gewünscht ist: Wie fein soll sie sein (eine Zeile pro Eintrag, pro Übung oder pro Tag)? Einzelwerte oder Durchschnitt?
9. Gibt es Besonderheiten, etwa Einheiten, Dauer, Befinden oder Notizen?

## 3. Umgebung prüfen

Das Artefakt läuft in Claude.ai mit dem Artifact-Tool. Falls ein Skill `artifact-design` oder `artifact-capabilities` verfügbar ist, beide laden, bevor die Datei geschrieben wird. Danach prüfen, welche Fähigkeiten vorhanden sind:

| Fähigkeit | Nutzen | Wenn sie fehlt |
|---|---|---|
| `db` und `user` | Speicherung im eigenen Konto, ein Dokument pro Tag | Die Vorlage fällt auf `localStorage` zurück. Dann steht im Statuschip „Nur auf diesem Gerät gespeichert“. Das ausdrücklich sagen. |
| `downloads` | Dateien speichern (CSV, Markdown, JSON) | Die Speicherknöpfe werden ausgeblendet. „Markdown kopieren“ mit markiertem Textfeld bleibt als Rückfall. |

Ohne Artifact-Tool die Datei als `.html` ausliefern. Sie läuft dann im normalen Browser mit `localStorage`. In `save()` ergänzt man dafür einen Rückfall: Blob erzeugen, einen Link mit `download`-Attribut anlegen und anklicken.

Veröffentlichen mit `capabilities: {"db": {}, "user": {}, "downloads": true}`, sofern die Fähigkeiten angeboten werden.

## 4. Vorlage anpassen

Gleich bleiben: Kopf mit Statuschip, Reiter, Datumsnavigation, Speicherlogik (`touch`, `flush`, `onSnapshot`), Rückfall auf `localStorage`, Export und Import, Hilfe-Reiter, Farbtokens und Hell-Dunkel-Umschaltung.

Anzupassen sind:

1. **Name und Schlüssel:** `<title>`, Überschrift, `KEY` (z. B. `schlafprotokoll-v1`), `app`-Kennung im JSON, Dateinamen.
2. **Akzentfarbe:** pro Protokoll ein eigener Ton, sonst sehen alle gleich aus.
3. **Arten:** das Array `TYPES` und die Regel `isEnd(k)`, die bestimmt, welche Arten nur eine Dauer haben.
4. **Eintragsform:** Datenmodell der Zeilen (`blankRow`, `normalize`, `filledRow`) und die Maske (`exHtml`). Bei Sätzen gibt es eine Unterliste, bei einfachen Protokollen genügen Felder pro Zeile.
5. **Kennzahlen:** `agg`, `stats`, `METRICS` und die Kacheln „Auswertung des Tages“ und „Überblick“.
6. **Entwicklung:** `buildSeries` fasst Einträge nach Namen zusammen. Bei Protokollen ohne Namen die Reihe nach Art oder Tagesfeld bilden.
7. **Export:** Spalten in `buildCsv`, Tabelle in `buildMd`, Zeitraumtext.
8. **Hilfe-Reiter:** sechs kurze Hinweise, die zum Thema passen.

Für das Ernährungsprotokoll `references/ernaehrung.md` lesen. Dort stehen Felder, Kennzahlen und Spalten.

## 5. Regeln für die Umsetzung

**Daten**
- Speicherort: `db.collection("data/users/" + uid)`, ein Dokument pro Tag mit der ID `day-YYYY-MM-DD`. Das ist privat für die eigene Person.
- Jeden Eintrag beim Einlesen mit `normalize()` bereinigen. Ältere Einträge dürfen nie ungültig werden, wenn später Felder hinzukommen.
- Speichern verzögert (700 ms), pro Tag ein Schreibvorgang gleichzeitig, bei Fehler erneut versuchen. Beim Verlassen der Seite alles sichern.
- Datumsrechnung über `Date.UTC(...) / 86400000`, damit Sommerzeit nichts verschiebt.
- Keine erfundenen Beispieldaten in der Datenbank. Ein leerer Tag zeigt einen klaren Hinweis und die Knöpfe zum ersten Eintrag.

**CSV**
- Semikolon als Trenner, Byte-Order-Mark am Anfang, Zeilenende `\r\n`.
- Jede Zelle in Anführungszeichen, Anführungszeichen verdoppeln. Zellen, die mit `=`, `+`, `-` oder `@` beginnen, mit einem Apostroph schützen.
- Dezimalzahlen mit Komma, damit Excel und Numbers in deutschen Einstellungen sie als Zahl lesen.
- Tagesangaben (z. B. Befinden) nur in der ersten Zeile des Tages.

**Verlauf und Diagramm**
- Reihen nach Namen zusammenführen, ohne Unterschied bei Groß- und Kleinschreibung. Mehrere Blöcke am selben Tag zusammenrechnen.
- Nur Kennzahlen anbieten, für die Werte existieren.
- Für sichtbare Steigerungen ist das höchste Gewicht des Tages die klarste Kennzahl und die Voreinstellung. Ein Durchschnittsgewicht verwischt Stufen (Sätze mit 4, 4 und 5 kg ergeben 4,33) und ist deshalb nicht Teil der Vorlage. Das Volumen (Wiederholungen × Gewicht) bleibt als Zusatz, mit Hinweis, dass Sätze ohne Gewicht nicht zählen.
- Diagramm als SVG in der echten Breite des Containers, Zeitachse maßstäblich, runde Achsenwerte, bei Zählwerten ganze Schritte. Farben nur aus Tokens. Neu zeichnen bei Größenänderung.
- Darunter Erster Wert, Letzter Wert, Bestwert und eine Tabelle.

## 6. Prüfen und veröffentlichen

1. Das Skript aus der Datei herausziehen und mit `node --check` auf Syntax prüfen. Das braucht keine Paketinstallation.
2. Veröffentlichen mit einem passenden `icon`, einer einsätzigen `description` und den Fähigkeiten aus Abschnitt 3. Spätere Änderungen mit derselben Datei veröffentlichen, damit die Adresse gleich bleibt.
3. Die private Datenbank lässt sich von außen nicht lesen. Das ehrlich sagen und bitten, Speichern, Diagramm und Download beim ersten Eintrag zu testen.

## 7. Stolperfallen

- `grid-area` nur setzen, wo ein Raster mit benannten Bereichen besteht. Sonst entstehen unsichtbare Zusatzspalten.
- Beim Tippen nicht die ganze Liste neu zeichnen, sonst geht der Fokus verloren. Nur Kennzahlen und Hinweiszeilen aktualisieren. Die Vorschlagsliste erst bei `change` neu aufbauen.
- `confirm()`, `alert()` und Links mit `download` funktionieren im Artefakt nicht. Löschen mit „Rückgängig“ lösen, Dateien über `downloads.save`.
- Optionale Felder bleiben leer und zählen nicht als Null in Durchschnitten.
- Reiter-IDs, Schlüssel und `app`-Kennung eindeutig halten, damit sich zwei Protokolle nicht überschreiben oder gegenseitig einlesen.

## 8. Datenschutz

Trainings-, Ernährungs- und Gesundheitsdaten sind persönlich. Sie liegen im eigenen Konto, die Veröffentlichung ist zunächst privat. Nicht aus Bequemlichkeit teilen. Bei Ernährung und Gesundheit den Hinweis aufnehmen, dass das Protokoll der Selbstbeobachtung dient und keine ärztliche Beratung ersetzt.
