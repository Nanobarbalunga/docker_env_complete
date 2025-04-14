FROM ubuntu:22.04

# Imposta variabili non interattive per evitare prompt durante l'installazione
ENV DEBIAN_FRONTEND=noninteractive

# Aggiornamento e installazione dei pacchetti base
RUN apt-get update && apt-get install -y \
    apache2 \
    php \
    php-mysql \
    libapache2-mod-php \
    python3 \
    python3-pip \
    nodejs \
    npm \
    curl \
    git \
    unzip \
    && apt-get clean

# Abilitazione moduli Apache necessari
RUN a2enmod rewrite

# Installazione di Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Imposta la directory di lavoro
WORKDIR /var/www/html

# Espone la porta 80
EXPOSE 80

# Avvia Apache in foreground
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
