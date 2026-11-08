# Priorisierer 3000 · Plan

## 1. Ziel

Eine einzelne HTML-Datei, die Aufgaben als waagrechte **Flugstreifen** zeigt, wie Fluglotsen ihre Flight Strips führen.
Was oben liegt, hat Prio 1. Die Daten liegen in einer **JSON-Datei**, die einmal verknüpft wird und danach bei jedem Start automatisch geladen und gespeichert wird.
Optimiert für einen 16:9-Bildschirm, scrollbar, mit Projekten als Kategorien.

## 2. Aufbau eines Streifens

| Bereich | Inhalt | Bedeutung |
|---|---|---|
| ⋮⋮ Griff | Drag & Drop | Reihenfolge ist die Priorität |
| Farbbalken (ganz links) | Ampelfarbe | Dringlichkeit, Klick schaltet weiter |
| Prio-Nummer | 01, 02, … | ergibt sich automatisch aus der Position |
| Überschrift + Projekt | Titel, Projekt-Auswahl | Was und wofür |
| Notiz | freier Text | nächster Schritt, Kontext, Blocker |
| Ampel | 4 Punkte | Dringend · Bald · Kann warten · Wartet |
| Story Points | 1 2 3 5 8 13 21 | Aufwand nach Fibonacci, wie in Scrum |

## 3. Farbsystem (aus deinen zwei Paletten)

**Ampel / Dringlichkeit**
- Rot `#f9596f` Dringend
- Gelb `#ffa600` Bald
- Grün `#238b4a` Kann warten
- Lila `#674f95` Wartet auf andere / blockiert

**Aufwand (Story Points)** läuft von Grün nach Rot:
`1 #238b4a · 2 #569933 · 3 #8aa40e · 5 #c2a900 · 8 #ffa600 · 13 #ff7a47 · 21 #f9596f`

**Projekte** bekommen die kühleren Töne (`#31497e`, `#a14e9a`, `#006960`, `#d44c8d`, `#04565c` …), damit sie nicht mit der Ampel konkurrieren.
**Rahmen**: Kopfzeile in Navy `#003f5c`, Hauptbutton in Amber `#ffa600`.
**Schrift**: Inter (Fallback Segoe UI), Zahlen in JetBrains Mono, damit die Prio-Nummern wie auf einem Streifen wirken.

## 4. JSON dauerhaft verknüpfen (Technik)

- Über die **File System Access API** (Chrome und Edge) wird die Datei ausgewählt.
- Der Datei-Zugriff wird in der **IndexedDB** des Browsers gemerkt. Beim nächsten Start wird die Datei automatisch geladen.
- Jede Änderung wird nach 0,4 Sekunden automatisch in die Datei geschrieben.
- Je nach Browser-Einstellung fragt Chrome beim Neustart einmal nach der Erlaubnis. Dann reicht **ein Klick** auf den gelben Status oben rechts. Wenn Chrome „Bei jedem Besuch erlauben“ anbietet, entfällt auch dieser Klick.
- Zusätzlich liegt immer eine Kopie im Browser (localStorage). Für Firefox gibt es Export und Import als Fallback.
- Tipp: Die JSON kann in einem OneDrive- oder Teams-Ordner liegen. Dann ist sie automatisch gesichert.

**Datenmodell**

```json
{
  "app": "Priorisierer3000",
  "version": 1,
  "settings": { "capacity": 20 },
  "projects": [ { "id": "p1", "name": "Tagesgeschäft", "color": "#31497e" } ],
  "tasks": [
    { "id": "a1b2c3", "title": "Budgetplanung abgeben", "note": "Zahlen fehlen noch",
      "project": "p1", "urgency": "red", "points": 8 }
  ],
  "updated": "2026-11-08T10:00:00.000Z"
}
```

Die Reihenfolge im Array `tasks` ist die Priorität.

## 5. Was der Prototyp v0.1 schon kann

- Flugstreifen mit Ampel, Story Points, Notiz, Projekt
- Drag & Drop am Griff oder an der Prio-Nummer, alternativ `Alt + ↑/↓`
- Projekt-Tabs oben mit Anzahl und Summe der Story Points, „Alle Projekte“ zeigt die Gesamtliste
- Sortieren innerhalb eines Projekts ändert die Gesamtreihenfolge sinnvoll mit
- **Kapazitätsgrenze**: gestrichelte Linie nach den Aufgaben, die in deine Wochenkapazität passen
- **Lagebild** rechts: „Jetzt dran“, Kapazität, Ampel-Lage mit Warnungen, Projektverteilung
- JSON verknüpfen, neu anlegen, lösen, exportieren, importieren

## 6. Iterationsplan

1. **Mockup bewerten** (jetzt): Farben, Dichte, Spalten, Schrift. Was fehlt, was stört?
2. **Projekte verwalten**: Farbe wählen, löschen, archivieren, Reihenfolge der Tabs
3. **Erledigt-Ablage**: Streifen abhaken, wandern in ein Archiv mit Datum
4. **Fälligkeitsdatum** und optional „Wartet auf wen?“
5. **Priorisierungshilfen**
   - Zweite Achse **Wert / Impact** (ebenfalls Fibonacci)
   - Vorschlag nach **WSJF** (Wert + Dringlichkeit geteilt durch Aufwand) als Knopf „Vorschlag anzeigen“, du entscheidest final per Drag & Drop
   - Optional eine Eisenhower-Ansicht als zweite Darstellung
6. **WIP-Limit**: maximal 3 Streifen gleichzeitig „in Arbeit“
7. Feinschliff: Dunkelmodus, Druckansicht für das Wochen-Meeting, Suche

## 7. Empfehlungen aus Sicht Priorisierung

- **Die Reihenfolge ist die Priorität, nicht die Farbe.** Die Ampel sagt, wie dringend etwas ist. Die Position sagt, was du als Nächstes tust. Der Prototyp warnt, wenn beides nicht zusammenpasst.
- **Story Points messen Aufwand, nicht Wichtigkeit.** Wenn du Punkte als Wichtigkeit verwenden willst, sollten wir das klar trennen (siehe Wert / Impact oben).
- **Maximal 2 bis 3 rote Streifen.** Wenn alles dringend ist, ist nichts dringend. Ab 30 % Rot gibt es einen Hinweis.
- **Neue Aufgaben starten unten.** Sie müssen sich ihren Platz verdienen. Das schützt dich vor dem Reflex, alles Neue sofort zu machen.
- **Kapazität ehrlich setzen.** Alles unter der gestrichelten Linie ist eine bewusste Entscheidung für „nicht diese Woche“.
