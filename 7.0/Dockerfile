#7.0 130M 左右
FROM php:7.0-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
    && apk --update add --no-cache \ 
    # Packages
    zip \
    curl \
    # zip
    libzip-dev \
    # gd
    libpng-dev \
    libjpeg-turbo-dev \
    && docker-php-ext-install bcmath opcache pcntl pdo_mysql sockets \
    # zip
    zip \
    # gd
    gd \
    # redis
    && curl -fsSL 'https://pecl.php.net/get/redis-5.3.6.tgz' -o redis.tar.gz \
    && mkdir -p /tmp/redis \
    && tar -xf redis.tar.gz -C /tmp/redis --strip-components=1 \
    && rm redis.tar.gz \
    && docker-php-ext-configure /tmp/redis --enable-redis \
    && docker-php-ext-install /tmp/redis \
    && rm -r /tmp/redis \
    # event
    && apk --update add --no-cache libevent-dev openssl-dev \
    && curl -fsSL 'https://pecl.php.net/get/event-3.0.6.tgz' -o event.tar.gz \
    && mkdir -p /tmp/event \
    && tar -xf event.tar.gz -C /tmp/event --strip-components=1 \
    && rm event.tar.gz \
    && docker-php-ext-install /tmp/event \
    && rm -r /tmp/event \
    && mv "$PHP_INI_DIR/conf.d/docker-php-ext-event.ini" "$PHP_INI_DIR/conf.d/docker-php-ext-zevent.ini" \
    ## composer
    && php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer \
	# Clean up
    && rm -rf /var/cache/apk/*