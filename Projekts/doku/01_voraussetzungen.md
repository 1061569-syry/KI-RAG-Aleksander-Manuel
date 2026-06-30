# Vorab-Checkliste: Was muss vor Tag 1 installiert sein?

> Diese Liste **vor Projektbeginn** abarbeiten – am besten in der Stunde davor
> oder als Hausaufgabe. Wenn alles hier abgehakt ist, verliert ihr an Tag 1
> keine Zeit mit Installation.

---

## 1. Pflicht-Software

### ☐ Docker Desktop
Das Kernstück – darin läuft Open WebUI. Auf Windows mit WSL2-Backend.
Installation braucht **Admin-Rechte**. Nach der Installation einmal starten
(Wal-Symbol in der Taskleiste muss laufen).

Prüfen:
```bash
docker --version
docker compose version
```

### ☐ Ollama + Modell `gemma3:1b`
Die lokale KI auf eurem PC.

1. Ollama installieren (Windows: `winget install Ollama.Ollama` oder von
   <https://ollama.com/download>).
2. **Systemvariable setzen** (wichtig, sonst erreicht Docker Ollama später nicht):
   `OLLAMA_HOST = 0.0.0.0`
   (Systemsteuerung → System → Erweiterte Systemeinstellungen →
   Umgebungsvariablen → Neu)
3. Modell laden:
   ```bash
   ollama pull gemma3:1b
   ```

Prüfen:
```bash
ollama --version
ollama list          # gemma3:1b muss auftauchen
```

### ☐ Git / GitHub Desktop
Für die Projektdokumentation. GitHub Desktop ist am einfachsten
(<https://desktop.github.com>); die git-Kommandozeile geht auch.

Prüfen:
```bash
git --version
```

### ☐ Markdown-Editor (VS Code empfohlen)
Zum Schreiben der Wissensbasis-Dateien (`.md`).
**VS Code** (<https://code.visualstudio.com>) ist leicht und hat eine
Markdown-Vorschau. Das große Visual Studio aus dem C#-Unterricht geht zwar auch,
ist hier aber überdimensioniert und nicht nötig.

### ☐ Aktueller Browser
Chrome, Edge oder Firefox – für den Zugriff auf Open WebUI unter
`http://localhost:3000`. Auf jedem Laptop ohnehin vorhanden.

---

## 2. Accounts (vorab anlegen)

### ☐ GitHub-Account
Für euer Projekt-Repository. Falls noch nicht vorhanden, vorab auf
<https://github.com> registrieren.

### ☐ (Optional) Groq-Account
Nur für die freiwillige Zusatzaufgabe (AB5, Cloud-LLM). Kostenloser API-Key auf
<https://console.groq.com>. Muss nicht für alle vorab da sein.

---

## 3. System-Voraussetzungen (vorab prüfen)

- ☐ **Mindestens 8 GB RAM**
- ☐ **Ca. 5 GB freier Speicher** (Modell ~0,8 GB + WebUI-Image ~1 GB + Puffer)
- ☐ **Admin-Rechte** auf dem Laptop (für Docker, Ollama und die Firewall-Regel
  für Port 11434)

---

## 4. Wird von der Lehrkraft bereitgestellt (nicht selbst installieren)

- Die vorgegebene `docker-compose.yml` (aus `material/compose/`)
- Die Arbeitsblätter AB1–AB6
- Ggf. das vorab heruntergeladene Modell per USB (falls das Schulnetz zu langsam ist)

---

## Schnell-Selbsttest (alles auf einen Blick)

Führt diese Befehle aus – jede Zeile sollte eine Version/Ausgabe liefern:

```bash
docker --version
docker compose version
ollama --version
ollama list
git --version
```

Läuft alles durch und taucht `gemma3:1b` in `ollama list` auf?
**Dann seid ihr startklar für Tag 1.**
