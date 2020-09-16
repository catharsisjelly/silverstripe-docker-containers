FROM php:7.1-fpm
COPY php.ini /usr/local/etc/php/php.ini
RUN apt-get update && \
    apt-get install -y libzip-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libicu-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ && \
    docker-php-ext-configure intl && \
    docker-php-ext-configure zip && \
    docker-php-ext-install -j "$(nproc)" gd intl pdo_mysql zip
RUN pecl install xdebug
COPY extra-ini/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
RUN apt-get clean && apt-get purge
