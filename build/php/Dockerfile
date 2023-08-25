FROM php:7.0-fpm-alpine

COPY ./build/php/php-fpm.conf /usr/local/etc/php-fpm.d/www.conf

RUN apk update \
    && apk add --no-cache libpng libpng-dev libjpeg-turbo-dev libwebp-dev zlib-dev \
    && docker-php-ext-install mysqli pdo pdo_mysql gd

