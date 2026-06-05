# M169 Mini-Projekt — Container / Cloud
**Luka Aurelius Sola (LAS)** | GBS St. Gallen | Modul 169

---

## Aufgabe 1 — Eigener NGINX Webserver

### Beschreibung
Eigenes Docker-Image auf Basis von `nginx:alpine` mit einer einfachen HTML-Seite.  
Die Seite ist über Port **8080** erreichbar. HTML-Dateien und Logs liegen als Volumes lokal.

### Struktur
```
aufgabe1-webserver/
├── Dockerfile
├── html/
│   └── index.html
└── logs/
```

### Befehle

**Image bauen:**
```bash
docker build -t las-webserver .
```

**Container starten:**
```bash
docker run -d \
  -p 8080:80 \
  -v $(pwd)/html:/usr/share/nginx/html \
  -v $(pwd)/logs:/var/log/nginx \
  --name las-webserver \
  las-webserver
```

**Webseite aufrufen:** → `http://<AWS-IP>:8080`

---

## Aufgabe 2 — WordPress mit Docker

### Beschreibung
WordPress + MySQL als zwei separate Docker Container, verbunden über ein eigenes Docker Netzwerk.

### Struktur
```
aufgabe2-wordpress/
└── README.md
```

### Befehle

**Netzwerk erstellen:**
```bash
docker network create wp-network
```

**MySQL Container starten:**
```bash
docker run -d --name wp-db --network wp-network \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=wordpress \
  -e MYSQL_USER=wpuser \
  -e MYSQL_PASSWORD=wppass \
  mysql:8.0
```

**WordPress Container starten:**
```bash
docker run -d --name wp-app --network wp-network \
  -p 80:80 \
  -e WORDPRESS_DB_HOST=wp-db:3306 \
  -e WORDPRESS_DB_NAME=wordpress \
  -e WORDPRESS_DB_USER=wpuser \
  -e WORDPRESS_DB_PASSWORD=wppass \
  wordpress:latest
```

**WordPress aufrufen:** → `http://<AWS-IP>`

---

*Modul 169 | W16 | GBS St. Gallen*
