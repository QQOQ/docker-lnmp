FROM php:7.4-fpm-alpine

COPY custom.php.ini /usr/local/etc/php/conf.d/docker-php-custom.ini

RUN apk add autoconf g++ make util-linux-dev re2c libpng-dev icu-dev freetype-dev \
        openssl-dev pcre-dev jpeg-dev libtool imagemagick imagemagick-dev postgresql-dev tzdata linux-headers git sudo libbsd libxml2-dev libzip-dev \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN pecl install redis
RUN docker-php-ext-enable redis

RUN docker-php-ext-install gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install soap \
    && docker-php-ext-install bcmath \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

USER www-data

#RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
    #&& composer global require "hirak/prestissimo" \
    #&& composer global require "fxp/composer-asset-plugin" \
    #&& composer global require "symfony/var-dumper"

#USER root

#RUN echo "auto_prepend_file = \"/home/www-data/.composer/vendor/autoload.php\"" > /usr/local/etc/php/conf.d/docker-php-composer.ini

VOLUME /Documents

WORKDIR /Documents