# 8.1 150M 左右
FROM php:8.1-cli-alpine3.15 as main

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk --update add --no-cache \ 
    # Packages
    # git \
    zip \
    curl \
    # zip
    libzip-dev \
    # gd
    libpng-dev \
    && docker-php-ext-install bcmath opcache pcntl pdo_mysql \
    # sockets
    && CFLAGS="$CFLAGS -D_GNU_SOURCE" docker-php-ext-install sockets \
    # zip
    zip \
    # gd
    gd \
    # redis
    #&& mkdir -p /usr/src/php/ext/redis \
	#&& curl -fsSL https://pecl.php.net/get/redis-5.3.6.tgz --ipv4 | tar xvz -C "/usr/src/php/ext/redis" \
	#&& docker-php-ext-install redis \
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
	# Clean up
    && rm -rf /var/cache/apk/*

    