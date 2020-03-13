FROM ubuntu:latest

RUN apt-get update && apt-get upgrade -y

RUN apt install -y software-properties-common

RUN apt install -y language-pack-en-base

RUN apt-get install -y iputils-ping

RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN echo "Europe/Moscow" > /etc/timezone
RUN apt-get install tzdata -y
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get install -y php7.3 php7.3-cli php7.3-common php7.3-json php7.3-opcache php7.3-mysql php7.3-mbstring \
    php7.3-zip php7.3-fpm php7.3-dev php7.3-pgsql php7.3-amqp php7.3-xml php7.3-intl php7.3-curl php7.3-bcmath \
    php7.3-gd php7.3-imagick php7.3-igbinary php7.3-sqlite3 php7.3-xdebug php7.3-redis

RUN pecl install timezonedb \
    && echo "extension=timezonedb.so" > /etc/php/7.3/mods-available/timezonedb.ini \
    && phpenmod timezonedb

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

RUN apt-get install -y git

RUN  apt-get install -y supervisor

RUN mkdir /run/php

WORKDIR /app

EXPOSE 9000

RUN echo "listen = 0.0.0.0:9000" >> /etc/php/7.3/fpm/pool.d/www.conf
RUN echo "xdebug.remote_enable=1" >> /etc/php/7.3/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_connect_back=1" >> /etc/php/7.3/fpm/conf.d/20-xdebug.ini

CMD ["php-fpm7.3", "--nodaemonize"]
