# ===== Mini-Projekt M169 | LAS =====
# Basis-Image: NGINX Alpine (schlanke Linux-Variante)
FROM nginx:alpine

# Metadaten
LABEL maintainer="Luka Aurelius Sola (LAS)"
LABEL description="M169 Mini-Projekt - Custom NGINX Webserver"
LABEL version="1.0"
LABEL school="GBS St. Gallen"
LABEL module="M169 - Container / Cloud"

# Standardmässige NGINX-Seite entfernen
RUN rm -rf /usr/share/nginx/html/*

# Eigene HTML-Seite ins NGINX-Webroot kopieren
COPY html/ /usr/share/nginx/html/

# Port 80 freigeben (wird extern auf 8080 gemappt)
EXPOSE 80

# NGINX im Vordergrund starten (wichtig für Docker)
CMD ["nginx", "-g", "daemon off;"]
