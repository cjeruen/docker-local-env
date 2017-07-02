FROM php:7.1

COPY php.ini         /usr/local/etc/php/php.ini
COPY sources.list    /etc/apt/sources.list
COPY src/zan/zan-extension /usr/src/php/ext/zan
COPY php_swoole.h /usr/src/php/ext/zan/php_swoole.h

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng12-dev \
    libmcrypt-dev \
    libcurl4-openssl-dev \
    libssl-dev \

    && docker-php-ext-install -j$(nproc) mcrypt  \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) gd \

    # ext-ldap start
    && apt-get install -y libldb-dev libldap2-dev \
    && ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
    && ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so \
    && docker-php-ext-install -j$(nproc) ldap \
    # ext-ldap end

    # ext-imap start
    && apt-get install -y libc-client-dev libkrb5-dev \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap \
    # ext-imap end

    && pecl install redis \
    && docker-php-ext-enable redis \

    # cannot find -lhiredis_linux
    && apt-get install -y libhiredis-dev \
    && ln -s /usr/lib/x86_64-linux-gnu/libhiredis.so /usr/lib/libhiredis_linux.so \
    # cannot find -lhiredis_linux

    && docker-php-ext-install -j$(nproc) sockets \

    && docker-php-ext-configure zan --enable-sockets --enable-async-redis  --enable-openssl \
    && docker-php-ext-install -j$(nproc) zan \


    && rm -r /var/lib/apt/lists/*

EXPOSE 8030

WORKDIR /zan

# ENTRYPOINT ["php-fpm"]
ENTRYPOINT ["php", "bin/httpd"]
