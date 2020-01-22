#使用的基础镜像
FROM php:fpm
#作者
MAINTAINER houdunren.com@xiangjun 2300071698@qq.com
#时区
ENV TZ Asia/Shanghai
#换国内源
# RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
# RUN apt-get clean
# RUN apt-get update
#基本更新
RUN apt-get update && apt-get install -y \
    vim \
    curl \
    net-tools \
    iputils-ping \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev 
#安装GD扩展
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd
#安装REDIS/XDEBUG
RUN apt-get install -y libmemcached-dev zlib1g-dev
RUN pecl install redis-5.1.1 
RUN pecl install memcached 
RUN docker-php-ext-enable redis memcached 
#使用镜像中的生产环境PHP.INI配置文件
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
#添加自定义配置文件
COPY ./config/php.ini $PHP_INI_DIR/conf.d/php.ini
# #容器工作目录
# WORKDIR /html
