FROM php:8.1-fpm

RUN apt-get update -y

RUN apt-get install -y --no-install-recommends \
	libgd-dev libsodium-dev libxslt1-dev libzip-dev \
    libpng++-dev libwebp-dev libjpeg-dev  \
    libjpeg62-turbo-dev libpng-dev unzip libzip-dev curl

RUN docker-php-ext-install opcache
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN docker-php-ext-install zip bcmath intl pdo_mysql soap sockets sodium xsl opcache

# install GD
RUN docker-php-ext-configure gd \
	#--with-png \
	--with-jpeg \
	--with-xpm \
	--with-webp \
	--with-freetype \
	&& docker-php-ext-install -j$(nproc) gd

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Clean up
RUN apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /magento