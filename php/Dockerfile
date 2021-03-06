# see https://github.com/cmaessen/docker-php-sendmail for more information

FROM php:7.1-fpm

RUN apt-get update && apt-get install -q -y ssmtp mailutils zlib1g-dev libicu-dev g++ libpng-dev libjpeg62-turbo-dev libfreetype6-dev libmcrypt-dev libxslt-dev && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ 

RUN docker-php-ext-install pdo_mysql mysqli sysvsem intl zip intl gd mcrypt xsl bcmath soap mbstring json hash soap gd

RUN pecl install xdebug-2.5.5 \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "[XDebug]" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_log=/tmp/xdebug.log" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini

RUN echo "hostname=localhost.localdomain" > /etc/ssmtp/ssmtp.conf \
    && echo "root=root@localhost" >> /etc/ssmtp/ssmtp.conf \
    && echo "mailhub=maildev" >> /etc/ssmtp/ssmtp.conf \
    && echo "sendmail_path=sendmail -i -t" >> /usr/local/etc/php/conf.d/php-sendmail.ini

RUN echo "[Date]" >> /usr/local/etc/php/conf.d/php-sendmail.ini \
    && echo "date.timezone = Europe/Amsterdam" >> /usr/local/etc/php/conf.d/php-sendmail.ini

RUN echo "localhost localhost.localdomain" >> /etc/hosts