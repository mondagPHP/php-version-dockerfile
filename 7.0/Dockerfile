# 7.0 其他版本 90M 左右
FROM php:7.0-alpine

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
    && apk --update add --no-cache \ 
    # Packages
    zip \
    curl \
    # gd
    libpng-dev \
    libjpeg-turbo-dev \
    && docker-php-ext-install bcmath opcache pcntl pdo_mysql \
    # gd
    gd \
    && install-php-extensions sockets zip redis-5.3.6 event-3.0.6 \
    # Clean up
    && rm -rf /var/cache/apk/*