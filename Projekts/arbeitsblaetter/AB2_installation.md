# Arbeitsblatt 2 – Installation der lokalen KI-Umgebung

**Gruppe:** Gruppe 13  **Domäne:** Datenbanken

> **Ziel:** Ihr habt Docker, Ollama und Open WebUI eingerichtet und das Modell
> `gemma3:1b` läuft.
> **Hintergrund:** `docs/03_installation.md` · Bei Fehlern: `docs/05_troubleshooting.md`

---

## Architektur – was läuft wo?

Trage ein, wo welche Komponente läuft (im Container / direkt auf dem PC):

| Komponente | läuft … | Port |
|------------|---------|------|
| Open WebUI | (im Container von Docker) | 3000 |
| Ollama | (direkt auf PC)| 11434 |
| gemma3:1b | (im Modell-Speicher von Ollama) | 8080 |

---

## Checkliste Installation

Hake ab, sobald ein Schritt erledigt und geprüft ist.

- [X] **Docker Desktop** läuft (`docker --version` zeigt eine Version)
- [X] **Ollama installiert** (`ollama --version`)
- [X] **Umgebungsvariable** `OLLAMA_HOST = 0.0.0.0` gesetzt
- [X] **Modell geladen** (`ollama pull gemma3:1b`)
- [X] **Compose-Datei** im Projektordner
- [X] **Container gestartet** (`docker compose up -d`)
- [X] **WebUI erreichbar** unter `http://localhost:3000`
- [X] **Account angelegt** (lokal)
- [X] **Modell `gemma3:1b`** in der Auswahl sichtbar
- [X] **Erste Antwort** erhalten

---

## Prüf-Befehle (Ergebnis notieren)

**Ollama läuft?**
```bash
curl http://localhost:11434
```
Ausgabe: "Ollama is running"

**Welche Modelle sind installiert?**
```bash
curl http://localhost:11434/api/tags
```
Gefundene Modelle: "{"models":[{"name":"gemma3:1b","model":"gemma3:1b","modified_at":"2026-06-23T10:00:15.7672409+02:00","size":815319791,"digest":"8648f39daa8fbf5b18c7b4e6a8fb4990c692751d49917417b8842ca5758e7ffc","details":{"parent_model":"","format":"gguf","family":"gemma3","families":["gemma3"],"parameter_size":"999.89M","quantization_level":"Q4_K_M"},"capabilities":["completion"]}]}"

---

## Fehler-Protokoll

Notiert **jedes** Problem und wie ihr es gelöst habt – das ist später Teil eurer
Dokumentation und hilft anderen Gruppen!

| Problem | Lösung | gelöst? |
|---------|--------|---------|
| Diese App kann auf dem PC nicht ausgeführt werden (Docker) | Falsche Docker Seite genutzt |[X]|

> **Tipp:** Die drei häufigsten Fehler sind: (1) WebUI findet kein Modell →
> `host.docker.internal` statt `localhost`; (2) `OLLAMA_HOST` nicht gesetzt;
> (3) Firewall blockiert Port 11434. Alle Lösungen in `docs/05_troubleshooting.md`.

---

✅ **Geschafft, wenn:** Das Modell `gemma3:1b` in Open WebUI antwortet und euer
Fehler-Protokoll ausgefüllt ist.
