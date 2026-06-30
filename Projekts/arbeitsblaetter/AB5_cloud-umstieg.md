# Arbeitsblatt 5 – Umstieg auf ein externes (Cloud-)LLM  ⭐ OPTIONAL

**Gruppe:** ____________________  **Domäne:** ____________________

> **⭐ Zusatzaufgabe für schnelle Gruppen.** Nur bearbeiten, wenn euer RAG-System
> läuft, getestet und dokumentiert ist (AB1–AB4 fertig).
>
> **Ziel:** Ihr bindet ein schnelles Cloud-LLM (z. B. Groq) an, vergleicht es mit
> dem lokalen Modell und bewertet Vor- und Nachteile – auch beim Datenschutz.
> **Hintergrund:** `docs/05_troubleshooting.md` (Abschnitt 5)

---

## Teil A – Warum überhaupt umsteigen?

**A.1** Wie lange dauert eine typische Antwort mit dem lokalen `gemma3:1b`?

ca. ______ Sekunden

**A.2** Was ist der vermutete Grund für die Geschwindigkeit lokaler Modelle ohne
Grafikkarte?

_________________________________________________________________

---

## Teil B – Cloud-LLM anbinden

> Den API-Key stellt die Lehrkraft bereit (oder ihr legt selbst einen
> kostenlosen Groq-Account an: console.groq.com).

**B.1** Tragt den externen Anbieter in Open WebUI ein:
`Admin Panel → Settings → Connections → OpenAI API`

- Base URL: `https://api.groq.com/openai/v1`
- API-Key: (von der Lehrkraft)

**B.2** Wählt ein Modell mit großem Kontextfenster:
`llama-3.1-8b-instant` (128k Token).

**B.3** Stellt eine eurer Domänen-Fragen. Antwortzeit jetzt?

ca. ______ Sekunden  (lokal war: ______ Sekunden)

---

## Teil C – Das „Request Entity Too Large"-Problem

Viele Gruppen stoßen jetzt auf diese Fehlermeldung.

**C.1** Was bedeutet sie? (Tipp: Token-Limit + RAG-Kontext)

_________________________________________________________________

**C.2** Welche Lösung habt ihr angewandt? (mehrere möglich)

- [ ] Modell mit größerem Kontext gewählt
- [ ] Chunk Size reduziert (auf ______)
- [ ] Top-K reduziert (auf ______)
- [ ] Dokumente gekürzt

**C.3** Hat es funktioniert? ☐ ja ☐ nein – Beobachtung:

_________________________________________________________________

---

## Teil D – Vergleich & Bewertung

Füllt die Vergleichstabelle aus (eigene Einschätzung):

| Kriterium | Lokal (gemma3:1b) | Cloud (Groq) |
|-----------|-------------------|--------------|
| Geschwindigkeit | | |
| Antwortqualität | | |
| Datenschutz | | |
| Internet nötig? | | |
| Kosten | | |

---

## Teil E – Datenschutz-Reflexion (wichtig!)

**E.1** Beim Cloud-LLM verlassen eure Eingaben den eigenen Rechner. Wohin gehen
die Daten ungefähr, und warum ist das relevant?

_________________________________________________________________

**E.2** Nennt ein Beispiel aus dem IT-Berufsalltag, bei dem man **auf keinen
Fall** ein Cloud-LLM nutzen sollte:

_________________________________________________________________

**E.3** Wann ist umgekehrt ein lokales Modell die bessere Wahl, obwohl es
langsamer ist?

_________________________________________________________________

---

✅ **Geschafft, wenn:** Das Cloud-LLM antwortet, das „Too Large"-Problem gelöst
ist und eure Vergleichstabelle + Datenschutz-Reflexion ausgefüllt sind.
