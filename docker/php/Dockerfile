FROM php:fpm-alpine

COPY php.ini $PHP_INI_DIR/conf.d/

# Install PHP extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions xdebug redis pgsql

RUN set -ex \
    && apk --no-cache add \
    postgresql-dev

RUN docker-php-ext-install mysqli pdo pdo_mysql pdo_pgsql

# Install packages
RUN apk add git  bash nano apk-cron

# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
