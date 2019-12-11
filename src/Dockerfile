FROM php:7.4.0-fpm

#entrypoint
COPY docker-php-entrypoint /usr/local/bin/docker-php-entrypoint
RUN chmod a+x /usr/local/bin/docker-php-entrypoint \
	&& apt-get update && apt-get install -y --no-install-recommends \
	procps \
	git \
	unzip \
	libzip-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	#redis
	&& pecl install redis \
	&& docker-php-ext-enable redis \
	#mysql
	&& docker-php-ext-install -j$(nproc) mysqli pdo_mysql \
	#gd
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
	#zip
	&& docker-php-ext-install -j$(nproc) zip \
	#composer
	&& COMPOSER_DOWNLOAD_URL="https://getcomposer.org/composer.phar" \
	&& curl -o /usr/local/bin/composer ${COMPOSER_DOWNLOAD_URL} \
	&& chmod a+x /usr/local/bin/composer
