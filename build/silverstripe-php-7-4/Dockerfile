FROM php:7.4-fpm
COPY php.ini /usr/local/etc/php/php.ini
COPY couchbase.key /tmp/couchbase.key
COPY extra-ini/* /usr/local/etc/php/conf.d/
RUN apt-get update && \
    apt-get install -y libzip-dev \
        libjpeg62-turbo-dev \
        libicu-dev \
        libpng-dev \
        gnupg2 \
        lsb-release \
        software-properties-common \
        build-essential
RUN apt-key add /tmp/couchbase.key && \
    apt-add-repository 'deb https://packages.couchbase.com/clients/c/repos/deb/debian10 buster buster/main' && \
    apt-get update && \
    apt-get install -y libcouchbase-dev
RUN docker-php-ext-install intl pdo_mysql zip gd
RUN pecl install xdebug
RUN pecl install https://packages.couchbase.com/clients/php/couchbase-3.0.3.tgz
RUN apt-get clean && apt-get purge
