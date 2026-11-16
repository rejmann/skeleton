FROM node:lts-slim AS assets

COPY --chown=www-data:www-data ./package*.json /var/www/html/
WORKDIR /var/www/html

RUN npm install --pure-lockfile

COPY --chown=www-data:www-data ./assets /var/www/html/assets
COPY --chown=www-data:www-data ./tsconfig.json ./vite.config.js ./tailwind.config.js ./postcss.config.js /var/www/html/

FROM php:8.5-fpm

ENV TZ=America/Sao_Paulo

RUN apt update -y \
    && apt install -y zlib1g-dev g++ git libicu-dev libzip-dev supervisor \
    && docker-php-ext-configure zip \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-install intl pdo pdo_mysql zip pcntl bcmath \
    && pecl install apcu redis \
    && docker-php-ext-enable apcu redis

WORKDIR /var/www/html

COPY ./devops/dev/php/php.ini /usr/local/etc/php/php.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
