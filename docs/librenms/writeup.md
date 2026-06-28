Some stuff about how I deployed LibreNMS in my homelab.

Start with the source. docs.librenms.org/

Some quick google-fu says docker is best as otherwise I'll bungle it due to complex dependency configurations.

Ok, let's go...

Docker quickstart says to download and unzip composer files:

```
mkdir librenms
cd librenms
wget https://github.com/librenms/docker/archive/refs/heads/master.zip
unzip master.zip
cd docker-master/examples/compose
```
Then to "Set a new mysql password in .env and inspect compose.yml"

Uhhh what? What even does "inspect compose.yml" mean? Am I supposed to set a password for both? Set a password for .env and THEN just inspect compose.yml? Inspect it for what? 

A quick google search reveals something along the lines of: 

```
MYSQL_DATABASE=librenms
MYSQL_USER=librenms
MYSQL_PASSWORD=YourStrongPassword123!
```
For the .evn 

and 

```
services:
  db:
    image: mariadb:10.5  # or mysql:8
    environment:
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      # Optional: Set root password separately if needed
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
```

for the compose.yml 

