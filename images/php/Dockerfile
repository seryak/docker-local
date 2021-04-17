# Для начала указываем исходный образ, он будет использован как основа
FROM php:7.4-apache

# нода и yarn
RUN curl -sL https://deb.nodesource.com/setup_15.x | bash -
RUN apt-get update && apt-get install -y nodejs
RUN npm install -g yarn && npm config set cache /var/www/html/.npm --global


# устанавливаем дополнительный софт
RUN apt-get update && apt-get install -y \
        libpq-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        zlib1g-dev \
        libzip-dev \
        libtidy-dev \
        libonig-dev \
        libicu-dev \
        libaio1 \
        g++ \
        wget \
        rsync \
        git \ 
        zip \ 
        unzip \ 
        libpng-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install -j$(nproc) mbstring zip pdo_mysql pdo_pgsql tokenizer iconv mysqli tidy gd exif opcache \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \




# Java Oracle Driver
RUN mkdir /opt/oracle \
    && cd /opt/oracle \
    && wget http://wtolk.ru/demo/oracle/instantclient-basic-linux.x64.zip \
    && wget http://wtolk.ru/demo/oracle/instantclient-sdk-linux.x64.zip \
    && wget http://wtolk.ru/demo/oracle/instantclient-sqlplus-linux.x64.zip \
    && unzip /opt/oracle/instantclient-basic-linux.x64.zip -d /opt/oracle \
    && unzip /opt/oracle/instantclient-sdk-linux.x64.zip -d /opt/oracle \
    && rm -rf /opt/oracle/*.zip \
    && docker-php-ext-configure oci8 --with-oci8=instantclient,/opt/oracle/instantclient_21_1 \
    && docker-php-ext-install oci8 \
    && echo /opt/oracle/instantclient_21_1/ > /etc/ld.so.conf.d/oracle-insantclient.conf \
    && ldconfig












RUN apt-get install -y locales locales-all
ENV LC_ALL ru_RU.UTF-8
ENV LANG ru_RU.UTF-8
ENV LANGUAGE ru_RU.UTF-8


# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN wget http://robo.li/robo.phar
RUN chmod +x robo.phar && mv robo.phar /usr/bin/robo
# PHP Deployr
RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep

# Необязательная строка с указанием автора образа
MAINTAINER wtolk <web@wtolk.ru>

# Apache modules
RUN a2enmod rewrite
