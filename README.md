# docker lnmp

### php      -- 5.6 -- 7.2 -- 7.4 -- 8.0
### nginx    -- 1.20
### mysql    -- 5.7 -- 8.0
### redis    -- 5.0 -- 6.0

### 说明：
个人感觉十分简洁好用的lnmp环境。欢迎大家使用，以及提出意见。

推荐在windows使用[wsl---windows subsystem for linux](https://github.com/slkde/wsl)。

推荐使用[vscode](https://github.com/slkde/vscode) 点击连接远程，点击remote-containers: attach to running container
### 使用方法：
国内：
```
git clone git@gitee.com:slkde/docker_lnmp.git
```
国外：
```
git clone git@github.com:slkde/docker_lnmp.git
```
进入目录：
```
cd docker_lnmp
```
将环境变量文件.env.example复制为.env
```
cp .env.example .env
```
构建：
```
docker-compose build
```
启动：
```
docker-compose up -d
```
开机：
```
docker-compose start
```
关机：
```
docker-compose stop
```
### 其他说明：
```
docker-compose build
docker-compose up -d
docker-compose stop
docker-compose start
docker-compose restart
```
### 在windows中使用时，请一定先把mysql的配置文件my.cnf设置为只读文件。不然mysql会忽略配置文件。或者直接在docker-compose.yml文件中将my.cnf文件映射注释掉。
```
build/mysql/etc/my.cnf
```
### 在wsl中使用时，wsl每次启动都有不同的ip，不要被迷惑，wsl和windows的ip都可以用，直接使用windows的ip和hosts即可。

### 修改nginx配置文件后，重启nginx。
```
docker-compose restart nginx
```
### 修改php配置文件后，重启php
```
docker-compose restart php
```
### 如果虚拟网络有问题或重名。请删除重名的网络。
```
docker network ls

docker network rm docker_docker_lnmp
```
### 删除容器
```
docker-compose down --rmi all
```
## 目录结构：

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

docker_[php](https://hub.docker.com/_/php)

docker_[nginx](https://hub.docker.com/_/nginx)

docker_[mysql](https://hub.docker.com/_/mysql)

docker_[redis](https://hub.docker.com/_/redis)