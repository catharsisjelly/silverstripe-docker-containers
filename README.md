# Docker containers for Silverstripe

This is a sample config for running PHP that is capable of running the Silverstripe CMS, it is compatible with V3 and V4 of Silverstripe and uses NginX as the webserver.

## Requirements

 * Docker
 * Docker Compose

## Instructions

Copy the `build` directory and the `docker-compose.yml` file over to your relevant project.

```
docker-compose build --force-rm --no-cache
docker-compose up -d
docker-compose exec php ./vendor/bin/sake dev/build
```

## TODO

* Make this more interactive so that a CLI builds the containers for you, similar to `silverstripe-installer`

## Container Breakdown

### PHP

PHP is supplied in both PHP 7.1 and 7.4, if you want other versions then feel free to submit a PR or create an issue. To switch between the two versions change lines in the `docker-compose.yml` file accordingly. Some of the variables you need in the for the `.env` config are setup in the container, look at the `environment` section and change as you see fit or override by using a `.env` file

#### XDebug

To setup XDebug you need to make sure that your IDE is set to listen on port `9001`.  You will need to uncomment and change the `xdebug.idekey` value in the `xdebug.ini` file.

#### PHP 7.1

```
php:
  build:
    context: build/silverstripe-php-7-1
  image: catharsisjelly/silverstripe-php:7.1-fpm
```

#### PHP 7.4

```
php:
  build:
    context: build/silverstripe-php-7-4
  image: catharsisjelly/silverstripe-php:7.4-fpm
```

### NginX

NginX has been set up to work with the most recent stable version of the application. To switch between SS3 and SS4 configuration change the line in the `build\nginx\Dockerfile` and then ensure you rebuild your containers. It's set up as SSL on port by default with a self-generated key, the `docker-compose.yml` file exposes that on port `4430` so to access your webserver browse to `https://0.0.0.0:4430`

```
COPY ss-{version}.conf /etc/nginx/conf.d/default.conf
```
