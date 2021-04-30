# 引入版本
ARG VERSION
FROM nginx:${VERSION}

# 引入其他变量
ARG MIRRORS_URL
ARG TIMEZONE

LABEL maintainer="slkde@sina.com"
LABEL Description="使用官方容器，稍做修改。"

# 修改时区
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

# 修改源
RUN sed -i "s%deb.debian.org%${MIRRORS_URL}%g" /etc/apt/sources.list
RUN sed -i "s%security.debian.org/debian-security%${MIRRORS_URL}/debian-security%g" /etc/apt/sources.list

# 安装基本工具
# RUN apt-get update \
#     && apt-get install -y --no-install-recommends \
#     apt-utils \
#     vim \
#     wget \
#     curl \
#     && apt-get autoremove \
#     && apt-get clean \
#     && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www

# 更改权限。无法修改docker外挂载的目录权限。
RUN chown -R www-data:www-data /var/www/ /var/log/nginx/

WORKDIR /var/www