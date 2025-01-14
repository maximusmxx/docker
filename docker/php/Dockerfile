ARG PHP_V=8.3
ARG PHP_V2=php83
#ENV PHP_V="php83"

FROM php:${PHP_V}-fpm-alpine

# Setup unique user and group - needs bash
RUN apk add --no-cache bash

# Install main packages and remove default server definition
RUN apk add --no-cache \
  curl \
  wget \
  zip \
  bash \
  vim \
  git

RUN set -xe \
    && apk add --no-cache --virtual .build-deps \
        libzip-dev \
        freetype-dev \
        icu-dev \
        libmcrypt-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libxslt-dev \
        patch \
        openssh-client

# Install PHP and its extensions packages and remove default server definition
RUN apk add --no-cache \
  ${PHP_V2} \
  ${PHP_V2}-cli \
  ${PHP_V2}-ctype \
  ${PHP_V2}-curl \
  ${PHP_V2}-dom \
  ${PHP_V2}-fileinfo \
  ${PHP_V2}-fpm \
  ${PHP_V2}-gd \
  ${PHP_V2}-intl \
  ${PHP_V2}-mbstring \
  ${PHP_V2}-opcache \
  ${PHP_V2}-openssl \
  ${PHP_V2}-phar \
  ${PHP_V2}-session \
  ${PHP_V2}-tokenizer \
  ${PHP_V2}-soap \
  ${PHP_V2}-xml \
  ${PHP_V2}-xmlreader \
  ${PHP_V2}-xmlwriter \
  ${PHP_V2}-simplexml \
  ${PHP_V2}-zip \
  # Databases
  ${PHP_V2}-pdo \
  ${PHP_V2}-pdo_sqlite \
  ${PHP_V2}-sqlite3 \
  ${PHP_V2}-pdo_mysql \
  ${PHP_V2}-mysqlnd \
  ${PHP_V2}-mysqli \
  ${PHP_V2}-pdo_pgsql \
  ${PHP_V2}-pgsql \
  ${PHP_V2}-mongodb \
  ${PHP_V2}-redis

# PHP requires these extension from Docker
RUN docker-php-ext-install pdo pdo_mysql gd

# PHP PECL extensions
RUN apk add \
  ${PHP_V2}-pecl-amqp \
  ${PHP_V2}-pecl-xdebug

# PHP Composer
#COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
COPY --from=composer:2.8.4 /usr/bin/composer /usr/bin/composer

# install php and node.js dependencies
#RUN composer install --no-dev --prefer-dist \
#    && npm install \
#    && npm run build

# copy necessary files and change permissions
RUN chown -R www-data:www-data /var/www \
    && chown -R www-data:www-data /var/www/vendor \
    && chmod -R 775 /var/www/bootstrap/cache \
    && chmod -R 775 /var/www/storage \
    && chmod -R 775 /var/www/vendor

# Create symlink for php
#RUN ln -sf /usr/bin/${PHP_V2} /usr/bin/php

WORKDIR /var/www/
