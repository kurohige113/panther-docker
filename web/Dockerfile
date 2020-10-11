FROM php:7.3.20-apache-stretch

# ドキュメントルートをデフォルトから修正
ENV APACHE_DOCUMENT_ROOT /var/www/panther/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN ["apt-get", "update"]
RUN apt-get install -y \
libzip-dev \
zip \
unzip \
vim \
&& docker-php-ext-install zip

# install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 環境変数設定
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# install Laravel
RUN composer global require "laravel/installer"

# Laravelで必要になるmodRewriteを有効化する
RUN mv /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled
RUN /bin/sh -c a2enmod rewrite

WORKDIR /var/www/panther