FROM php:8.0-apache

RUN apt update \
	&& apt install -y \
	g++ \
	libicu-dev \
	libpq-dev \
	libzip-dev \
	zip \
	zlib1g-dev \
	&& docker-php-ext-install \
	intl \
	opcache \
	pdo

RUN apt-get install -y git-core curl build-essential openssl libssl-dev \
	&& git clone https://github.com/nodejs/node.git \
	&& cd node \
	&& ./configure \
	&& make \
	&& sudo make install

WORKDIR /var/www/html

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
