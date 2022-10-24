# # From official php image.
FROM php:7.4.16-fpm-alpine3.12
# Install postgres pdo driver.
RUN apk add --no-cache postgresql-dev \
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
php7-redis

# RUN docker-php-ext-install ext-fileinfo ext-pdo ext-simplexml ext-tokenizer ext-dom ext-sodium ext-bcmath

# Install redis driver.
RUN mkdir -p /usr/src/php/ext/redis; \
    curl -fsSL --ipv4 https://github.com/phpredis/phpredis/archive/5.3.4.tar.gz | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
    docker-php-ext-install redis

RUN set -eux; \
	docker-php-ext-enable opcache; \
	{ \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini
# https://wordpress.org/support/article/editing-wp-config-php/#configure-error-logging
RUN { \
# https://www.php.net/manual/en/errorfunc.constants.php
# https://github.com/docker-library/wordpress/issues/420#issuecomment-517839670
		echo 'error_reporting = E_ERROR | E_WARNING | E_PARSE | E_CORE_ERROR | E_CORE_WARNING | E_COMPILE_ERROR | E_COMPILE_WARNING | E_RECOVERABLE_ERROR'; \
		echo 'display_errors = Off'; \
		echo 'display_startup_errors = Off'; \
		echo 'log_errors = On'; \
		echo 'error_log = /dev/stderr'; \
		echo 'log_errors_max_len = 1024'; \
		echo 'ignore_repeated_errors = On'; \
		echo 'ignore_repeated_source = Off'; \
		echo 'html_errors = Off'; \
	} > /usr/local/etc/php/conf.d/error-logging.ini

# Install php extensions inside docker containers easily
# https://github.com/mlocati/docker-php-extension-installer
COPY --from=mlocati/php-extension-installer:1.2.19 /usr/bin/install-php-extensions /usr/local/bin/
RUN set -eux; \
    install-php-extensions \
        bcmath \
        gd \
        ldap \
        mysqli \
        pdo_mysql \
        zip; \
    rm -f /usr/local/bin/install-php-extensions; \
    # Install prerequisites packages
    apk add --no-cache \
        mysql-client

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
