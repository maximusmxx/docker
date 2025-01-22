
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










