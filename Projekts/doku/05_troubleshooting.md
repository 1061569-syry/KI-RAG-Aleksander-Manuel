# Troubleshooting: Häufige Probleme & Lösungen

> Diese Sammlung deckt die Fehler ab, die in diesem Projekt erfahrungsgemäß am
> häufigsten auftreten. Erst hier nachsehen, bevor man lange selbst sucht.

---

## 1. Docker-Container startet nicht

**Symptom:** `docker compose up -d` bricht ab oder Container ist sofort wieder „Exited".

**Prüfen / Lösen:**
- Läuft Docker Desktop? (Wal-Symbol in der Taskleiste)
- Logs ansehen: `docker compose logs -f`
- Port 3000 schon belegt? Anderen Port nutzen, z. B. `3001:8080` in der Compose-Datei.

---

## 2. Open WebUI lädt, aber kein Modell sichtbar

**Symptom:** WebUI öffnet sich, aber die Modellauswahl ist leer.

**Ursache:** WebUI (im Container) erreicht Ollama (auf dem PC) nicht.

**Lösung – die wichtigste Fehlerquelle im ganzen Projekt:**

`localhost` bedeutet **innerhalb des Containers** den Container selbst – nicht
deinen PC. WebUI muss den PC über einen Sonder-Namen ansprechen:

```
http://host.docker.internal:11434      (Windows / Mac)
http://172.17.0.1:11434                (Linux)
```

Das ist in den mitgelieferten Compose-Dateien bereits eingestellt
(`OLLAMA_BASE_URL`). Falls trotzdem leer:

In der WebUI prüfen: `Admin Panel → Settings → Connections → Ollama API`
→ dort muss `http://host.docker.internal:11434` stehen, **nicht** `localhost`.

---

## 3. Docker erreicht Ollama nicht (trotz richtiger URL)

**Ursache A – Ollama hört nur auf localhost:**
Ollama bindet sich standardmäßig nur an `127.0.0.1`. Docker kommt dann nicht ran.

```powershell
# vorübergehend:
$env:OLLAMA_HOST = "0.0.0.0"
ollama serve
```
Dauerhaft als Umgebungsvariable setzen (siehe `03_installation.md`, Schritt 2).

**Ursache B – Windows-Firewall blockiert Port 11434:**
Einmalig in einer **Administrator-Powershell**:

```powershell
New-NetFirewallRule -DisplayName "Ollama Docker" -Direction Inbound `
  -Protocol TCP -LocalPort 11434 -Action Allow
```

**Test, ob es klappt:**
```bash
docker run --rm curlimages/curl curl http://host.docker.internal:11434
# Erwartet: "Ollama is running"
```

---

## 4. Antworten dauern extrem lange (Minuten)

**Ursache:** Das Modell läuft auf der CPU; ohne dedizierte GPU ist das langsam.
`gemma3:4b` kann auf Office-Laptops mehrere Minuten pro Antwort brauchen.

**Lösungen:**
- Kleineres Modell verwenden: **`gemma3:1b`** (Projektstandard) oder
  `qwen2.5:1.5b`.
- Andere Programme schließen (RAM/CPU freigeben).
- Für Tag 3: auf Cloud-LLM (Groq) umsteigen – siehe AB5.

---

## 5. Cloud-LLM: „Request Entity Too Large"

**Symptom (bei Groq u. ä.):**
> Es ist ein Problem mit der Antwort aufgetreten. Request Entity Too Large

**Ursache:** Mit RAG schickt WebUI System-Prompt + viele Dokument-Chunks +
Verlauf mit. Das überschreitet das **Input-Token-Limit** kleiner Modelle.

**Lösungen (eine oder mehrere kombinieren):**

1. **Modell mit großem Kontext wählen.** Bei Groq:
   - `llama-3.1-8b-instant` → 128.000 Token ✅ (empfohlen)
   - `gemma2-9b-it` → nur 8.192 Token ❌ oft zu klein

2. **Chunk-Einstellungen verkleinern:**
   `Admin Panel → Settings → Documents`

   | Einstellung | Standard | Empfehlung |
   |-------------|----------|------------|
   | Chunk Size | 1500 | 500 |
   | Chunk Overlap | 100 | 50 |
   | Top K | 5 | 3 |

3. **Dokumente kürzen / kompakter schreiben.**

---

## 6. SSH/Modell-Antworten auf Englisch statt Deutsch

**Ursache:** System-Prompt fehlt oder ist zu schwach.

**Lösung:** Im Modell einen klaren System-Prompt setzen, der „Antworte immer auf
Deutsch" enthält (siehe Vorlage in `material/wissensbasis-vorlagen/`).

---

## 7. Änderungen an Dokumenten wirken nicht

**Ursache:** Geänderte Dokumente müssen neu indiziert werden.

**Lösung:** Dokument in der Knowledge-Base entfernen und neu hochladen, dann
prüfen, ob es dem Modell weiterhin zugeordnet ist.

---

## Schnell-Checkliste bei „geht nicht"

1. Läuft Docker Desktop?
2. Läuft Ollama? (`curl http://localhost:11434`)
3. Ist `OLLAMA_HOST=0.0.0.0` gesetzt?
4. Firewall-Regel für Port 11434 vorhanden?
5. Steht in WebUI `host.docker.internal` statt `localhost`?
6. Bei Cloud: Modell mit großem Kontext gewählt? Chunks verkleinert?
