# docker lnmp

### php      -- 5.6 -- 7.2 -- 7.4 -- 8.0
### nginx    -- 1.20
### mysql    -- 5.7 -- 8.0
### redis    -- 5.0 -- 6.0

>build
>
>>mysql
>>>etc
>>
>>nginx
>>>etc
>>
>>php
>>>5.6
>>>
>>>7.2
>>>
>>>7.4
>>>
>>>8.0
>>>
>>>ext--其他php扩展
>>
>>redis
>>>etc
>>
>data
>>mysql--MySQL数据库目录
>>
>>nginx--证书，网站配置
>>
>>redis--redis数据库目录
>
>tmp
>>.composer--composer缓存
>>
>>logs--日志目录
>>
>>run--sock文件目录
>
>www--项目目录

#### php配置文件
build/php/v/php/php.ini

build/php/v/php/conf.d/

build/php/v/php-fpm.d/

#### nginx配置文件
build/nginx/etc/nginx.conf

build/nginx/etc/conf.d/

#### my sql配置文件
build/mysql/etc/my.cnf

build/mysql/etc/conf.d/

#### redis配置文件
build/redis/etc/redis.conf

#### 网站配置文件
data/nginx/*.conf

#### https证书
data/nginx/certs/

## 说明：

1. php使用sock连接。
   
    -配置文件www.conf，第36行。zz-docker.conf第6行
2. 编辑docker-php-ext-all.ini开启php扩展
   
    -有些扩展可以拷贝到build/php/ext/下。
3. https证书位置/data/nginx/conf.d/certs/

[php](https://hub.docker.com/_/php)

[nginx](https://hub.docker.com/_/nginx)

[mysql](https://hub.docker.com/_/mysql)

[redis](https://hub.docker.com/_/redis)