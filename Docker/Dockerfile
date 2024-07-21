FROM php:8.2.0-fpm-alpine

RUN mkdir -p /var/www/html

ARG PHP_EXTENSIONS="dom exif gd intl mysqli opcache pdo_mysql pdo_sqlite soap xsl zip pcntl"

# Download browscap.ini
RUN mkdir /var/lib/browscap \
    && wget http://browscap.org/stream?q=BrowsCapINI -O /var/lib/browscap/browscap.ini

# Install dependencies
RUN apk add --update \
		acl \
		apk-cron \
		augeas-dev \
		autoconf \
		bash \
		curl \
		ca-certificates \
		dialog \
		freetype-dev \
		gomplate \
		git \
		gcc \
		icu-dev \
		libcurl \
		libffi-dev \
		libgcrypt-dev \
		libjpeg-turbo-dev \
		libmcrypt-dev \
		libpng-dev \
        libwebp-dev \
		libpq \
		libressl-dev \
		libxslt-dev \
		libzip-dev \
		linux-headers \
		make \
		musl-dev \
		mysql-client \
		nginx \
		openssh-client \
		ssmtp \
		sqlite-dev \
		supervisor \
		su-exec \
		wget \
        logrotate \
		&& \
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp && \
    docker-php-ext-install $PHP_EXTENSIONS

RUN pecl install redis
RUN docker-php-ext-enable redis

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer



CMD ["php-fpm"]
