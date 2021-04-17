# Для начала указываем исходный образ, он будет использован как основа
FROM php:5.6-apache

# устанавливаем дополнительный софт
RUN apt-get update && apt-get install -y \
        libpq-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        zlib1g-dev \
        libzip-dev \
        libicu-dev \
        g++ \
        wget \
        rsync \
        git \ 
        zip \ 
        unzip \ 
        libmcrypt-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install -j$(nproc) mbstring pdo_mysql pdo_pgsql mcrypt tokenizer iconv mysqli \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 

# Куда же без composer'а.
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN wget http://robo.li/robo.phar
RUN chmod +x robo.phar && mv robo.phar /usr/bin/robo

RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep


ENV PANTHER_NO_SANDBOX 1

# Необязательная строка с указанием автора образа
MAINTAINER wtolk <web@wtolk.ru>

# Apache modules
RUN a2enmod rewrite
