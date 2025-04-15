FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

ARG PHP_VERSION=8.3
ARG NODE_VERSION=18
ARG PYTHON_VERSION=3.11
ARG ENABLE_APACHE_MODS=rewrite
ARG PHP_MODULES="mysqli pdo pdo_mysql"
ARG COMPOSER_INSTALL=true
ARG APACHE_PRESET=none

RUN apt-get update && apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php -y && \
    apt-get update

RUN apt-get install -y \
    apache2 \
    php${PHP_VERSION} \
    php${PHP_VERSION}-cli \
    php${PHP_VERSION}-common \
    php${PHP_VERSION}-mysql \
    libapache2-mod-php${PHP_VERSION} \
    python${PYTHON_VERSION} python3-pip \
    nodejs npm \
    curl git unzip && \
    a2enmod rewrite

# COPY apache /etc/apache2/custom-conf
# COPY /apache-presets /etc/apache2/custom-conf
COPY config/docker-web/apache /etc/apache2/custom-conf


RUN cat /etc/apache2/custom-conf/base.conf > /etc/apache2/sites-available/000-default.conf && \
    if [ "$APACHE_PRESET" != "none" ] && [ -f "/etc/apache2/custom-conf/${APACHE_PRESET}.conf" ]; then \
        echo "\n# Caricamento preset: ${APACHE_PRESET}" && \
        cat /etc/apache2/custom-conf/${APACHE_PRESET}.conf >> /etc/apache2/sites-available/000-default.conf ; \
    fi

RUN if [ "$COMPOSER_INSTALL" = "true" ]; then \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    fi

WORKDIR /var/www/html

EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
