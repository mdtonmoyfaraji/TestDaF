# TestDaF-Modelltests im Format des offiziellen g.a.s.t.-Demo-PDFs

Ordner = ein Modelltest, darin `lesen.json`, `hoeren.json`, `schreiben.json`, `sprechen.json`
(Kopf wie bei den vorhandenen Dateien: `kind, version, exam:"testdaf", level:"TestDaF", module, name, content`).
`content` enthält je Aufgabentyp einen Schlüssel (L1–L7, H1–H7, S1–S2, P1–P7).
Die **Arbeitsanweisungen, Zeiten und Itemzahlen** stehen fest in der App (nach PDF) – in den JSON-Dateien steht nur der Inhalt.
Zeichen: `**fett**`, `__kursiv__`. Absätze durch Leerzeile.

| Typ | Pflichtfelder | Items |
|---|---|---|
| L1 | `title`, `passage` mit `[1]`…`[5]`, `items:[{options:[4 Wörter], answer:"a"-"d"}]` | 5 |
| L2 | `paras:[{key,text}]` (5, in angezeigter Reihenfolge), `order:[keys richtig]`, `items:[{answer:key}]` für Position 2–5 | 4 |
| L3 | `title`, `passage` (Absätze mit `(1)`…), `items:[{prompt, options:[4], answer:Index}]` | 7 |
| L4 | `title`, `passage` mit `[1]`…`[4]` (Zahl bezieht sich auf den folgenden Satz), `items:[{answer:"a"-"h"}]` (a bedauert, b begrüßt, c empfiehlt, d kritisiert, e prognostiziert, f vermutet, g warnt vor, h zweifelt an) | 4 |
| L5 | `title`, `passage`, `cats` (4, Standard Stadt/Land/beide/passt nicht), optional `catPhrase`, `items:[{prompt, answer:0-3}]` | 7 |
| L6 | `title`, `heading`, `pair:[Spalte1,Spalte2]`, `passage`, `statements:[{t, col:0\|1\|null}]` (8; 4 richtige), `items:[{prompt, answer:col}]` (nur die richtigen) | 4 |
| L7 | `title`, `passage`, `chart`, `summary:[Sätze]`, `wrong:[3 Indizes]`, `items:[{answer:Index}]` | 3 |
| H1 | `topic`, `grid{title, headRight, cols, rows}` (Zellen mit `[[1]]`…`[[5]]` = Eingabefeld; Zeile `{span:"Mittagessen"}`), `audio.script`, `items:[{prompt, answer, alts[]}]` | 5 |
| H2 | `topic`, `persons:[2]`, `audio.script`, `items` (4: P1-Forderung, P1-Argument, P2-Forderung, P2-Argument) mit `answer`, `alts[]` | 4 |
| H3 | `topic`, `field`, `audio.script`, `summary`, `wrong:[2]`, `items:[{answer:Index}]` | 2 |
| H4 | `topic`, `persons:[2]`, `speakers`, `audio.script`, optional `video` (URL), `items:[{prompt, answer:0 Person1 \| 1 Person2 \| 2 beide \| 3 keiner}]` | 6 |
| H5 | `topic`, `field`, `slideTitle`, `audio.script`, `items:[{prompt, answer, alts[]}]` | 4 |
| H6 | `topic`, `audio.script`, `items:[{prompt, options:[4], answer:Index}]` | 5 |
| H7 | `topic`, `title`, `text` mit `{{geschrieben\|gehört}}` (4×), `audio.script`, `items:[{answer:"ok"}]×4` | 4 |
| S1 | `title`, `situation`, `task`, `notes[]` | – |
| S2 | `title`, `situation`, `task`, `text`, `chart`, `notes[]` | – |
| P1,P2,P7 | `situation`, `task`, `notes[]` (P7 zusätzlich `notice:{title,text}`) | – |
| P3 | `title`, `situation`, `task`, `text`, `notes[]` | – |
| P4 | `situation`, `task`, `chart`, `statement.script`, `notes[]` | – |
| P5 | `situation`, `task`, `outline:{title, points:[…{t,sub[]}]}`, `notes[]` | – |
| P6 | `situation`, `task`, `statement.script`, `notes[]` | – |

`audio.script` = `[{speaker, text}]`; optional `audioUrl` (mp3) ersetzt die Sprachausgabe. `video` (mp4) bei H4/H5.
`chart` = `{title, cats[], series:[{name, values[], color?}], max, step, unit?, axis?, horizontal?, tags?}`.
Kurzantworten (H1/H2/H5) werden gegen `answer` + `alts` toleranter abgeglichen (Schlüsselwörter, ≥60 %).

## KI-Erzeugung
Die KI-Generierung ist für TestDaF aktiv. Für jede der 23 Aufgaben (L1–L7, H1–H7, S1–S2, P1–P7) gibt es ein festes Feldschema (siehe oben). Antworten der KI werden geprüft (Markerzahl, Optionen, Indizes, Diagramm) und fehlende abgeleitete Felder automatisch ergänzt: `items` aus `order` (L2), `statements` (L6) und `wrong` (L7, H3); Hörtext und `items` aus dem `{{geschrieben|gehört}}`-Text (H7). Fehlerhafte Antworten werden verworfen und mit der konkreten Fehlermeldung neu angefragt.
