# Docker containers for Silverstripe

This is a sample config for running PHP that is capable of running the Silverstripe CMS, it is compatible with V3 and V4 of Silverstripe

## Requirements

 * Docker
 * Docker Compose

## Instructions

```
docker-compose build
docker-compose up -d
```

## Container Breakdown

### PHP

PHP is supplied in both PHP 7.1 and 7.4, if you want other versions then feel free to submit a PR or create an issue. To switch between the two versions change lines in the `docker-compose.yml` file accordingly

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

NginX has been set up to work with the most recent stable version of the application. To switch between SS3 and SS4 configuration change the line in the `build\nginx\Dockerfile` and then ensure you rebuild your containers

```
COPY ss-{version}.conf /etc/nginx/conf.d/default.conf
```
