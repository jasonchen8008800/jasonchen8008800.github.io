`php8.3fpm`

``` bash
docker run --name php8.3fpm \
-v /Users/jasonchan/Workspace/www:/home/wwwroot \
-v /Users/jasonchan/Workspace/docker/php_apps/php8.3fpm/conf.d⁠:/usr/local/etc/php \
-p 9000:9000 \
-d php:8.3-fpm

```



`php7.3.33`

```bash
docker run --name php7.3fpm \
-v /Users/jasonchan/Workspace/www:/home/wwwroot \
-v /Users/jasonchan/Workspace/docker/php_apps/php7.3fpm/conf.d⁠:/usr/local/etc/php \
-p 9000:9000 \
-d php

```

