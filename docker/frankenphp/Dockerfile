FROM dunglas/frankenphp:1.4.0-php8.3.15-alpine

# add additional extensions here:
RUN install-php-extensions \
	pdo_mysql \
	gd \
	intl \
	zip \
	opcache

COPY cfg/ /etc/caddy/

ENV FRANKENPHP_CONFIG="worker ./public/index.php"

#ENTRYPOINT ["php", "artisan", "octane:frankenphp"]
#COPY cfg/nginx.conf /etc/nginx/nginx.conf
#frankenphp php-server -r public/
