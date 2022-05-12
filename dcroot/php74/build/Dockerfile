FROM registry.cn-beijing.aliyuncs.com/kokofirst/php:7.4-fpm-general

RUN echo "deb http://mirrors.aliyun.com/debian/ buster main non-free contrib \n \
    deb-src http://mirrors.aliyun.com/debian/ buster main non-free contrib \n \
    deb http://mirrors.aliyun.com/debian-security buster/updates main \n \
    deb-src http://mirrors.aliyun.com/debian-security buster/updates main \n \
    deb http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib \n \
    deb-src http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib \n \
    deb http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib \n \
    deb-src http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib" > /etc/apt/sources.list \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug

#RUN usermod -s /bin/bash www-data \
#    && php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
#    && php composer-setup.php \
#    && php -r "unlink('composer-setup.php');" \
#    && mv composer.phar /bin/composer \
#    && composer config -g repo.packagist composer https://packagist.phpcomposer.com

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#RUN usermod -u 2200 www-data && groupmod -g 2200 www-data

WORKDIR /data/wwwroot
RUN apt-get update && apt-get install -y git && git config --global user.name "yubin" && git config --global user.email "bin.yu10@pactera.com" && apt-get install -y vim && apt-get install unzip -y && apt-get install wget -y
#CA 证书
RUN wget -P /usr/lib/ssl/ http://curl.haxx.se/ca/cacert.pem && chmod 744 /usr/lib/ssl/cacert.pem
#RUN cp /share-data/dev_CA.crt /usr/local/share/ca-certificates && update-ca-certificates
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \    
        && php composer-setup.php \    && php -r "unlink('composer-setup.php');" \    
        && mv composer.phar /bin/composer \    
        && composer config -g repo.packagist composer https://packagist.phpcomposer.com
