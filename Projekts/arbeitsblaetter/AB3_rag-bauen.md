# Arbeitsblatt 3 – Mini-RAG bauen

**Gruppe:** Grupp 13  **Domäne:** Datenbanken

> **Ziel:** Ihr baut für eure Domäne eine eigene Wissensbasis und seht im
> direkten Vorher/Nachher-Vergleich, was RAG bewirkt.
> **Hintergrund:** `docs/04_rag-erklaert.md`

---

## Teil A – Verstehen, was RAG ist

**A.1** Wofür steht die Abkürzung RAG?

Retrieval Augmented Generation

**A.2** Erkläre den Vergleich „Klassenarbeit ohne / mit Spickzettel" in eigenen
Worten:

Klassenarbeit, ohne Spickzettel muss man alles auswendig können, was natürlich zu Fehlern kommen kann, aber mit Spickzettel, wenn es Lücken in Wissen gibt, dann kann man einen kleinen Blick auf das Spickzettel machen und dann wieder auf das richtige Weg gehen, KI in diesen Zusammenhang, muss normalerweise ohne Wissen Basis, selber deine Frage beantworten, was dazu führt, dass er Halluzinationen viel öfter kriegt, aber mit einer Wissen Basis, kann die KI hineingucken und viel weniger Fehler machen.

**A.3** Nenne die zwei wichtigsten Faktoren für die Qualität eines RAG-Systems:

1. 
2. _______________________________________________________________

---

## Teil B – VORHER: Modell ohne Wissensbasis

> Wichtig: Dieser Schritt passiert **bevor** ihr Dokumente hochladet.

**B.1** Überlegt euch **5 Fachfragen** zu eurer Domäne, deren korrekte Antwort
ihr kennt. Tragt sie in die Tabelle ein und stellt sie dem Modell.

| # | Frage | Antwort korrekt? (ja/teils/nein) | Was war falsch? |
|---|-------|----------------------------------|-----------------|
| 1 | Was ist ORDER BY und wie nutzt man die? | JA | Nichts 
| 2 | Wie erstellt man einen Primary Key? | JA | Nichts |
| 3 | Was ist der Unterschied zwischen INNER JOIN und LEFT JOIN? | NEIN | Erfundene Begriffe: INNER SELECT? "Verzeit für Ergebnisse", "Link zur Linksseite" |
| 4 | Was bewirkt die GROUP-BY Klausel und welche Bedingung nutzt man danach statt WHERE? | | |
| 5 | Was ist der Unterschied zwischen den Datentypen CHAR und VARCHAR? | | |

**B.2** Wie viele der 5 Antworten waren vollständig korrekt? ______ / 5

---

## Teil C – Wissensbasis erstellen

**C.1** Erstellt pro Thema eine Markdown-Datei (`.md`). Nutzt die Vorlage aus
`material/wissensbasis-vorlagen/` für eure Domäne als Startpunkt.

Achtet auf gute Struktur (siehe Checkliste in `docs/04_rag-erklaert.md`):
- klare Überschriften
- kurze Absätze
- Befehle/Code in Codeblöcken
- häufige Fehler benennen

**C.2** Welche Dateien habt ihr erstellt?

| Dateiname | Inhalt (Stichworte) |
|-----------|---------------------|
| | |
| | |
| | |

**C.3 System-Prompt setzen.** Legt in Open WebUI ein eigenes Modell an:
`Workspace → Models → + Create Model`, basierend auf `gemma3:1b`, mit einem
System-Prompt, der die Rolle festlegt (Vorlage in den Wissensbasis-Vorlagen).

Euer System-Prompt (Kurzfassung notieren):

_________________________________________________________________

---

## Teil D – NACHHER: Modell mit Wissensbasis

**D.1** Ladet eure Dokumente hoch
(`Workspace → Knowledge → + Create Knowledge`) und ordnet sie eurem Modell zu
(`Workspace → Models → (euer Modell) → Knowledge`).

**D.2** Stellt **dieselben 5 Fragen** aus Teil B erneut.

| # | Antwort jetzt korrekt? (ja/teils/nein) | Besser als vorher? |
|---|----------------------------------------|--------------------|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |
| 5 | | |

**D.3** Wie viele sind **jetzt** korrekt? ______ / 5  (vorher: ______ / 5)

**D.4** Beschreibt den deutlichsten Unterschied, den ihr beobachtet habt:

_________________________________________________________________

_________________________________________________________________

---

## Teil E – Verbessern

**E.1** Wählt eine Frage, die noch nicht gut beantwortet wird. Verbessert das
zugehörige Dokument (mehr Details, klarere Struktur). Lade es neu hoch und teste
erneut. Was hat sich geändert?

_________________________________________________________________

---

✅ **Geschafft, wenn:** Ihr den Vorher/Nachher-Vergleich vollständig ausgefüllt
habt und eure Wissensbasis im RAG aktiv ist.
