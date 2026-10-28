# telc Deutsch — Aufgabenformat und digitale Oberfläche

Die telc-Prüfungen (A1–C2) laufen in einer eigenen Oberfläche nach der telc-Prüfungsplattform
(Engine `window.TC` in `index.html`). Die JSON-Dateien enthalten nur Inhalte; Zeiten, Teile und Punkte
stammen aus den offiziellen telc-Übungstests und stehen im `BLUEPRINTS.telc`-Block von `index.html`.

## Prüfungsaufbau (aus den telc-Übungstests)

| Niveau | Block / Modul | Zeit | Teile (Punkte) |
|---|---|---|---|
| **A1** Start Deutsch 1 | Hören | ca. 20 Min | T1 6 (Bilder, a/b/c) · T2 4 (R/F) · T3 5 (a/b/c) = 15 |
| | Lesen + Schreiben (ein Block) | 45 Min | Lesen: T1 5 R/F · T2 5 a/b · T3 5 R/F = 15 · Schreiben: T1 Formular 5 · T2 Mitteilung 10 = 15 |
| | Sprechen | ca. 15 Min | T1 3 · T2 6 · T3 6 = 15 · **gesamt 60, bestanden ab 36** |
| **A2** Start Deutsch 2 | Hören | ca. 20 Min | T1 5 Telefonnotizen · T2 5 a/b/c · T3 5 Zuordnen = 15 |
| | Lesen + Schreiben (ein Block) | 50 Min | Lesen: T1 5 a/b/c · T2 5 R/F · T3 5 Anzeigen (a–h, x) = 15 · Schreiben: Formular 5 + Brief 10 = 15 |
| | Sprechen | ca. 15 Min | 15 · **gesamt 60, bestanden ab 36** |
| **B1 / B2** | Lesen + Sprachbausteine (ein Block) | 90 Min | Lesen T1 5×5 · T2 5×5 · T3 10×2,5 = 75 · Sprachbausteine T1 10×1,5 · T2 10×1,5 = 30 |
| | Hören | B1 ca. 30, B2 ca. 20 Min | T1 5×5 · T2 10×2,5 · T3 5×5 (alle Richtig/Falsch) = 75 |
| | Schreiben | 30 Min | 45 (B2: Aufgabe A *oder* B) |
| | Sprechen | ca. 15 Min (+ 20 Vorb.) | 75 · **schriftlich 225 (ab 135), mündlich 75 (ab 45)** |
| **C1** | Lesen + Sprachbausteine (ein Block) | 90 Min | Lesen T1 6×2 (Sätze in Lücken) · T2 6×2 (Absätze a–e) · T3 11×2 (R/F/nicht im Text) · T4 1×2 Makroaufgabe · Bausteine 22×1 |
| | Hören (nach 20 Min Pause) | ca. 40 Min | T1 8×1 · T2 10×2 · T3 10×2 (Informationen ergänzen) = 48 |
| | Schreiben | 70 Min | 48 (Thema 1 *oder* 2) |
| | Sprechen | ca. 16 Min (+ 20 Vorb.) | 48 · **schriftlich 166 (ab 99), mündlich 48 (ab 29), gesamt ab 128** |
| **C2** | Lesen | 80 Min | T1 5×2 (Abschnitte ordnen) · T2 10×1 (a/b/c) · T3 10×2 (Zuordnen, x) = 40 |
| | Hören und Schreiben | 60 Min | Vortrag hören, Notizen, Zusammenfassung schreiben = 40 |
| | Schreiben (nach 20 Min Pause) | 90 Min | Aufsatz mit Quellentexten = 40 |
| | Sprechen | ca. 15 Min (+ 20 Vorb.) | Vortrag 6–8 Min + vertiefendes Gespräch = 40 · **schriftlich 120 (ab 72), mündlich 40 (ab 24), gesamt ab 96** |

Zusammengehörige Untertests laufen wie in der echten Prüfung in **einem** Block mit gemeinsamer Uhr
(`blockWith` / `blockMinutes` im Blueprint). Die Reiter oben zeigen alle Teile des Blocks; erledigte Teile erhalten einen Haken.

## Oberfläche (wie auf den telc-Screenshots)
- Kopfzeile: telc-Logo, Reiter „Leseverstehen Teil 1 (25 Punkte)“, „Deutsch – B2“, „Verbleibende Zeit“, „Restzeit“, **ABGABE** und **SPEICHERN**.
- Blaue Untertest-Leiste („Leseverstehen, TEIL 1“), gelber Hinweiskasten, Fußzeile mit „TEST USER“, **CHARACTERS** (ä ö ü ß …), „Meldung:“.
- Hören: Player im Kopf (▶/❚❚, Zeit, Lautstärke). Die Aufnahme läuft durchgehend: Lesezeit → Signalton → Wiedergabe (ggf. 2×) → Bearbeitungszeit → nächster Teil; die Reiter springen mit.
- **ABGABE** → „SIND SIE SICHER, DASS SIE DIE PRÜFUNG VERSENDEN WOLLEN?“ → „Ich danke Ihnen! …“ → Ergebnis.
- Wörterbuch/Hilfsmittel: nicht vorgesehen. Bilder in den Aufgaben sind immer dasselbe Platzhalterbild.

## Aufgabentypen und Felder (je Teil unter `content.<Modul>.<Teil-ID>`)
| Format (Blueprint) | Darstellung | Felder |
|---|---|---|
| `tf` / `tfn` | Tabelle RICHTIG / FALSCH (/ NICHT IM TEXT) | `items[{prompt, answer: 0\|1\|2}]`, optional `passage`, `texts[{label,text}]`, `audio` |
| `mc2` / `mc3` / `mc4` | Karten mit Auswahl | `items[{prompt, options[], answer}]`, optional `passage`, `images: true` (Platzhalterbilder je Option) |
| `match` + `ui:"heads"` | Überschriften per Drag & Drop (oder Anklicken) auf Texte | `bank[{key,text}]` = Überschriften, `items[{prompt = Text, answer = key}]` |
| `match` + `ui:"ads"` | Situationen auf Anzeigen ziehen, `x` = keine passt | `bank` = Anzeigen, `items[{prompt = Situation, answer = key \| "x"}]` |
| `match` + `ui:"paras" \| "persons"` | Buchstaben wählen | `bank` = Absätze bzw. Aussagen, `items[{prompt, answer}]` |
| `order` | Reihenfolge der Abschnitte | `example{key,text}`, `bank` = Abschnitte, `items[{answer = key an Position n}]` |
| `gapmc` | Lückentext links, Auswahl rechts | `passage` mit `___1___` …, `items[{options[], answer}]` |
| `gapbank` | Lückentext mit Wortbank bzw. Sätzen | `passage`, `bank[{key,text}]`, `items[{answer = key}]` |
| `short` | Eingabefelder (Telefonnotiz, Formular, Informationstransfer) | `items[{prompt, answer, answers[] = Varianten}]`, optional `passage`, `formTitle`, `audio` |
| `writing` | Textfeld mit Wortzähler, KI-Bewertung | `stimulus`, `prompt`, `bullets[]`, `words`; bei Wahlaufgabe `tasks[{key,title,stimulus,prompt,bullets,words}]` + `choiceLabel` |
| `speaking` | Sprechaufgabe mit Aufnahme | `prompt`, `bullets[]`, `topics[]`, `seconds` |

Hörtexte: `audio: { plays, readSec, script: [{speaker, text}] }`. Short-Antworten werden ohne Groß-/Kleinschreibung und
ohne Satzzeichen verglichen; Schreiben und Sprechen werden per KI bewertet (Anteil der Teilpunkte).
