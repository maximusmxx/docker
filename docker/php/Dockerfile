FROM php:8.3-fpm-alpine

# Install main packages and remove default server definition
RUN apk add --no-cache \
  bash \
  curl \
  git \
  wget \
  zip

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

ARG PHP_V=php83

# Install PHP and its extensions packages and remove default server definition
RUN apk add --no-cache \
  ${PHP_V}-cli \
  ${PHP_V}-ctype \
  ${PHP_V}-curl \
  ${PHP_V}-dom \
  ${PHP_V}-fileinfo \
  ${PHP_V}-fpm \
  ${PHP_V}-gd \
  ${PHP_V}-intl \
  ${PHP_V}-mbstring \
  ${PHP_V}-opcache \
  ${PHP_V}-openssl \
  ${PHP_V}-phar \
  ${PHP_V}-session \
  ${PHP_V}-tokenizer \
  ${PHP_V}-soap \
  ${PHP_V}-xml \
  ${PHP_V}-xmlreader \
  ${PHP_V}-xmlwriter \
  ${PHP_V}-simplexml \
  ${PHP_V}-zip \
  # Databases
  ${PHP_V}-pdo \
  ${PHP_V}-pdo_sqlite \
  ${PHP_V}-sqlite3 \
  ${PHP_V}-pdo_mysql \
  ${PHP_V}-mysqlnd \
  ${PHP_V}-mysqli \
  ${PHP_V}-pdo_pgsql \
  ${PHP_V}-pgsql \
  ${PHP_V}-mongodb \
  ${PHP_V}-redis

# PHP requires these extension from Docker
RUN docker-php-ext-install pdo pdo_mysql gd

# PHP PECL extensions
RUN apk add \
  ${PHP_V}-pecl-amqp \
  ${PHP_V}-pecl-xdebug

# PHP Composer
COPY --from=composer:2.8.4 /usr/bin/composer /usr/bin/composer

# Create symlink for php
RUN ln -sf /usr/bin/${PHP_V} /usr/bin/php

WORKDIR /var/www/
