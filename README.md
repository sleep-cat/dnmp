#### 项目介绍
Docker环境下构造PHP开发环境  
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
git clone https://gitee.com/shanyu/dnmp.git
cd dnmp
docker-compose up -d --build
```

#### 使用说明
##### mysql
* `./docker/mysql/docker-entrypoint-initdb.d/remote.sql`调整权限允许root远程登陆mysql
* 默认密码 root
##### redis
* 默认密码 root
##### php-work
* 默认目录: `./www`映射目录`/var/www`
* composer: `docker exec dnmp-work composer`
* phpunit: `docker exec dnmp-work phpunit`

#### 常用命令
* 进入指定容器: `docker exec -it dnmp_nginx sh`
* 查看容器状态: `docker-compose ps`
* 查看容器日志: `docker-compose logs -f`

#### 程序版本
* nginx:1.14.0
* php:7.0.30-fpm
* php:7.0.30-cli
* mysql:5.6.40
* redis:4.0.10