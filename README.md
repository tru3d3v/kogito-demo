Create etchost :

sudo nano /private/etc/hosts  
127.0.0.1  data-index
127.0.0.1  keycloak

Run Docker Compose:
docker-compose -f docker-compose-keycloak.yaml up -d --build
