# Projekt: Musikfest Aufgaben-Tracker
**Musikkapelle Wohnrod e.V. — Musikfest 2026**
*Erstellt: Mai 2026*

---

## 🎯 Ziel
Interaktiver Aufgaben-Tracker für das Musikfest, der für alle Vorstandsmitglieder ohne Login zugänglich ist. Aufgaben können abgehakt, bearbeitet, kommentiert und neu erstellt werden. Alle Änderungen sind sofort für alle sichtbar.

---

## 🔗 Wichtige Links & Zugänge

| Was | Wo |
|---|---|
| **Live-App** | https://hweismantel.github.io/musikfest-aufgaben/musikfest_aufgaben.html |
| **GitHub Repo** | https://github.com/hweismantel/musikfest-aufgaben |
| **JSONBin Dashboard** | https://jsonbin.io |
| **JSONBin Bin-ID** | `6a18b1fdddf5aa59f771b22c` |

---

## 🏗️ Architektur

```
Browser (User)
    │
    ▼
GitHub Pages          ← hostet die HTML-Datei (statisch)
    │
    ▼
JSONBin API           ← speichert alle Aufgaben als JSON (cloud)
    │
    ▼
localStorage          ← lokaler Fallback im Browser
```

### Warum diese Kombination?
- **GitHub Pages**: Kostenlos, HTML wird direkt im Browser geöffnet (kein Download), stabiler Hosting-Service
- **JSONBin**: Einfache REST-API für JSON-Daten, kostenloser Free-Plan (10.000 Requests/Monat), kein eigener Server nötig
- **localStorage**: Fallback wenn JSONBin nicht erreichbar, zeigt sofort Daten beim Laden

---

## 📁 Dateien

| Datei | Beschreibung |
|---|---|
| `musikfest_aufgaben.html` | Die komplette App — eine einzige selbstständige HTML-Datei |
| `README.md` | GitHub Repository Beschreibung |

---

## ⚙️ Technische Details

### JSONBin Konfiguration
```javascript
const BIN_ID  = '6a18b1fdddf5aa59f771b22c';  // Public Bin
const API_KEY = '$2a$10$f3U9e1oo...';          // X-Master-Key (in HTML-Datei)
const BIN_URL = `https://api.jsonbin.io/v3/b/${BIN_ID}`;
```

> ⚠️ **Wichtig:** Der X-Master-Key steht im Quellcode der HTML-Datei. Für Vereinsaufgaben akzeptables Risiko. Bei Bedarf kann der Key in JSONBin regeneriert werden.

### Speicher-Logik
- Beim Öffnen: zuerst localStorage laden (sofort), dann JSONBin laden (cloud)
- Bei Änderungen: 1,5 Sekunden nach letzter Änderung wird JSONBin aktualisiert
- Alle 60 Sekunden: automatische Synchronisierung im Hintergrund

### Sync-Status (oben rechts in der App)
| Farbe | Bedeutung |
|---|---|
| 🟡 Gelb blinkend | Wird gerade geladen/gespeichert |
| 🟢 Grün | Erfolgreich synchronisiert |
| 🔴 Rot | Fehler — lokale Daten werden angezeigt |

---

## 👥 Personen & Kürzel

| Kürzel | Name |
|---|---|
| HW | Harry |
| BH | Nickels |
| TM | Thiemo |
| FG | Flobbes |
| JV | Jannis |
| EV | Eli |
| KS | unbekannt |
| RH | unbekannt |
| MM | unbekannt |
| VS | unbekannt |

---

## ✅ Implementierte Features

- [x] 50 Aufgaben aus VSS4-Protokoll vom 17.05.2026
- [x] Aufgaben abhaken (Erledigt-Status)
- [x] Filter nach Person, Bereich, Status
- [x] Freitextsuche
- [x] Sortierbare Spalten (Aufgabe, Bereich, Person)
- [x] Bemerkungsfeld pro Zeile (inline, Platzhalter „Bemerkung…")
- [x] ✏️ Bearbeiten-Modal (Aufgabe, Bereich, Person ändern)
- [x] 🗑️ Aufgaben löschen
- [x] Neue Aufgaben hinzufügen
- [x] Dropdown-Menüs mit „+ Neu…" Option für eigene Einträge
- [x] Statistik-Kacheln (Gesamt / Erledigt / Offen / Angezeigt)
- [x] Fortschrittsbalken
- [x] Cloud-Sync via JSONBin (alle sehen denselben Stand)
- [x] Lokaler Fallback via localStorage
- [x] Automatische Synchronisierung alle 60 Sekunden
- [x] Responsive Design (funktioniert auf Mobilgeräten)

---

## 🔧 Offene Punkte / TODO

- [ ] Checkbox vertikal zentrieren (kosmetisches Problem)
- [ ] Kürzel KS, RH, MM, VS durch echte Namen ersetzen
- [ ] Evtl. PDF-Import: neue Aufgaben aus Protokoll-PDF automatisch einlesen

---

## 🔄 Workflow: App aktualisieren

### Neue Version deployen
1. HTML-Datei lokal bearbeiten (oder von Claude erstellen lassen)
2. Auf GitHub hochladen: **„Add file"** → **„Upload files"** → Datei auswählen → **„Commit changes"**
3. GitHub Pages deployed automatisch innerhalb von ~1 Minute

### JSONBin Key erneuern (falls nötig)
1. jsonbin.io → API Keys → X-Master-Key regenerieren
2. Neuen Key in HTML-Datei eintragen: `const API_KEY = 'NEUER_KEY';`
3. Datei auf GitHub hochladen

### JSONBin Bin zurücksetzen (Notfall)
1. jsonbin.io → Bins → Bin bearbeiten
2. Inhalt ersetzen mit: `{"tasks":[],"nextId":100}`
3. App lädt dann beim nächsten Öffnen die Default-Aufgaben neu

---

## 💡 Für zukünftige Projekte: Vorlage

Diese Architektur (GitHub Pages + JSONBin) eignet sich für jeden einfachen Vereins-Tracker:
- Kosten: **0 €**
- Kein Server, kein Backend, kein Login
- Einfach HTML-Datei anpassen und neu hochladen
- Skaliert für kleine Teams (bis ~10 Personen, bis ~10.000 API-Calls/Monat kostenlos)

**Anpassbare Teile für neue Projekte:**
- `DEFAULT_TASKS` Array → eigene Einträge
- Spalten in der Tabelle → beliebig erweiterbar
- Farben und Schriften → CSS-Variablen am Anfang der Datei

---

*Dokumentation erstellt mit Claude (Anthropic) — Mai 2026*
