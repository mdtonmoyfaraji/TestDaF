# Goethe-Zertifikat — Aufgabenformat und digitale Oberfläche

Die Goethe-Prüfungen (A1–C2) laufen in einer eigenen Oberfläche nach dem Goethe-Institut-Demo
„Digital German exams“ (Engine `window.GZ` in `index.html`). Die JSON-Dateien enthalten nur Inhalte;
Zeiten, Teile und Punkte kommen aus den Durchführungsbestimmungen (Stand 01.09.2025) und stehen im
`BLUEPRINTS`-Block von `index.html`.

## Ablauf je Modul
1. Startbildschirm (Niveau-Badge, Modul, Dauer, Hinweise, Tutorial, „Prüfung starten“).
   Beim Hören zusätzlich der Audiocheck („Können Sie gut hören?“).
2. Aufgabenseiten: links Text/Material, rechts Aufgaben; Kopfzeile mit Prüfungsnummer, Restzeit und Reglern
   (Helligkeit, Schriftgröße, Kontrast, Lautstärke); Aufgabenübersicht (☰), Pfeile, Seitenzähler, Layout-Umschalter, Info.
3. Hören: je Teil Lesezeit (Sanduhr) → Wiedergabe 1 (→ Pause mit Signal → Wiedergabe 2) → Bearbeitungszeit → nächster Teil.
4. Sprechen: Vorbereitungszeit mit Notizen (B1: 15 Min., B2: 15, C1: 20, C2: 15; A1/A2 keine), dann die Teile mit Aufnahme.
5. „Prüfung beendet“-Dialog, anschließend die Auswertung (Konversionstabelle 30 Messpunkte → 100 Punkte für B1/B2/C1).

## Optionale Felder
| Feld | Wirkung |
|---|---|
| `audio.script` | Hörtext (Liste von `{speaker, text}`), wird automatisch gesprochen |
| `audio.plays` | Anzahl der Wiedergaben (Standard: `plays` des Teils) |
| `audio.readSec` | Lesezeit vor dem Hören in Sekunden (Standard je Niveau/Teil) |
| `image: true` | zeigt ein Platzhalterbild (immer dasselbe, keine KI-Bilder) |
| `images: true` | Antwortoptionen bzw. Auswahlbank mit Platzhalterbildern (A1/A2 Hören) |
| `personas` | Personenporträts mit Platzhalterfoto (B2 Lesen 1) |
| `format: gapbank` | Sätze per Ziehen (oder Anklicken) in Lücken legen (B2 Lesen 2, C1/C2 Lesen) |
