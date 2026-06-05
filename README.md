# M169 Mini-Projekt — Container / Cloud
**Luka Aurelius Sola (LAS)** | GBS St. Gallen | Modul 169

---

## Aufgabe 1 — Eigener NGINX Webserver

### Beschreibung
Eigenes Docker-Image auf Basis von `nginx:alpine` mit einer einfachen HTML-Seite.  
Die Seite ist über Port **8080** erreichbar. HTML-Dateien und Logs liegen als Volumes lokal.

### Struktur
```
m169-miniprojekt/
├── README.md
├── aufgabe1-webserver/
│   ├── Dockerfile
│   ├── html/
│   │   └── index.html
│   └── logs/          ← leer, aber .gitkeep rein damit Git den Ordner trackt
└── aufgabe2-wordpress/
    └── docker-compose.yml
```

### Befehle

**Image bauen:**
```bash
docker build -t las-webserver .
```

**Container starten (mit Volumes für HTML & Logs):**
```bash
docker run -d \
  -p 8080:80 \
  -v $(pwd)/html:/usr/share/nginx/html \
  -v $(pwd)/logs:/var/log/nginx \
  --name las-webserver \
  las-webserver
```

**Webseite aufrufen:** → http://localhost:8080

---

## Aufgabe 2 — WordPress mit Docker Compose

### Beschreibung
WordPress + MySQL als Multi-Container-Stack via `docker-compose.yml`.

### Struktur
```
wordpress/
└── docker-compose.yml
```

### Befehle

**Stack starten:**
```bash
docker compose up -d
```

**Stack stoppen:**
```bash
docker compose down
```

**WordPress aufrufen:** → http://localhost:8080

### Erklärung docker-compose.yml
| Zeile / Key | Bedeutung |
|---|---|
| `version: "3.9"` | Compose-Datei-Format-Version |
| `services:` | Liste aller Container im Stack |
| `db:` | MySQL-Datenbank-Container |
| `wordpress:` | WordPress-Applikations-Container |
| `image:` | Welches Docker-Image verwendet wird |
| `restart: always` | Container startet automatisch neu bei Absturz |
| `depends_on:` | Startreihenfolge — WordPress wartet auf DB |
| `ports:` | Port-Mapping Host:Container |
| `environment:` | Umgebungsvariablen (Zugangsdaten, DB-Name) |
| `volumes:` | Persistente Datenspeicher (Daten bleiben nach Neustart) |

---

*Modul 169 | W16 | GBS St. Gallen*
