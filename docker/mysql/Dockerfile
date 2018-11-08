FROM mysql:5.6.40

LABEL maintainer="weifeng <910099271@qq.com>"

ARG TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN chown -R mysql:root /var/lib/mysql/

COPY ./my.cnf /etc/mysql/conf.d/my.cnf

RUN echo "grant all on *.* to ${MYSQL_ROOT_PASSWORD}@'%' identified by '${MYSQL_ROOT_PASSWORD}';flush privileges;" > /docker-entrypoint-initdb.d/start.sql

CMD ["mysqld"]

EXPOSE 3306