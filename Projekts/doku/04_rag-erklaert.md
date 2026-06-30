# RAG erklärt: Wie bekommt die KI eigenes Fachwissen?

> Grundlage für Arbeitsblatt 3. Erklärt das Prinzip hinter dem Mini-RAG.

---

## Das Grundproblem

Ein Sprachmodell kennt nur, was beim Training dabei war. Es kann:

- veraltet sein,
- dein spezielles Thema nur oberflächlich kennen,
- Dinge **erfinden** (halluzinieren), die plausibel klingen.

Für einen verlässlichen Fach-Assistenten reicht das nicht.

---

## Die Idee von RAG

**RAG** = **R**etrieval **A**ugmented **G**eneration
(auf Deutsch etwa: „durch Abruf erweiterte Erzeugung").

Statt das Modell neu zu trainieren, geben wir ihm bei jeder Frage die
**passenden Ausschnitte aus unseren eigenen Dokumenten** mit. Das Modell
formuliert die Antwort dann auf Basis dieser mitgelieferten Fakten.

Vergleich: Eine Klassenarbeit …
- **ohne RAG** = aus dem Kopf antworten (Gefahr: Erinnerungslücken, Erfindungen)
- **mit RAG** = mit erlaubtem Spickzettel antworten (die Fakten liegen vor)

---

## Wie läuft eine RAG-Anfrage ab?

```
1. Du stellst eine Frage
        │
2. System durchsucht deine Dokumente
   und findet die passenden Ausschnitte (Chunks)
        │
3. Frage + gefundene Ausschnitte gehen
   zusammen an das Sprachmodell
        │
4. Modell formuliert die Antwort
   auf Basis dieser Ausschnitte
```

---

## Wichtige Begriffe

### Chunks (Textbausteine)
Lange Dokumente werden in kleine Stücke zerteilt (z. B. je 500 Zeichen). Nur die
**relevanten** Stücke werden mitgeschickt – nicht das ganze Dokument. Das spart
Tokens und macht die Antwort präziser.

### Embeddings (Bedeutungs-Vektoren)
Damit das System „passende" Stücke findet, wird jeder Chunk in eine Zahlenreihe
umgewandelt, die seine **Bedeutung** abbildet. Texte mit ähnlicher Bedeutung
haben ähnliche Zahlenreihen. So findet das System z. B. zu „Wie sichere ich den
Fernzugriff?" den Chunk über SSH – auch wenn das Wort „Fernzugriff" dort gar
nicht steht.

### Retrieval (Abruf)
Der Schritt, in dem die am besten passenden Chunks ausgewählt werden. Die
Einstellung **Top-K** legt fest, wie viele Chunks mitgeschickt werden (z. B. 3).

---

## Wovon hängt die Qualität ab?

| Faktor | Auswirkung |
|--------|------------|
| **Qualität der Dokumente** | Müll rein → Müll raus. Korrekte, klare Docs sind alles. |
| **Struktur der Dokumente** | Überschriften & kurze Absätze verbessern das Chunking. |
| **Chunk-Größe** | Zu groß → zu viele Tokens. Zu klein → Zusammenhang geht verloren. |
| **Top-K** | Mehr Chunks = mehr Kontext, aber mehr Tokens. |
| **System-Prompt** | Gibt dem Modell Rolle und Verhalten vor. |

> **Kernbotschaft für die Schüler:** Bei RAG ist *eure* inhaltliche Arbeit an
> den Dokumenten der entscheidende Hebel – nicht das Modell.

---

## Gute Wissensdokumente schreiben (Checkliste)

- [ ] Klare Überschriften pro Thema (`##`, `###`)
- [ ] Kurze Absätze statt Textwüsten
- [ ] Befehle/Code in Codeblöcken (```)
- [ ] Pro Abschnitt ein abgeschlossener Gedanke
- [ ] Fachlich geprüft und korrekt
- [ ] Häufige Fehler / Stolpersteine explizit benennen

---

## In Open WebUI umgesetzt

1. **Dokumente hochladen:** `Workspace → Knowledge → + Create Knowledge`
2. **Wissensbasis dem Modell zuordnen:**
   `Workspace → Models → (Modell) → Knowledge`
3. **Chunk-Einstellungen** (falls nötig):
   `Admin Panel → Settings → Documents`

Details und Schritt-für-Schritt-Aufgaben stehen in Arbeitsblatt 3.
