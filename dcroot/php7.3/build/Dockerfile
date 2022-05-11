FROM php:7.3-fpm

RUN apt-get update && apt-get install -y git && git config --global user.name "bingo110" && git config --global user.email "977856041@qq.com" && apt-get install -y vim && apt-get install unzip -y && apt-get install -y wget  
#CA 证书
RUN wget -P /usr/lib/ssl/ http://curl.haxx.se/ca/cacert.pem && chmod 744 /usr/lib/ssl/cacert.pem
#xdebug
RUN pecl install xdebug-2.8.1 && docker-php-ext-enable xdebug

RUN apt-get install -y --no-install-recommends \
  autoconf \
  build-essential \
  apt-utils \
  zlib1g-dev \
  libzip-dev \
  zip \
  libmagick++-dev \
  libmagickwand-dev \
  libpq-dev \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  libwebp-dev \ 
  libxpm-dev \
  libxslt-dev
# magento 需要的 扩展
RUN docker-php-ext-configure gd \
  --with-png-dir=/usr/include/ \
  --with-jpeg-dir=/usr/include/ \
  --with-freetype-dir=/usr/include/

RUN docker-php-ext-configure zip --with-libzip

RUN docker-php-ext-install gd intl pdo_mysql pdo_pgsql mysqli zip xsl bcmath soap

# redis 扩展
RUN pecl install redis-5.0.0 && docker-php-ext-enable redis 

RUN apt remove -y --auto-remove  \
    && apt-get autoremove && apt-get autoclean \
    && rm  -rf /var/lib/apt/lists/*

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /data/wwwroot
#安装composer
RUN curl -sS https://getcomposer.org/installer | php \    
        && mv composer.phar /usr/local/bin/composer  \    
        && composer config -g repo.packagist composer https://packagist.phpcomposer.com
