# Priorisierer 3000

Aufgaben priorisieren wie Fluglotsen ihre Flugstreifen: Was oben liegt, ist dran. Eine einzige HTML-Datei, die Daten liegen in einer JSON-Datei auf deinem Rechner oder in OneDrive.

## Einrichten (einmalig, in Microsoft Edge)

1. `index.html` an einen festen Ort kopieren, zum Beispiel `Dokumente\Priorisierer\index.html`.
2. Die Datei per Doppelklick in **Edge** öffnen. Wichtig: nicht in einer Vorschau, sondern direkt im Browser.
3. Im Startbildschirm **Neue Datei anlegen** wählen und die `priorisierer.json` speichern. Am besten in einem OneDrive-Ordner, dann ist sie automatisch gesichert.
4. Fertig. Ab jetzt wird die Datei bei jedem Start geladen und jede Änderung nach einer knappen halben Sekunde gespeichert.

**Als Startseite in Edge:** Einstellungen, *Start, Startseite und neue Tabs*, *Diese Seiten öffnen*, dann den Pfad eintragen, zum Beispiel `file:///C:/Users/<Name>/Documents/Priorisierer/index.html`.

**Nach einem Neustart von Edge** steht oben rechts eventuell „wieder verbinden (1 Klick)“. Ein Klick darauf genügt, Edge fragt dann einmal nach der Erlaubnis.

## Bedienung

| Was | Wie |
|---|---|
| Reihenfolge ändern | Streifen am Griff ⋮⋮ oder an der Prio-Nummer ziehen, alternativ `Alt + ↑/↓` |
| Neue Aufgabe | `＋ Aufgabe` oder Taste `N`. Neue Aufgaben starten unten. |
| Ampel | Punkte in der Spalte Ampel, oder Klick auf den Farbbalken links |
| Aufwand | Story Points 1, 2, 3, 5, 8, 13, 21. Nochmal klicken entfernt die Schätzung. |
| Deadline | Klick in die Spalte Deadline |
| Erledigt | Grüner Haken im Streifen oder „Erledigt“ in der One-Thing-Kachel |
| Warten auf | Chip unter dem Titel aufklappen, oder Ansicht „Warte auf“ oben rechts |
| Projekte | Tab „Projekte“: anlegen, umbenennen, Farbe, Reihenfolge, löschen |
| Rückgängig | „Rückgängig“ in der Meldung unten oder `Strg + Z` |

## Datensicherheit

- **Automatisch speichern** in die verknüpfte Datei, zusätzlich immer eine Kopie im Browser.
- **Konflikte:** Wurde die Datei inzwischen woanders geändert (zum Beispiel an einem zweiten PC über OneDrive), überschreibt der Priorisierer sie nicht still. Er fragt, welcher Stand gelten soll. Kehrst du ins Fenster zurück und die Datei ist neuer, wird sie automatisch geladen.
- **Defekte Datei:** Ist die JSON-Datei beschädigt, wird nichts überschrieben, und oben rechts erscheint ein Hinweis.
- **Tägliche Sicherung:** Der erste Stand jedes Tages wird im Browser abgelegt, die letzten 14 Tage bleiben erhalten. Wiederherstellen über *Datei, Sicherung wiederherstellen*.
- **Export:** *Datei, Als JSON herunterladen* legt eine Kopie mit Datum im Namen an.

## Technik

- Eine Datei, kein Server, keine Installation. Läuft vollständig lokal.
- Dateizugriff über die File System Access API. Die läuft in Edge und Chrome, nicht in Firefox. Dort bleiben Import und Export.
- Schriften Inter und Lora kommen von Google Fonts. Ohne Internet wird automatisch Segoe UI und Georgia genutzt.
- Datenformat und Fahrplan: siehe [PLAN.md](PLAN.md).
