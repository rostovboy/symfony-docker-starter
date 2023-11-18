FROM php:8.1-fpm-alpine
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install packages
RUN apk update && apk upgrade
RUN apk add --no-cache curl git build-base zlib-dev oniguruma-dev autoconf libzip-dev libpng-dev libjpeg-turbo-dev libwebp-dev libxslt-dev icu-dev bash
RUN docker-php-ext-install \
    pdo pdo_mysql zip xsl gd intl opcache exif mbstring

# Xdebug
ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; \
    then \
      pecl install xdebug-3.1.0 && docker-php-ext-enable xdebug; \
    fi;

COPY ./docker/php-fpm/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /var/www

CMD composer install --no-interaction && php-fpm

EXPOSE 9000