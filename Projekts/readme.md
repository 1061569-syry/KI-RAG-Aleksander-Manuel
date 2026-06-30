# Projektauftrag: Baut euren eigenen KI-Assistenten

**Bildungsgang:** Informationstechnische Assistenten (ITA), 12. Jahrgang
**Team:** 2er-Gruppe
**Dauer:** 2 Projekttage à 8 Schulstunden

---

## Eure Aufgabe

Ihr baut einen KI-Assistenten, der Fachfragen zu **einem** IT-Themengebiet
beantwortet – und zwar auf Basis von **Wissensdokumenten, die ihr selbst
schreibt**. Die Technik dahinter heißt **RAG** (Retrieval Augmented Generation):
Ihr kombiniert ein Sprachmodell mit euren eigenen Unterlagen, damit es fachlich
korrekt antwortet statt zu raten.

Am Ende soll euer System zeigen können: *Dieselbe Frage* beantwortet die KI
**ohne** eure Dokumente schlecht (oder falsch) – und **mit** euren Dokumenten
deutlich besser. Genau diesen Unterschied führt ihr beim Abnahmegespräch vor.

---

## Eure Domäne

Jede Gruppe übernimmt eines dieser Gebiete (Zuteilung durch die Lehrkraft):

| Domäne | Mögliche Inhalte eurer Wissensbasis |
|--------|-------------------------------------|
| **Cisco** | VLAN, Routing, Security, Troubleshooting |
| **C#** | Syntax, OOP, häufige Fehler, LINQ |
| **Datenbanken** | SQL-Befehle, Joins, Normalisierung |
| **Linux** | Shell-Befehle, Dateirechte, Paketverwaltung |

**Unsere Domäne:** ____________________________________________

---

## Was ihr abgebt

1. Ein **lauffähiges RAG-System** (lokale KI mit eurer Wissensbasis)
2. Ein **GitHub-Repository** mit eurer kompletten Dokumentation
3. Eine **Live-Demo** im Abnahmegespräch (Vorher/Nachher)

Eure Arbeitsschritte sind in den Arbeitsblättern **AB1–AB6** beschrieben.

---

## Zeitrahmen & Meilensteine

Die Meilensteine sind eure Orientierung: Wenn ihr am Zeitanker den jeweiligen
Punkt erreicht habt, seid ihr gut im Plan.

### Tag 1 – Aufbau & RAG-Kern

> **Meilenstein 1 – Die KI läuft** · *bis ca. Ende Stunde 3*
> Docker, Ollama und Open WebUI sind eingerichtet, `gemma3:1b` antwortet euch
> im Browser. Ihr habt die KI einmal bewusst zum Halluzinieren gebracht. → AB1, AB2

> **Meilenstein 2 – „Vorher" dokumentiert** · *bis ca. Ende Stunde 5*
> Gruppe & Domäne stehen, GitHub-Repo ist angelegt. Ihr habt **5 Fachfragen**
> an die Ki gestellt – **ohne** Wissensbasis – und die Fehler protokolliert. → AB3 Teil B

> **Meilenstein 3 – Wissensbasis + „Nachher"** · *bis Ende Tag 1*
> Eure selbst geschriebenen Wissensdokumente sind hochgeladen und dem Modell
> zugeordnet. Ihr habt **dieselben 5 Fragen erneut** gestellt und den
> Unterschied festgehalten. → AB3 Teil C + D

### Tag 2 – Verbessern, Grenzen & Abnahme

> **Meilenstein 4 – Verbessert & getestet** · *bis ca. Ende Stunde 4*
> Ihr habt eure Wissensbasis gezielt verbessert und das „KI kaputt
> machen"-Experiment (falsche Info einbauen) durchgeführt und dokumentiert. → AB3 Teil E, AB4

> **Meilenstein 5 – Abgabereif** · *bis ca. Ende Stunde 6*
> Euer Repo ist vollständig (README, Wissensbasis, Doku, Screenshots). Die
> Vorher/Nachher-Demo läuft auf eurem Laptop. → AB6
> *Schnell fertig? Dann ran an die optionale Zusatzaufgabe AB5 (Cloud-LLM).*

> **Meilenstein 6 – Abnahmegespräch** · *Stunde 7–8*
> Die Lehrkraft kommt zu euch an den Arbeitsplatz. Ihr zeigt euer Ergebnis und
> beantwortet 2–3 Fachfragen. **Beide** im Team müssen sprechen können.

---

## Wie ihr bewertet werdet

| Was | Gewicht |
|-----|---------|
| **Abnahmegespräch** – Demo + Fachfragen (beide reden!) | 50 % |
| **Dokumentation** im GitHub-Repo | 50 % |

Die optionale Cloud-Aufgabe (AB5) zählt als **Bonus** – sie kann eure Note
verbessern, aber ihr Fehlen schadet nicht.

---

## Spielregeln & Tipps

- **Dokumentiert von Anfang an**, nicht erst am Schluss. Jeder gelöste Fehler
  gehört ins Repo – das ist Teil eurer Leistung und hilft euch beim Gespräch.
- **Keine API-Keys oder Passwörter** ins Repository hochladen.
- **Eure Wissensbasis ist der Hebel:** Je besser und klarer eure Dokumente,
  desto besser die KI. Müll rein = Müll raus.
- **Bei Technikproblemen** zuerst in `docs/05_troubleshooting.md` schauen – die
  häufigsten Stolperfallen (Verbindung WebUI↔Ollama, Firewall) stehen dort.
- **Arbeitet als Team:** Teilt euch auf, aber sorgt dafür, dass **beide** alles
  erklären können. Im Abnahmegespräch werden beide gefragt.

---

**Viel Erfolg – ihr baut hier in zwei Tagen etwas, das vor Kurzem noch nach
Zukunftsmusik klang.**
