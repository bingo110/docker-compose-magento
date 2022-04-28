FROM composer

#全局代理
#RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

#局部项目代理 composer config repo.packagist composer https://mirrors.aliyun.com/composer/

WORKDIR /data/wwwroot