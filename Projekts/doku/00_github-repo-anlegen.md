# Arbeitsblatt 0 – Git-Repository anlegen (mit GitHub Desktop)

**Gruppe:** ____________________  **Domäne:** ____________________

> **Wann?** Tag 1, sobald Gruppe und Domäne feststehen.
> **Ziel:** Ihr habt ein gemeinsames GitHub-Repository mit der richtigen
> Ordnerstruktur, in das ihr ab jetzt **fortlaufend** dokumentiert.
> **Voraussetzung:** GitHub Desktop installiert, GitHub-Account vorhanden
> (siehe `docs/07_voraussetzungen.md`).

---

## Warum ein Repo von Anfang an?

Eure Dokumentation zählt **50 %** der Note. Wer erst am Ende alles
zusammenschreibt, verliert Details (und Punkte). Deshalb legt ihr das Repo
**jetzt** an und committet nach jedem wichtigen Schritt.

---

## Teil A – Die Zielstruktur

So soll euer Repository am Ende aussehen:

```
unser-ki-rag/
├── README.md              ← Kurzbeschreibung eures Projekts
├── wissensbasis/          ← eure .md-Wissensdokumente
├── compose/               ← eure docker-compose-Datei
├── arbeitsblaetter/       
├── doku/
│   ├── installation.md    ← Installationsweg + Fehler/Lösungen
│   └── tests.md           ← Vorher/Nachher + Grenzen-Experiment
└── screenshots/           ← Belege (WebUI, Antworten, Fehler)
```

> **Wichtig zu wissen:** Git speichert **keine leeren Ordner**. Damit ein Ordner
> im Repo auftaucht, muss eine Datei darin liegen. Wir nutzen dafür eine leere
> Platzhalter-Datei namens `.gitkeep` (siehe Teil C).

---

## Teil B – Repository in GitHub Desktop anlegen

**B.1** GitHub Desktop öffnen. Falls noch nicht angemeldet:
`File → Options → Accounts → Sign in` und mit eurem GitHub-Account anmelden.

**B.2** Neues Repository erstellen:
`File → New Repository…` (oder `Strg + N`).

Im Dialog ausfüllen:

| Feld | Eingabe |
|------|---------|
| **Name** | `unser-ki-rag` (oder ein eigener Name) |
| **Description** | z. B. „RAG-Assistent für Domäne XY" |
| **Local Path** | wo das Repo auf eurem PC liegen soll |
| **Initialize with a README** | ✅ Haken setzen |
| **Git ignore** | Dropdown: `Node` oder leer lassen (wir ergänzen gleich) |
| **License** | kann leer bleiben |

Dann **Create Repository** klicken.

**B.3** Repo auf GitHub veröffentlichen:
Oben auf **Publish repository** klicken.

- Haken bei **„Keep this code private"** setzen, wenn das Repo privat sein soll
  (mit Lehrkraft absprechen).
- **Publish Repository** bestätigen.

✅ Euer Repo liegt jetzt lokal **und** auf github.com.

---

## Teil C – Ordnerstruktur erstellen

**C.1** Öffnet den lokalen Repo-Ordner:
In GitHub Desktop `Repository → Show in Explorer` (Windows).

**C.2** Legt die Ordner an: `wissensbasis`, `compose`, `doku`, `screenshots`.

**C.3** Damit die (noch leeren) Ordner ins Repo kommen, legt in **jeden** Ordner
eine leere Datei namens `.gitkeep`. Schnell per Terminal im Repo-Ordner:

```bash
mkdir wissensbasis compose doku screenshots
type nul > wissensbasis\.gitkeep
type nul > compose\.gitkeep
type nul > doku\.gitkeep
type nul > screenshots\.gitkeep
```

(Unter Linux/Mac statt `type nul >` einfach `touch` verwenden.)

**C.4** Erstellt in `doku/` schon die zwei leeren Dateien `installation.md` und
`tests.md` – die füllt ihr im Laufe des Projekts.

---

## Teil D – Der Commit-Workflow (das macht ihr ab jetzt immer)

Jedes Mal, wenn ihr etwas Wichtiges geschafft habt (Installation läuft, Vorher-Test
gemacht, Wissensbasis geschrieben …):

**D.1** GitHub Desktop zeigt links unter **Changes** alle geänderten Dateien.

**D.2** Unten links eine kurze **Summary** eintippen, was ihr gemacht habt, z. B.:
- „Repo-Struktur angelegt"
- „Installation dokumentiert + Firewall-Problem gelöst"
- „Wissensbasis VLAN ergänzt"

**D.3** Auf **Commit to main** klicken.

**D.4** Oben auf **Push origin** klicken → eure Änderung ist auf github.com.

> **Merksatz:** *Schreiben → Commit → Push.* Erst nach dem Push sieht euer
> Teampartner (und die Lehrkraft) eure Änderungen online.

---

## Teil E – Teampartner einladen (einmalig)

Damit **beide** ins selbe Repo committen können:

**E.1** Auf <https://github.com> euer Repo öffnen.

**E.2** `Settings → Collaborators → Add people`.

**E.3** Den GitHub-Benutzernamen des Partners eingeben und einladen. Der Partner
nimmt die Einladung per E-Mail/GitHub an.

**E.4** Der Partner holt sich das Repo in GitHub Desktop:
`File → Clone Repository → (euer Repo auswählen) → Clone`.

> **Zusammenarbeit:** Bevor ihr loslegt, immer erst **Fetch/Pull origin**
> klicken, um den neuesten Stand des Partners zu holen. Sonst gibt es Konflikte.

---

## Teil F – .gitignore prüfen (keine Geheimnisse hochladen!)

Öffnet die Datei `.gitignore` in eurem Repo (oder legt sie an) und stellt sicher,
dass dort mindestens steht:

```
*.env
**/secrets*
*api*key*
webui-data/
ollama-data/
```

> **Niemals** API-Keys oder Passwörter committen – auch nicht in ein privates
> Repo.

---

## Abnahme-Checkliste

- [ ] Repo existiert lokal und auf github.com
- [ ] Ordner `wissensbasis`, `compose`, `doku`, `screenshots` sind im Repo sichtbar
- [ ] README.md vorhanden
- [ ] `.gitignore` enthält die Secret-Regeln
- [ ] Teampartner ist als Collaborator eingeladen
- [ ] Mindestens ein eigener Commit wurde gepusht

✅ **Geschafft, wenn:** Beide Teammitglieder das Repo in GitHub Desktop sehen und
die Struktur online auf github.com sichtbar ist.
