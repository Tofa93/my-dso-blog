---
title: Deployment
sidebar_label: Deployment
sidebar_position: 3
description: Running Baby Tools World in Docker on a Linux virtual server.
---

# Deployment

I deployed Baby Tools World to an existing Linux virtual server using SSH, Git, Docker, and Gunicorn.

## Build the image

On the server, I checked out the project branch and built the Docker image:

```bash
git clone -b add-product-tags git@github.com:Tofa93/baby-tools-world.git
cd baby-tools-world
docker build -t baby-tools-world:local .
```

## Configure the application

The server uses a local `.env` file (excluded from Git) containing the required configuration:

```dotenv
ALLOWED_HOSTS=YOUR_SERVER_IP,127.0.0.1,localhost
DEBUG=false
DJANGO_SECRET_KEY=REPLACE_WITH_A_RANDOM_SECRET
```

The real secret is generated separately and is **never committed**. Django reads it from the `DJANGO_SECRET_KEY` environment variable.

## Run with persistent data

SQLite data and uploaded product images are stored outside the container using bind mounts:

```bash
mkdir -p ~/btw-data/media
touch ~/btw-data/db.sqlite3

docker run -d \
  --name baby-tools-world \
  --restart unless-stopped \
  --env-file .env \
  -p 8000:8000 \
  -v "$HOME/btw-data/db.sqlite3:/app/src/db.sqlite3" \
  -v "$HOME/btw-data/media:/app/src/media" \
  --entrypoint /bin/sh \
  baby-tools-world:local \
  -c 'python manage.py migrate && python manage.py collectstatic --noinput && exec gunicorn btw_app.wsgi:application --bind 0.0.0.0:8000'
```

The initial sample products were added using:

```bash
docker exec baby-tools-world python manage.py seed_db
```

## Result

The application was reachable through the VM's IP address on port `8000`. The four sample categories and 15 seeded products loaded correctly. I created an additional product, `cuddly-fox-01`, and confirmed that it **still existed after `docker restart baby-tools-world`**.

:::caution Security
The IP-based HTTP endpoint was used for a project demonstration. Before public production use, HTTPS and Django's production security settings should be configured. Admin credentials should not be entered over unencrypted public HTTP.
:::
