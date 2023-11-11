FROM unit:1.31.0-php8.2

RUN apt update  \
    && apt install -y libicu-dev libpq5 libpq-dev git zip unzip libzip-dev libpng-dev libgmp-dev libmagickwand-dev libwebp-dev cron \
    && docker-php-ext-install pdo pdo_pgsql bcmath sockets zip sysvsem intl exif gmp opcache \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin \
    && php -r "unlink('composer-setup.php');" \
    && mv /usr/bin/composer.phar /usr/bin/composer

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install gd

RUN mkdir -p /usr/src/php/ext/redis; \
	curl -fsSL https://pecl.php.net/get/redis --ipv4 | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
	docker-php-ext-install redis;
