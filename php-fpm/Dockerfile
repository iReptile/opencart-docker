FROM php:8.2-fpm

ADD ./opencart.ini /usr/local/etc/php/conf.d
ADD ./opencart.pool.conf /usr/local/etc/php-fpm.d/

RUN apt-get update && apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng-dev \
	libzip-dev \
    curl 

RUN apt-get install -y libmcrypt-dev
RUN pecl install mcrypt-1.0.6 && docker-php-ext-enable mcrypt

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
	zip \
	pdo_mysql \
	mysqli \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd

RUN usermod -u 1000 www-data

WORKDIR /var/www/opencart

CMD ["php-fpm"]

EXPOSE 9000
