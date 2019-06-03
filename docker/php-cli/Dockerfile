FROM php:7.0.30-cli

LABEL maintainer="weifeng <910099271@qq.com>"

ARG TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libmemcached-dev \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libssl-dev \
        libmcrypt-dev

RUN apt-get install -y --no-install-recommends \
        zip \ 
        unzip \
        git \
        wget \
        vim \
        nano \
        procps

# MYSQL
RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql

# MCRYPT
RUN docker-php-ext-install mcrypt

# GD
# RUN docker-php-ext-configure gd \
#         --enable-gd-native-ttf \
#         --with-jpeg-dir=/usr/lib \
#         --with-freetype-dir=/usr/include/freetype2 && \
#     docker-php-ext-install gd

# COMPOSER
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
#RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

# XDEBUG
#RUN export http_proxy=http://172.23.149.241:1080 && export https_proxy=http://172.23.149.241:1080
#RUN pecl install xdebug && \
#    docker-php-ext-enable xdebug
#COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# PHPUNIT
RUN wget http://phar.phpunit.cn/phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit

# CRONTAB
RUN apt-get install -y cron
COPY ./cron.d /etc/cron.d
RUN chmod -R 644 /etc/cron.d

# SUPERVISOR
RUN apt-get install -y supervisor
COPY supervisord.conf /etc/supervisord.conf

# ACME
# RUN curl https://get.acme.sh | sh 
# RUN mkdir /root/.acme.sh/certs && echo "CERT_HOME='/root/.acme.sh/certs'" >> /root/.acme.sh/account.conf

RUN rm -rf /var/lib/apt/lists/* && apt-get clean

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www/html

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]