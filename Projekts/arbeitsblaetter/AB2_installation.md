# Arbeitsblatt 2 – Installation der lokalen KI-Umgebung

**Gruppe:** ____________________  **Domäne:** ____________________

> **Ziel:** Ihr habt Docker, Ollama und Open WebUI eingerichtet und das Modell
> `gemma3:1b` läuft.
> **Hintergrund:** `docs/03_installation.md` · Bei Fehlern: `docs/05_troubleshooting.md`

---

## Architektur – was läuft wo?

Trage ein, wo welche Komponente läuft (im Container / direkt auf dem PC):

| Komponente | läuft … | Port |
|------------|---------|------|
| Open WebUI | __________________ | ______ |
| Ollama | __________________ | ______ |
| gemma3:1b | (im Modell-Speicher von Ollama) | – |

---

## Checkliste Installation

Hake ab, sobald ein Schritt erledigt und geprüft ist.

- [ ] **Docker Desktop** läuft (`docker --version` zeigt eine Version)
- [ ] **Ollama installiert** (`ollama --version`)
- [ ] **Umgebungsvariable** `OLLAMA_HOST = 0.0.0.0` gesetzt
- [ ] **Modell geladen** (`ollama pull gemma3:1b`)
- [ ] **Compose-Datei** im Projektordner
- [ ] **Container gestartet** (`docker compose up -d`)
- [ ] **WebUI erreichbar** unter `http://localhost:3000`
- [ ] **Account angelegt** (lokal)
- [ ] **Modell `gemma3:1b`** in der Auswahl sichtbar
- [ ] **Erste Antwort** erhalten

---

## Prüf-Befehle (Ergebnis notieren)

**Ollama läuft?**
```bash
curl http://localhost:11434
```
Ausgabe: ____________________________________________

**Welche Modelle sind installiert?**
```bash
curl http://localhost:11434/api/tags
```
Gefundene Modelle: ___________________________________

---

## Fehler-Protokoll

Notiert **jedes** Problem und wie ihr es gelöst habt – das ist später Teil eurer
Dokumentation und hilft anderen Gruppen!

| Problem | Lösung | gelöst? |
|---------|--------|---------|
| | | ☐ |
| | | ☐ |
| | | ☐ |

> **Tipp:** Die drei häufigsten Fehler sind: (1) WebUI findet kein Modell →
> `host.docker.internal` statt `localhost`; (2) `OLLAMA_HOST` nicht gesetzt;
> (3) Firewall blockiert Port 11434. Alle Lösungen in `docs/05_troubleshooting.md`.

---

✅ **Geschafft, wenn:** Das Modell `gemma3:1b` in Open WebUI antwortet und euer
Fehler-Protokoll ausgefüllt ist.
