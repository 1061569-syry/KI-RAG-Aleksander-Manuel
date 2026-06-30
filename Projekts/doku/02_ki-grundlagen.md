# KI-Grundlagen: Wie funktioniert ein Sprachmodell?

> Dieses Dokument ist die fachliche Grundlage für Arbeitsblatt 1. Es erklärt
> die wichtigsten Konzepte so, dass sie ohne Mathematik-Vorwissen verständlich
> sind.

---

## 1. Was ist ein LLM?

**LLM** steht für **Large Language Model** (großes Sprachmodell). Es ist ein
Programm, das gelernt hat, Sprache fortzusetzen. Das Modell wurde mit
riesigen Mengen Text trainiert (Bücher, Webseiten, Code).

Der Kern ist überraschend simpel:

> **Ein LLM sagt immer nur das nächste Wort (genauer: das nächste Token)
> voraus.**

Aus „Die Hauptstadt von Frankreich ist …" berechnet das Modell, welches Wort
als nächstes am wahrscheinlichsten kommt – und das ist „Paris".

---

## 2. Tokens – die Bausteine

Ein LLM denkt nicht in Buchstaben oder ganzen Wörtern, sondern in **Tokens**.
Ein Token ist ein Wortstück. Faustregel:

- 1 Token ≈ 4 Zeichen ≈ ¾ eines englischen Wortes
- Das Wort „Konfiguration" besteht aus mehreren Tokens
- 100 Tokens ≈ 75 Wörter

Warum ist das wichtig? Modelle haben ein **Token-Limit** (Kontextfenster).
Passt nicht alles hinein, „vergisst" das Modell den Anfang. Bei RAG und bei
Cloud-APIs (Tag 3) wird das später konkret relevant.

---

## 3. Wahrscheinlichkeiten statt Wissen

Das Modell „weiß" nichts im menschlichen Sinn. Es rechnet **Wahrscheinlichkeiten**
aus. Für den Satzanfang „Der Switch hat einen …" könnten die nächsten Tokens so
aussehen:

| möglicher nächster Token | Wahrscheinlichkeit |
|--------------------------|--------------------|
| Port                     | 41 % |
| Fehler                   | 22 % |
| Anschluss                | 15 % |
| Konfigurationsfehler     | 9 % |
| Tisch                    | 0,1 % |

Das Modell wählt dann (meist) einen der wahrscheinlichen Tokens aus. Genau
deshalb können Antworten auch **plausibel klingen, aber falsch sein** – das
nennt man **Halluzination**. Das Modell erfindet eine wahrscheinliche, aber
nicht zwingend wahre Fortsetzung.

---

## 4. Nicht-deterministisch

**Deterministisch** heißt: Gleiche Eingabe → immer gleiche Ausgabe (wie eine
Formel). LLMs sind in der Regel **nicht-deterministisch**: Dieselbe Frage kann
unterschiedliche Antworten liefern, weil das nächste Token zufällig aus den
wahrscheinlichen Kandidaten gezogen wird.

Das ist ein wichtiger Unterschied zu klassischen Programmen, die die Schüler
kennen (z. B. eine C#-Methode liefert bei gleicher Eingabe immer dasselbe).

---

## 5. Wichtige Kenngrößen / Stellschrauben

| Kenngröße | Was sie bedeutet | Wirkung |
|-----------|------------------|---------|
| **Temperatur** | Wie „mutig" das Modell wählt | Niedrig (0–0.3) = sachlich, vorhersehbar. Hoch (0.8–1.5) = kreativ, sprunghaft |
| **Kontextfenster** | Wie viele Tokens ins „Gedächtnis" passen | Größer = mehr Text berücksichtigbar |
| **Parameter (z. B. 1b, 4b)** | Größe/Komplexität des Modells | Mehr Parameter = oft klüger, aber langsamer |
| **Top-p / Top-k** | Begrenzen die Auswahl der Kandidaten-Tokens | Beeinflussen Vielfalt der Antwort |

**Modellgrößen im Projekt:**
- `gemma3:1b` → ~1 Milliarde Parameter, klein & schnell, macht mehr Fehler
- `gemma3:4b` → ~4 Milliarden Parameter, besser, aber ohne GPU sehr langsam

---

## 6. Warum brauchen wir dann RAG?

Ein LLM kennt nur, was beim Training dabei war – und kann Dinge erfinden. Wenn
wir wollen, dass es **fachlich korrekt** zu *unserem* Thema antwortet, geben wir
ihm eigene, geprüfte Dokumente mit. Genau das ist **RAG** – erklärt in
`04_rag-erklaert.md`.

---

## Begriffsglossar (kurz)

- **LLM:** großes Sprachmodell, sagt das nächste Token voraus
- **Token:** Wortstück, kleinste Verarbeitungseinheit
- **Halluzination:** plausibel klingende, aber falsche Antwort
- **deterministisch / nicht-deterministisch:** gleiche Eingabe immer/nicht immer gleiche Ausgabe
- **Temperatur:** Stellschraube für Zufall/Kreativität
- **Kontextfenster:** maximale Token-Menge im „Gedächtnis"
- **RAG:** Kombination aus Sprachmodell + eigenen Dokumenten
