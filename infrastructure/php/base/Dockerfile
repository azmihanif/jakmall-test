# Image of php-fpm
FROM php:8.0.3-fpm-alpine3.13 AS php-fpm

WORKDIR /var/www/html

RUN rm ${PHP_INI_DIR}/php.ini-development \
    && cp -a ${PHP_INI_DIR}/php.ini-production ${PHP_INI_DIR}/php.ini \
    && apk --no-cache add --virtual .build-deps $PHPIZE_DEPS \
    && pecl install redis \     
    && docker-php-ext-install \
        pdo \
        pdo_mysql \
        bcmath \
        opcache \
    && apk del -f .build-deps \
    && docker-php-ext-enable pdo_mysql redis 

# Image of Worker
FROM php:8.0.3-fpm-alpine3.13 AS worker

WORKDIR /var/www/html

RUN rm ${PHP_INI_DIR}/php.ini-development \
    && cp -a ${PHP_INI_DIR}/php.ini-production ${PHP_INI_DIR}/php.ini \
    && apk --no-cache add --virtual .build-deps $PHPIZE_DEPS \
    && pecl install redis \     
    && docker-php-ext-install \
        pdo \
        pdo_mysql \
        bcmath \
    && apk del -f .build-deps \
    && docker-php-ext-enable pdo_mysql redis 
