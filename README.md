
Форкнуто и переделано на SOPDS 0.5

огромное спасибо https://github.com/ichbinkirgiz/sopds и https://github.com/zveronline/docker-sopds

# Introduction

Dockerfile to build a Simple OPDS server docker image.
http://www.sopds.ru

# Installation

собрать
docker build --network=host -t sopds .

# Quick Start

Run the image

```
docker run --name sopds -d \
   --volume /path/to/library:/library:ro \
   --publish 8001:8001 \
   sopds
```

This will start the sopds server and you should now be able to browse the content on port 8081.

```
docker run --name sopds -d \
   --volume /path/to/library:/library:ro \
   --volume /path/to/database:/var/lib/pgsql \
   --publish 8001:8001 \
   sopds
```

Also you can store postgresql database on external storage.

```
docker run --name sopds -d \
   --volume /path/to/library:/library:ro \
   --env 'DB_USER=sopds' \
   --env 'DB_NAME=sopds' \
   --env 'DB_PASS=sopds' \
   --env 'DB_HOST=""' \
   --env 'DB_PORT=""' \
   --env 'EXT_DB=True' \
   --publish 8001:8001 \
   sopds
```


# Create superuser

By default the superuser will be created with predefined name "admin" and password "admin". But you can manage it via appropriate environmental variables:
```bash
docker run --name sopds -d \
   --volume /path/to/library:/library:ro \
   --volume /path/to/database:/var/lib/pgsql \
   --env 'SOPDS_SU_NAME="your_name_for_superuser"' \
   --env 'SOPDS_SU_EMAIL='"your_mail_for_superuser@your_domain"' \
   --env 'SOPDS_SU_PASS="your_password_for_superuser"' \
   --publish 8001:8001 \
   sopds
```

# Scan library

```bash
docker exec -ti sopds bash
python3 manage.py sopds_util setconf SOPDS_SCAN_START_DIRECTLY True
```

# Telegram bot autostart

To do this you need to use a variable:
SOPDS_TMBOT_ENABLE=True
