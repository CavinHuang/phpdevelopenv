#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "update.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM php:7.2.2-fpm

ENV PHPREDIS_VERSION 3.1.3

#for redis and mysql
RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
        pdo pdo_mysql \
        bcmath

#for gd
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        procps \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# for grpc extention
RUN  apt-get install -y \
        libmemcached-dev zlib1g-dev \
    && pecl install grpc \
    && pecl install protobuf \
    && rm -rf /usr/src/php

# for zip
RUN apt-get update \
    && apt-get install -y --no-install-recommends libzip-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) zip