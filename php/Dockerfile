FROM php:7.4-fpm-alpine

EXPOSE 9000

COPY custom.php.ini /usr/local/etc/php/conf.d/docker-php-custom.ini

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk add --update-cache --no-cache \
        autoconf g++ make util-linux-dev re2c libpng-dev icu-dev freetype-dev \
        openssl-dev pcre-dev jpeg-dev libtool imagemagick imagemagick-dev postgresql-dev tzdata linux-headers git sudo libbsd libxml2-dev libzip-dev \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN git clone https://git.php.net/repository/pecl/database/mysql.git \
    && cd mysql \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && rm -rf mysql \
    && pecl install redis \
    && pecl install uuid \
    && pecl install xdebug \
    && pecl install mongodb \
    && pecl install imagick \
    && pecl install swoole \
    && docker-php-ext-enable mysql redis uuid xdebug mongodb imagick swoole

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install soap \
    && docker-php-ext-install bcmath \
    && curl -o /usr/local/bin/composer https://mirrors.aliyun.com/composer/composer.phar \
    && chmod +x /usr/local/bin/composer

USER www-data

RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer global require "hirak/prestissimo" \
    && composer global require "fxp/composer-asset-plugin" \
    && composer global require "symfony/var-dumper"

USER root

RUN echo "auto_prepend_file = \"/home/www-data/.composer/vendor/autoload.php\"" > /usr/local/etc/php/conf.d/docker-php-composer.ini

VOLUME /Documents

WORKDIR /Documents