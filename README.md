Portus and Docker Registry
==========================
* Only host on a single node
* HSTS

Edit nginx.portus.conf, change portus.host.tld to your FQDN
- server_name portus.host.tld;

Generate self-signed certificate in secrets forder
```
$ cd secrets/
$ openssl req -newkey rsa:4096 -nodes -sha256 -keyout portus.key -x509 -days 3650 -out portus.crt
```

Edit Enviornment Variables in docker-compose.yml
- PORTUS_DB_HOST: db.host.tld
- PORTUS_DB_DATABASE: portus
- PORTUS_DB_USERNAME: portus
- PORTUS_SECRET_KEY_BASE: "somerandomstring"
for both portus and background service
 
Enviornment Variables for docker-compose command
- PORTUS_URL=https://portus.host.tld
- PORTUS_MACHINE_FQDN_VALUE=portus.host.tld
- PORTUS_DB_PASSWORD=********
- PORTUS_PASSWORD=********

docker-compose command example:

```
PORTUS_URL="https://10.10.8.150" \
PORTUS_MACHINE_FQDN_VALUE=10.10.8.150 \
PORTUS_DB_PASSWORD=******** \
PORTUS_PASSWORD=******** \
docker-compose up -d 
```
