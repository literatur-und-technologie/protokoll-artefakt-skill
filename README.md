# protokoll-artefakt

Ein Skill für Claude, der ein persönliches Protokoll als einzelne Webseite baut, zum Beispiel ein Trainings- oder Ernährungsprotokoll. Das Protokoll hat die Reiter Tag, Verlauf, Export und Hilfe, wertet die Entwicklung über die Zeit aus und exportiert als CSV (Semikolon), Markdown und JSON-Sicherung.

Der Skill stellt zuerst Fragen, eine nach der anderen, und baut danach aus einer mitgelieferten Vorlage das passende Protokoll. Er braucht keine bestehenden Artefakte.

## Inhalt

| Pfad | Zweck |
|---|---|
| `protokoll-artefakt/SKILL.md` | Die Anleitung für den Assistenten |
| `protokoll-artefakt/assets/trainingsprotokoll.html` | Fertige, lauffähige Vorlage |
| `protokoll-artefakt/references/ernaehrung.md` | Anpassung der Vorlage zum Ernährungsprotokoll |
| `protokoll-artefakt/README.md` | Ausführliche Erklärung: was der Skill kann und nicht kann, Nutzung in Claude und mit anderen KI-Assistenten |

## Schnellstart in Claude

1. Die Datei `protokoll-artefakt.zip` aus dem [neuesten Release](https://github.com/literatur-und-technologie/protokoll-artefakt-skill/releases/latest) herunterladen. Wer den Skill vorher selbst ändert, packt den Ordner `protokoll-artefakt` selbst als ZIP. Die ZIP-Datei muss den Ordner selbst enthalten, nicht nur seinen Inhalt.
2. Die ZIP-Datei in Claude in den Einstellungen unter Fähigkeiten (Skills) hochladen.
3. Im Chat sagen, was protokolliert werden soll, etwa „Ich möchte ein Protokoll für mein Training“, und die Fragen der Reihe nach beantworten.

Die ausführliche Anleitung steht in [`protokoll-artefakt/README.md`](protokoll-artefakt/README.md).

## Hinweise

- Der Skill wurde für Claude geschrieben. Mit anderen KI-Assistenten ist er nicht getestet.
- Gespeichert wird im eigenen Claude-Konto, sonst im Browser auf dem Gerät. Einen Cloud-Abgleich außerhalb von Claude gibt es nicht.
- Das Protokoll dient der Selbstbeobachtung und ersetzt keine ärztliche oder sportliche Beratung.

## Lizenz

[MIT](LICENSE)
