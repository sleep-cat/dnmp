FROM nginx:1.14.0

LABEL maintainer="weifeng <910099271@qq.com>"

ARG TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY nginx.conf /etc/nginx/nginx.conf

WORKDIR /var/www

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]