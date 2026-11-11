# Ernährungsprotokoll: Anpassung der Vorlage

Diese Beschreibung zeigt, wie aus `assets/trainingsprotokoll.html` ein Ernährungsprotokoll wird. Die gemeinsamen Teile (Reiter, Speichern, Export, Import) bleiben. Ersetzt werden Eintragsform, Kennzahlen und Export.

## Name und Schlüssel

- Titel und Überschrift: „Ernährungsprotokoll“, Kopfzeile „Ernährung festhalten“.
- `KEY`: `ernaehrungsprotokoll-v1`. JSON-Kennung `app`: `ernaehrungsprotokoll`.
- Akzentfarbe: Petrol, hell `#0e6b66`, dunkel `#5cc4bc`. Weich: hell `#dcefed`, dunkel `#1b3b3a`.

## Datenmodell

Pro Tag ein Dokument `day-YYYY-MM-DD`:

```
{ date, f: { water, move, sleep, feel }, rows: [ { t, m, w, ml, s, n } ] }
```

- `t`: Uhrzeit (`HH:MM`)
- `m`: Art als Index in `MEALS`
- `w`: Was und wie viel, Freitext
- `ml`: Menge in Millilitern, nur bei der Art „Getränk (außer Wasser)“
- `s`: Sättigung als Index in `SAT`
- `n`: Notiz
- Tagesfelder: `water` (ml), `move` (Minuten), `sleep` (Stunden), `feel` (Befinden)

```
MEALS = ["Frühstück", "Zwischenmahlzeit", "Mittagessen", "Abendessen", "Snack", "Getränk (außer Wasser)"]
SAT   = ["–", "Noch hungrig", "Leicht satt", "Satt", "Sehr satt"]
```

Eine Zeile gilt als ausgefüllt, wenn „Was und wie viel“ oder „Notiz“ Text enthält. Zeilen nach Uhrzeit sortieren (ohne Uhrzeit ans Ende), in Verlauf und Export.

## Tag-Reiter

- Datumsnavigation wie in der Vorlage.
- Karte mit Tagesfeldern: Wasser (ml) mit Knöpfen „+ 250“ und „+ 500“, Bewegung (Min.), Schlaf (Std.).
- Karte „Mahlzeiten und Getränke“: Einträge als Blöcke mit Uhrzeit, Art, „Was und wie viel“, bei Getränken zusätzlich Menge (ml), Sättigung und Notiz. Knopf „Eintrag hinzufügen“ wählt die Art nach Tageszeit vor (vor 10 Uhr Frühstück, bis 11 Zwischenmahlzeit, bis 14 Mittagessen, bis 16 Snack, bis 21 Abendessen, danach Snack) und trägt die aktuelle Uhrzeit ein, wenn der Tag heute ist.
- Hinweis unter der Liste: Getränke außer Wasser trägt man als Art „Getränk“ ein, Wasser zählt oben in Millilitern.
- Karte „Auswertung des Tages“ mit Kacheln:
  - Einträge (Mahlzeiten und Getränke)
  - Hauptmahlzeiten (Frühstück, Mittag, Abend)
  - Zwischendurch (Zwischenmahlzeit, Snack, Getränk)
  - Wasser (ml)
  - Andere Getränke (ml, Summe der Mengen)
  - Balken „Einträge nach Art“ und Feld „Befinden, Besonderheiten“

## Verlauf-Reiter

- Überblick: Tage erfasst (mit Zeitraum), Einträge (mit Durchschnitt pro Tag), Wasser (Mittel pro Tag, nur Tage mit Wert), Bewegung (Mittel pro Tag).
- Pro Tag eine Karte mit Kennzahl-Tags, Liste der Einträge nach Uhrzeit (Uhrzeit, Art, Text, Menge, Sättigung, Notiz), Befinden und Knopf „Öffnen“.
- Ein Diagramm ist hier nicht nötig. Wer eine Entwicklung möchte, ergänzt sie aus der Vorlage, etwa Wasser pro Tag oder Anzahl Hauptmahlzeiten.

## Export

Überschrift der Karte: „Für den Arzttermin exportieren“ (oder neutral „Protokoll exportieren“).

CSV mit Semikolon, eine Zeile pro Eintrag:

```
Datum;Uhrzeit;Art;Was und wie viel;Menge (ml);Sättigung;Notiz;Wasser (ml);Bewegung (Min.);Schlaf (Std.);Befinden
```

- Menge nur bei Getränken, Art und Sättigung nur, wenn die Zeile Text hat.
- Tagesfelder (Wasser, Bewegung, Schlaf, Befinden) nur in der ersten Zeile des Tages.
- Tage ohne Einträge, aber mit Tagesfeldern, bekommen eine Zeile mit leeren Eintragsspalten.

Markdown: pro Tag ein Abschnitt, darunter die Tagesfelder in einer Zeile („Wasser: 1500 ml · Bewegung: 30 Min. · Schlaf: 7 Std.“), dann die Tabelle:

```
| Uhrzeit | Art | Was und wie viel | Menge | Sättigung | Notiz |
```

## Hilfe-Reiter

Sechs Hinweise: Direkt eintragen (aus der Erinnerung am Abend fehlen Snacks und Getränke), Mengen beschreiben (Esslöffel, Handvoll, Scheibe, Tasse, Teller), Alles zählt (auch Säfte, Milchkaffee, Kleinigkeiten), Sättigung, Befinden, Muster suchen.

Darunter der Hinweis: „Diese Vorlage dient der Selbstbeobachtung und ersetzt keine ärztliche Beratung. Besprich die Auswertung mit deiner Ärztin oder deinem Arzt.“

## Was aus der Vorlage entfällt

Sätze, Gewichte, Entwicklung pro Übung, Vorschlagslisten für Übungen und die Funktion „Sätze übernehmen“. Vorschläge für Gerichte lassen sich über dieselbe Technik (`datalist` aus früheren Einträgen) ergänzen, wenn gewünscht.
