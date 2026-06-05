# ===== Mini-Projekt M169 | LAS =====
# Basis-Image: NGINX (Alpine = schlanke Linux-Variante)
FROM nginx:alpine

# Metadaten
LABEL maintainer="LAS"
LABEL description="Mini-Projekt M169 - Custom NGINX Webserver"

# Eigene HTML-Seite ins NGINX-Webroot kopieren
COPY html/ /usr/share/nginx/html/

# Port 80 freigeben (wird extern auf 8080 gemappt)
EXPOSE 80
