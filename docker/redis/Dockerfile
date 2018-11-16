FROM redis:4.0.10

LABEL maintainer="weifeng <910099271@qq.com>"

ARG TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY ./redis.conf /usr/local/etc/redis/redis.conf
ARG REDIS_PASSWORD=root
RUN sed -i 's/^requirepass root/requirepass $REDIS_PASSWORD/' /usr/local/etc/redis/redis.conf

CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]

EXPOSE 6379