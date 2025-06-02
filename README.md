# Keycloak <= 26.8
Production keycloak deployment with postgres db
Maintenance steps:
- create TLS certs and fix access rights
- add options
- add backups
- add opentelemetry with traces

git clone https://github.com/Akhaladze/keycloak.git
cd keycloak
## Edit config appropriate to your domain name
nano ./keycloak.cnf
## Make ssl config folder and Copy config file to your host
sudo mkdir -p /etc/ssl/keycloak

sudo cp ./keycloak.cnf /etc/ssl/keycloak/keycloak.cnf

sudo openssl req -x509 -nodes -days 825 \
  -newkey rsa:2048 \
  -keyout /etc/ssl/keycloak/tls.key \
  -out /etc/ssl/keycloak/tls.crt \
  -config /etc/ssl/keycloak/keycloak.cnf

sudo chmod 600 /etc/ssl/keycloak/tls.key
sudo chown 1000:1000 /etc/ssl/keycloak/tls.key

## Run docker compose project
docker compose up -d
