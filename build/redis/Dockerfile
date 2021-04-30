# 引入版本
ARG VERSION
FROM redis:${VERSION}

# 引入其他变量
ARG MIRRORS_URL
ARG TIMEZONE

LABEL maintainer="slkde@sina.com"
LABEL Description="使用官方容器，稍做修改。"

# 修改时区
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

# 修改源
# RUN sed -i "s%deb.debian.org%${MIRRORS_URL}%g" /etc/apt/sources.list
# RUN sed -i "s%security.debian.org/debian-security%${MIRRORS_URL}/debian-security%g" /etc/apt/sources.list

# CMD [ "redis-server", "/etc/redis/redis.conf" ]

# EXPOSE 6379