# Aufgabe 2 — WordPress mit Docker

## Befehle

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

**Aufrufen:** → `http://<AWS-IP>`
