# From official php image.
FROM php:8.0-fpm-alpine
# Install postgres pdo driver.
RUN apk add --no-cache postgresql-dev && docker-php-ext-install pdo_pgsql
RUN apk add --no-cache \
        apache2 \
        php7 \
        php7-common \
        php7-apache2 \
        php7-curl \
        php7-ldap \
        php7-mysqli \
        php7-gd \
        php7-xml \
        php7-mbstring \
        php7-zip \
        php7-ctype \
        php7-tokenizer \
        php7-pdo_mysql \
        php7-openssl \
        php7-bcmath \
        php7-phar \
        php7-json \
        php7-iconv \
        php7-fileinfo \
        php7-simplexml \
        php7-session \
        php7-dom \
        php7-xmlwriter \
        php7-xmlreader \
        php7-sodium \
        php7-redis \
        curl \
        wget \
        vim \
        git \
        mysql-client \
        tini
# Install redis driver.
RUN mkdir -p /usr/src/php/ext/redis; \
    curl -fsSL --ipv4 https://github.com/phpredis/phpredis/archive/5.3.4.tar.gz | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
    docker-php-ext-install redis
