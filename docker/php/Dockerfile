FROM php:8.3-fpm-alpine

ARG PHP_V=php83

# Install main packages and remove default server definition
RUN apk add --no-cache \
  bash \
  curl \
  git \
  wget \
  zip

RUN set -xe \
    && apk add --no-cache --virtual .build-deps \
        autoconf \
        freetype-dev \
        g++ \
        icu-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxslt-dev \
        libzip-dev \
        make \
        openssh-client \
        patch \
        rabbitmq-c-dev

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
  ${PHP_V}-simplexml \
  ${PHP_V}-soap \
  ${PHP_V}-tokenizer \
  ${PHP_V}-xml \
  ${PHP_V}-xmlreader \
  ${PHP_V}-xmlwriter \
  ${PHP_V}-zip \
  # Databases
  ${PHP_V}-mongodb \
  ${PHP_V}-mysqli \
  ${PHP_V}-mysqlnd \
  ${PHP_V}-pdo \
  ${PHP_V}-pdo_mysql \
  ${PHP_V}-pdo_pgsql \
  ${PHP_V}-pdo_sqlite \
  ${PHP_V}-pgsql \
  ${PHP_V}-sqlite3 \
  # Other
  rabbitmq-c

# PHP requires these extension from Docker
#RUN docker-php-ext-install pdo pdo_mysql gd
RUN docker-php-ext-install pdo pdo_mysql gd intl pcntl

# PHP PECL extensions
RUN pecl install \
    redis \
    amqp

RUN docker-php-ext-enable redis amqp

#RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
#    && docker-php-ext-install zip bcmath opcache \
#    && pecl install xdebug \
#    && docker-php-ext-enable xdebug

#rm -rf /var/lib/apt/lists/*

# PHP Composer
COPY --from=composer:2.8.4 /usr/bin/composer /usr/bin/composer

# Create symlink for php
#RUN ln -sf /usr/bin/${PHP_V} /usr/bin/php

WORKDIR /var/www/
