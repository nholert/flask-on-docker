# Flask on Docker ![Build Status](https://github.com/nholert/flask-on-docker/actions/workflows/build.yml/badge.svg)

## Overview

This repo contains a Flask web app that lets users upload images and access those images through the browser. It also serves static files and includes separate development and production environments. Docker Compose is used to run the application alongside PostgreSQL, with Gunicorn and Nginx added for the production setup.

## Demo

![Application Demo](flask-docker.gif)

## Build Instructions

### Development

Build and start the development containers:

```bash
docker compose up -d --build
```

Create the database tables:

```bash
docker compose exec web python manage.py create_db
```

Once the containers are running, open the app at:

`http://localhost:1136`

To upload an image, go to:

`http://localhost:1136/upload`

Uploaded images can be viewed at:

`http://localhost:1136/media/<filename>`

Static files can be viewed at:

`http://localhost:1136/static/<filename>`

To stop the development containers:

```bash
docker compose down
```

### Production

Build and start the production services:

```bash
docker compose -f docker-compose.prod.yml up -d --build
```

Create the production database tables:

```bash
docker compose -f docker-compose.prod.yml exec web python manage.py create_db
```

To stop the production containers:

```bash
docker compose -f docker-compose.prod.yml down
```

## Using the Application

Static files are available at:

```text
/static/<filename>
```

Images can be uploaded at:

```text
/upload
```

Uploaded images can then be viewed at:

```text
/media/<filename>
```

