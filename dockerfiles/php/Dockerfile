FROM php:7.1-fpm-alpine

# 更改安装源 && 安装基础库 && 安装PHP扩展
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --no-cache libmcrypt-dev freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev curl rsync git openssh-client $PHPIZE_DEPS \
    && docker-php-ext-install pdo_mysql gd opcache pcntl bcmath mysqli zip posix \
    && docker-php-ext-enable mysqli

# 安装PECL扩展
RUN pecl install https://pecl.php.net/get/xdebug-2.9.6.tgz \
    && pecl install https://pecl.php.net/get/redis-5.2.2.tgz \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-enable redis

# Install Composer
#ENV COMPOSER_HOME /data/web
RUN curl -sS https://install.phpcomposer.com/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer global require "spatie/async" \
    && composer global require "xobotyi/rsync" \
    && composer global require "monolog/monolog"

# 移除基础库 && 清理不用缓存
RUN apk del --no-cache libmcrypt-dev freetype-dev libpng-dev libjpeg-turbo-dev \
    && rm -rf /tmp/* /usr/local/lib/php/doc/* /var/cache/apk/* 
