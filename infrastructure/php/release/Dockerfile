#Install composer
FROM composer:2.0.11 AS vendor
WORKDIR /app
RUN composer install -vvv --no-dev --ignore-platform-reqs --no-scripts


#Image of PHP-fpm
FROM jakmall/recruitment/cloud-engineer/counter/php-fpm AS php-fpm
WORKDIR /var/www/html
COPY --from=vendor /app/vendor /app/vendor
RUN composer dump-autoload && php artisan route:cache && php artisan view:cache
RUN mkdir -p storage/framework/views && chmod 777 -R storage .env bootstrap/cache \
    && touch .env \
    && rm -rf infrastructure \
    && composer dump-autoload \
    && php artisan route:cache \
&& php artisan view:cache


#Image of Worker
FROM jakmall/recruitment/cloud-engineer/counter/php-cli AS php-cli
WORKDIR /var/www/html
COPY --from=vendor /app/vendor /app/vendor
RUN composer dump-autoload && php artisan route:cache && php artisan view:cache
RUN mkdir -p storage/framework/views && chmod 777 -R storage .env bootstrap/cache \
    && touch .env \
    && rm -rf infrastructure \
    && composer dump-autoload \
    && php artisan route:cache \
&& php artisan view:cache
