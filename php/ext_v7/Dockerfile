FROM php:7.1-fpm

COPY php.ini         /usr/local/etc/php/php.ini
COPY php-fpm.conf    /usr/local/etc/php-fpm.conf
COPY sources.list    /etc/apt/sources.list
COPY .bashrc         /root/.bashrc


ENTRYPOINT ["php-fpm"]
