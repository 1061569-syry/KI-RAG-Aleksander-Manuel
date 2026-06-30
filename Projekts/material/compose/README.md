# Compose-Dateien – welche wofür?

| Datei | Wann verwenden |
|-------|----------------|
| `docker-compose.yml` | **Hauptvariante.** Ollama lokal auf dem PC, WebUI im Container. Schnellste lokale Variante. |
| `docker-compose-alles-im-container.yml` | Alternative, falls die lokale Ollama-Installation Probleme macht. Etwas langsamer. |
| `docker-compose-cloud.yml` | **Tag 3.** Kein lokales Modell, stattdessen Cloud-LLM (Groq). API-Key eintragen! |

## Starten / Stoppen

```bash
docker compose up -d        # Standard-Datei (docker-compose.yml)
docker compose down

# bestimmte Datei nutzen:
docker compose -f docker-compose-cloud.yml up -d
```

## Wichtig
- **Keine API-Keys** in ein öffentliches Repo hochladen.
- Bei Verbindungsproblemen: siehe `../../docs/05_troubleshooting.md`.
