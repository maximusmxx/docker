
## Install project
```bash
git clone ...
copy .env.example .env
```

Configure `.env`

```bash
docker compose build
docker compose up -d
```
---

## Install Laravel
```bash
docker compose exec php sh
cd app
compose create-project --prefer-dist laravel/laravel .

chown -R www-data:www-data ./storage

composer install --no-scripts --no-autoloader
```

Configure `.env`

```bash
php artisan about
```
---

## Manage Docker as a non-root user

[Install Docker](https://docs.docker.com/engine/install/ubuntu/)

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
---













___
___
___
___
___

## ....

```yml
services:
  php:
    build:
      args:
        user: testuser
        uid: 1000
```

# Start from a PHP image with Apache
FROM php:8.2-fpm

# Arguments defined in docker-compose.yml
ARG user
ARG uid
....

### Create system user to run Composer and Artisan Commands
```dockerfile
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
chown -R $user:$user /home/$user
```
### Set working directory
```dockerfile
WORKDIR /var/www
USER $user
```























