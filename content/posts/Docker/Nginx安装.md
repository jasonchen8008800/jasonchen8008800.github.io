

# Docker 安装 Nginx



`php8.3fpm`

```bash
docker run --name nginx \
-v /Users/jasonchan/Workspace/www:/home/wwwroot  \
-v /Users/jasonchan/Workspace/docker/nginx/conf.d:/etc/nginx/conf.d  \
-v /Users/jasonchan/Workspace/docker/nginx/nginx.conf:/etc/nginx/nginx.conf \
-v /usr/local/docker/nginx/logs:/var/nginx/logs \
-v /Users/jasonchan/Workspace/html:/usr/share/nginx/html \
 -p 80:80   -d nginx

--link php8.3fpm:php
```



Php7.3

```bash
docker run --name nginx \
-v /Users/jasonchan/Workspace/www:/home/wwwroot  \
-v /Users/jasonchan/Workspace/docker/nginx/conf.d:/etc/nginx/conf.d  \
-v /Users/jasonchan/Workspace/docker/nginx/nginx.conf:/etc/nginx/nginx.conf \
-v /usr/local/docker/nginx/logs:/var/nginx/logs \
-v /Users/jasonchan/Workspace/html:/usr/share/nginx/html \
-v /Users/jasonchan/Workspace/docker/nginx/etc:/etc/
--link php7.3fpm:php -p 80:80   -d nginx


```



