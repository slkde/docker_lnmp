# 引入版本
ARG VERSION
FROM php:${VERSION}-fpm

# 引入其他变量
ARG VERSION
ARG TIMEZONE
ARG MIRRORS_URL
ARG COMPOSER_URL

LABEL maintainer="slkde@sina.com"
LABEL Description="使用官方容器，稍做修改。"

# 修改时区
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

# 修改源
RUN sed -i "s%deb.debian.org%${MIRRORS_URL}%g" /etc/apt/sources.list
RUN sed -i "s%security.debian.org/debian-security%${MIRRORS_URL}/debian-security%g" /etc/apt/sources.list

# 安装基本工具和相关依赖
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apt-utils \
    git \
    vim \
    zip \
    wget \
    curl \
    unzip \
    graphviz \
    net-tools \
    iputils-ping \
    openssh-client \
    openssh-server \
    libz-dev \
    libpq-dev \
    libzip-dev \
    zlib1g-dev \
    libbz2-dev \
    libicu-dev \
    libssl-dev \
    libpng-dev \
    libonig-dev \
    libjpeg-dev \
    libxml2-dev \
    libmcrypt-dev \
    libmemcached-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    && apt-get autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 安装PHP扩展
RUN if [ `expr $VERSION \> 7.3` -lt 1 ] ; then \
    docker-php-ext-configure gd --with-jpeg-dir=/usr/lib --with-freetype-dir=/usr/include/freetype2 ; \
    elif [ `expr $VERSION \> 8.0` -lt 1 ] ; then \
    docker-php-ext-configure gd --with-jpeg=/usr/lib --with-freetype=/usr/include/freetype2 ; \
    else docker-php-ext-configure gd --with-jpeg=/usr/lib --with-freetype=/usr/include/freetype2 ; \
    fi

RUN docker-php-ext-configure exif --enable-exif \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-install -j$(nproc) \
    gd \
    zip \
    intl \
    exif \
    soap \
    pcntl \
    bcmath \
    sockets \
    fileinfo \
    mbstring \
    pdo_mysql \
    opcache \
    && docker-php-ext-enable \
    # 开启扩展
    gd \
    zip \
    intl \
    exif \
    soap \
    pcntl \
    bcmath \
    sockets \
    fileinfo \
    mbstring \
    pdo_mysql \
    opcache

# 安装 Redis 扩展
RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

# 拷贝其他扩展
RUN mkdir -p /usr/local/lib/php/extensions/ext/
COPY --chown=www-data:www-data ./ext/${VERSION}/* /usr/local/lib/php/extensions/ext/
RUN mv /usr/local/lib/php/extensions/ext/* `php-config --extension-dir`

# 安装 Composer。将缓存挂载到宿主机
RUN mkdir -p /root/.composer/cache
RUN curl -sS https://install.phpcomposer.com/installer | php -- --install-dir=/usr/bin --filename=composer
RUN composer config -g repo.packagist composer ${COMPOSER_URL} \
    && composer self-update --2

# 更改权限。无法修改docker外挂载的目录权限。
RUN chown -R www-data:www-data /var/www/

VOLUME /root/.composer/cache

WORKDIR /var/www