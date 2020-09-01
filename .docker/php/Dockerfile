FROM php:7.4-fpm

# 设置debian国内源
RUN sed -i 's/deb.debian.org/mirrors.163.com/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.163.com/g' /etc/apt/sources.list

# 安装依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    default-mysql-client \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmagickwand-dev \
    libzip-dev \
    libonig-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    && pecl install imagick \
    && pecl install redis

# 安装npm
RUN apt-get install -y nodejs npm

# 设置npm国内源
RUN npm config set registry https://registry.npm.taobao.org

# 清楚缓存
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# 安装扩展
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath opcache
RUN docker-php-ext-enable imagick redis

# 安装composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# 设置composer国内源
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# ubuntu 设置字符集
RUN echo fr_FR.UTF-8 UTF-8 > /etc/locale.gen && locale-gen

# 设置工作目录
WORKDIR /var/www

