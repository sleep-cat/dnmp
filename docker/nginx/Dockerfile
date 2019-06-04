FROM nginx:1.14.2

LABEL maintainer="weifeng <910099271@qq.com>"

ARG TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY ./sources.list /etc/apt/sources.list

# COPY nginx.conf /etc/nginx/nginx.conf

WORKDIR /var/www/html

EXPOSE 80

# CMD ["nginx", "-g", "daemon off;"]
