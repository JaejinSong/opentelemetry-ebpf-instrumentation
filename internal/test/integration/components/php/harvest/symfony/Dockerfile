FROM composer:2.11@sha256:537fb03057ed901ae06bde7ef25af348903485ae1acc7fc789b80d8bac666f35 AS dependencies

WORKDIR /app
COPY internal/test/integration/components/php/harvest/symfony/composer.json internal/test/integration/components/php/harvest/symfony/composer.lock ./
RUN composer install --no-dev --no-interaction --no-scripts --prefer-dist

FROM php:8.6.0-fpm@sha256:23da58abd99055b97191fcca104126d552cc7b96c8cfe25f724311d52635696d

WORKDIR /var/www/symfony-harvest
COPY --from=dependencies /app/vendor ./vendor
COPY internal/test/integration/components/php/harvest/symfony/composer.json internal/test/integration/components/php/harvest/symfony/composer.lock ./
COPY internal/test/integration/components/php/harvest/symfony/config ./config
COPY internal/test/integration/components/php/harvest/symfony/public ./public
COPY internal/test/integration/components/php/harvest/symfony/src ./src
COPY internal/test/integration/components/php/harvest/php-fpm.conf /usr/local/etc/php-fpm.d/www.conf
RUN mkdir -p var/cache var/log && chown -R www-data:www-data var
