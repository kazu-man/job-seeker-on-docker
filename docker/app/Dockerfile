# どんなdockerイメージを利用して構築をするか
FROM php:7.4-apache

# 設定ファイルをdockerコンテナ内のPHP、Apacheに読み込ませる
ADD php.ini /usr/local/etc/php/
ADD 000-default.conf /etc/apache2/sites-enabled/
ENV APACHE_LOG_DIR="/var/log/apache2"
# Composerのインストール
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# ミドルウェアインストール
RUN apt-get update \
&& apt-get install -y \
git \
zip \
unzip \
vim \
libpng-dev \
libpq-dev \
&& docker-php-ext-install pdo_mysql

# Laravelで必要になるmodRewriteを有効化する
RUN mv /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled
RUN /bin/sh -c a2enmod rewrite

# npmのインストール
RUN apt-get install -y \
    curl \
    gnupg
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g

RUN rm /var/log/apache2/access.log \
    rm /var/log/apache2/error.log \
    rm /var/log/apache2/other_vhosts_access.log \
    touch /var/log/apache2/access.log \
    touch /var/log/apache2/error.log \
    touch /var/log/apache2/other_vhosts_access.log \
