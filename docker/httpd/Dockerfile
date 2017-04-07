FROM ubuntu:xenial

ARG USER_ID=1000
ARG GROUP_ID=1000

RUN apt-get update && apt-get install -y \
    curl \
    git \
    vim \
    apache2 \
    libapache2-mod-php \
    php7.0-cli \
    php7.0-intl \
    php-xdebug

COPY bin/apache2-foreground /usr/bin/
COPY conf/apache2.conf /etc/apache2/

RUN rm -rf /var/www/html /etc/apache2/sites-enabled/* /etc/apache2/conf-enabled/* && \
    mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www && \
    chown -R www-data:www-data /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www && \
    a2dismod mpm_event && \
    a2enmod rewrite && \
    a2enmod mpm_prefork && \
    a2enmod php7.0 && \
    a2enmod headers && \
    usermod -u $USER_ID www-data && \
    groupmod -g $GROUP_ID www-data

COPY conf/90-php-development.ini /etc/php/7.0/apache2/conf.d/
COPY conf/90-php-development.ini /etc/php/7.0/cli/conf.d/

WORKDIR /var/www

EXPOSE 80

CMD ["apache2-foreground"]
