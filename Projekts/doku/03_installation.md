# Installationsanleitung: Docker, Ollama & Open WebUI

> Diese Anleitung gehört zu Arbeitsblatt 2. Sie beschreibt die komplette
> Einrichtung der lokalen KI-Umgebung. Bei Problemen: siehe
> `05_troubleshooting.md`.

---

## Überblick der Architektur

```
   Browser (du)
        │  http://localhost:3000
        ▼
   Open WebUI   ←  läuft im Docker-Container
        │  http://host.docker.internal:11434
        ▼
   Ollama       ←  läuft direkt auf dem PC (nicht im Container)
        │
        ▼
   gemma3:1b    ←  das kleine Sprachmodell
```

**Warum diese Aufteilung?** Ollama läuft direkt auf dem PC am schnellsten.
Open WebUI im Container ist sauber gekapselt und leicht zu starten/stoppen.

---

## Vorbereitung (durch die Lehrkraft, vor Tag 1)

Der Modell-Download (`gemma3:1b` ≈ 0,8 GB) und das Open-WebUI-Image (~1 GB)
sollten nicht von 15 Laptops gleichzeitig aus dem Schulnetz gezogen werden.

**Optionen:**
- Modell einmal laden und Volume per USB verteilen, **oder**
- Downloads zeitlich staffeln (gruppenweise), **oder**
- Wenn das Netz stark genug ist: alle gleichzeitig (Puffer einplanen).

---

## Schritt 1 – Docker Desktop prüfen

Docker Desktop muss installiert sein und laufen (Wal-Symbol in der Taskleiste).
Test im Terminal:

```bash
docker --version
docker compose version
```

---

## Schritt 2 – Ollama installieren

**Windows:**
```powershell
winget install Ollama.Ollama
```
Alternativ von <https://ollama.com/download> herunterladen.

**Dauerhaft die richtige Host-Einstellung setzen** (wichtig, damit Docker
später auf Ollama zugreifen kann):

```
Systemsteuerung → System → Erweiterte Systemeinstellungen
  → Umgebungsvariablen → Neu (Benutzervariablen)
Variable: OLLAMA_HOST
Wert:     0.0.0.0
```

Danach Ollama (neu) starten.

---

## Schritt 3 – Modell laden

```bash
ollama pull gemma3:1b
```

Test:
```bash
ollama run gemma3:1b "Sage Hallo auf Deutsch"
```

---

## Schritt 4 – Projektordner & Compose-Datei

Lege einen Ordner an, z. B. `C:\Schule\ki-projekt\`, und kopiere die Datei
`docker-compose.yml` (aus `material/compose/`) hinein.

```bash
cd C:\Schule\ki-projekt
docker compose up -d
```

Beim ersten Start wird das Open-WebUI-Image geladen.

---

## Schritt 5 – Open WebUI öffnen

Im Browser:
```
http://localhost:3000
```

Beim ersten Aufruf einen **lokalen Account** anlegen (Name, E-Mail, Passwort –
bleibt nur auf dem eigenen PC, kein Internet nötig).

---

## Schritt 6 – Modell auswählen & testen

Oben im Chat `gemma3:1b` auswählen und eine erste Frage stellen.
Antwortet das Modell? **Glückwunsch – die lokale KI läuft.**

---

## Start/Stop im Alltag

```bash
# starten
docker compose up -d

# stoppen
docker compose down

# Logs ansehen (bei Problemen)
docker compose logs -f
```

Ollama läuft separat. Falls `OLLAMA_HOST` dauerhaft gesetzt ist, genügt ein
normaler Ollama-Start; sonst:

```powershell
$env:OLLAMA_HOST = "0.0.0.0"
ollama serve
```

---

## Schnelltest: Ist Ollama für Docker erreichbar?

```bash
# sollte "Ollama is running" zeigen
curl http://localhost:11434

# zeigt installierte Modelle
curl http://localhost:11434/api/tags
```

Klappt das nicht → `05_troubleshooting.md`, Abschnitt „Docker erreicht Ollama nicht".
