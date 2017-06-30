FROM php:7.1-fpm

COPY php.ini         /usr/local/etc/php/php.ini
COPY php-fpm.conf    /usr/local/etc/php-fpm.conf
COPY sources.list    /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng12-dev \
    libmcrypt-dev \
    libcurl4-openssl-dev \
    && docker-php-ext-install -j$(nproc) mcrypt  \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) gd \
    && pecl install redis \
    && docker-php-ext-enable redis \
    # ext-ldap start
    && apt-get install -y libldb-dev libldap2-dev \
    && ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
    && ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so \
    && docker-php-ext-install -j$(nproc) ldap \
    # ext-ldap end
    # ext-imap start
    && apt-get install -y libc-client-dev libkrb5-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap
    # ext-imap end


ENTRYPOINT ["php-fpm"]
