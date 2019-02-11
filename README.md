## 介绍
基于Docker构建PHP开发环境( Docker + Nginx + MySQL + PHP7 + REDIS )

## 安装(LINUX)
1. 安装docker  
```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```
> https://www.docker.com/get-started

2. 安装docker-compose  
```
curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
```
> https://docs.docker.com/compose/install/#install-compose

3. 启动Dnmp  
```
git clone https://github.com/sleep-cat/dnmp
cd dnmp

#启动
docker-compose up -d

#关闭
docker-compose down

```

## 说明
### Mysql
* 调整权限允许root远程登陆mysql `./docker/mysql/docker-entrypoint-initdb.d/remote.sql`
* 连接地址:mysql 连接密码:root 配置示例:
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=test
DB_USERNAME=root
DB_PASSWORD=root
```
### Redis
* 连接地址:redis 连接密码:root 配置示例:
```
REDIS_HOST=redis
REDIS_PASSWORD=root
REDIS_PORT=6379
```

### Work
* 默认目录: `./www`映射目录`/var/www`
* composer: `docker exec dnmp-work composer`
* phpunit: `docker exec dnmp-work phpunit`

### 命令
* 进入指定容器: `docker exec -it dnmp-nginx sh`
* 查看容器状态: `docker-compose ps`
* 查看容器日志: `docker-compose logs -f`

## 版本
* nginx:1.14.0
* php:7.0.30-fpm
* work:7.0.30-cli+supervisor
* mysql:5.6.40
* redis:4.0.10