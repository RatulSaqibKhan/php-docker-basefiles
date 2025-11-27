FROM php:8.4-apache

LABEL maintainer="Md. Nazmus Saqib Khan <ratulkhan.jhenidah@gmail.com>"

# -------------------------------------------------------
# ----------- Apache Document Root Setup ----------------
# -------------------------------------------------------

ENV APACHE_DOCUMENT_ROOT=/var/www/html/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
    && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf

# -------------------------------------------------------
# ----------- System Dependencies ------------------------
# -------------------------------------------------------

ARG APT_DEPENDENCIES="git zip unzip curl libpng-dev libjpeg-dev libfreetype6-dev libonig-dev libxml2-dev libzip-dev libssl-dev libicu-dev supervisor"
ARG PHP_DOCKER_EXTENSIONS="gd pdo pdo_mysql mbstring intl xml zip sockets opcache"

RUN apt-get update && apt-get install -y ${APT_DEPENDENCIES}\
    && docker-php-ext-configure gd --with-jpeg --with-freetype \
    && docker-php-ext-install ${PHP_DOCKER_EXTENSIONS}\
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# -------------------------------------------------------
# ----------- Apache Modules -----------------------------
# -------------------------------------------------------
RUN a2enmod rewrite headers ssl

# -------------------------------------------------------
# ----------- Install Composer ---------------------------
# -------------------------------------------------------
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# -------------------------------------------------------
# ----------- PHP Configuration --------------------------
# -------------------------------------------------------
COPY ./php-apache/conf.d/php.ini        /usr/local/etc/php/conf.d/01-php.ini
COPY ./php-apache/conf.d/error.ini      /usr/local/etc/php/conf.d/02-error.ini
COPY ./php-apache/conf.d/opcache.ini    /usr/local/etc/php/conf.d/03-opcache.ini