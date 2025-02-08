FROM php:8.3-fpm-alpine
ENV TZ=UTC

# Default modules in PHP 8.3
# ctype curl date dom fileinfo filter hash iconv json libxml mbstring mysqlnd openssl pcre pdo pdo_sqlite phar posix
# random readline reflection session simplexml sodium spl sqlite3 standard tokenizer xml xmlreader xmlwriter zlib

# Server Requirements for Laravel 11
# ctype curl dom fileinfo filter hash mbstring openssl pcre pdo session tokenizer xml

# Install main packages and remove default server definition
RUN apk add --no-cache \
  bash \
  curl \
  git \
  linux-headers \
  vim \
  wget \
  zip

RUN set -xe \
  && apk add --no-cache --virtual .build-deps \
    autoconf \
    icu-dev \
    g++ \
    libpng-dev \
    libzip-dev \
    make \
    openssh-client \
    postgresql-dev \
    rabbitmq-c-dev

# For command docker-php-ext-install possible values
# bcmath bz2 calendar ctype curl dba dl_test dom enchant exif ffi fileinfo filter ftp gd gettext gmp hash iconv imap
# intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql
# pdo_sqlite pgsql phar posix pspell random readline reflection session shmop simplexml snmp soap sockets sodium spl
# standart sysvmsg sysvsem sysvshm tidy tokenizer xml xmlreader xmlwriter xsl zend_test zip

# Install PHP extensions from Docker
RUN docker-php-ext-install \
    gd \
    intl \
    pcntl \
    pdo_mysql
    #pdo_pgsql

# Install PHP PECL extensions
RUN pecl install amqp && docker-php-ext-enable amqp \
    && pecl install mongodb && docker-php-ext-enable mongodb \
    && pecl install redis && docker-php-ext-enable redis \
    && pecl install xdebug && docker-php-ext-enable xdebug

# Install PHP Composer
COPY --from=composer:2.8.4 /usr/bin/composer /usr/bin/composer

# Enable Laravel schedule in Cron
RUN echo "$(crontab -l; echo '* * * * * cd /var/www/ && php artisan schedule:run >> /dev/null 2>&1')" | crontab -

# Enable Cron
CMD crond -l 0 && php-fpm

WORKDIR /var/www/

# Install PHP dependencies
#RUN composer install --no-dev --prefer-dist

# Install node.js and dependencies
#RUN npm install && npm run build
