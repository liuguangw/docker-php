FROM php:8.1-fpm-alpine

#entrypoint
COPY docker-php-entrypoint /usr/local/bin/docker-php-entrypoint
RUN chmod a+x /usr/local/bin/docker-php-entrypoint \
	&& apk add --no-cache --virtual .build-deps \
	autoconf \
	g++ \
	gcc \
	make \
	# persistent / runtime deps
	&& apk add --no-cache \
	libzip-dev \
	freetype-dev \
	jpeg-dev \
	libpng-dev \
	#redis
	&& pecl install redis \
	&& docker-php-ext-enable redis \
	#mysql
	&& docker-php-ext-install -j$(nproc) mysqli pdo_mysql \
	#gd
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd \
	#zip
	&& docker-php-ext-install -j$(nproc) zip \
	#composer
	&& COMPOSER_DOWNLOAD_URL="https://getcomposer.org/download/1.10.22/composer.phar" \
	&& curl -o /usr/local/bin/composer ${COMPOSER_DOWNLOAD_URL} \
	&& chmod a+x /usr/local/bin/composer \
	&& apk del --no-network .build-deps \
	&& php -m
