``` bash
docker run --restart=always --privileged=true -d -p 3306:3306 \
-v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/conf.d/:/etc/mysql/conf.d/ \
-v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=my-secret-pw --name 0c27e8e5fcfab7805cfed996b55e5e98f43fd7ee76e1516f20cba139c6a299c5
```





```
docker run --restart=always -d -p 3307:3306 \
-v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/conf.d/:/etc/mysql/conf.d/ \
-v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=my-secret-pw \
--name mysql8.0.19 mysql:8.0.19
```





```
docker run --restart=always -d -p 3308:3306 \
-v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=my-secret-pw \
--name mysql8.0.191 mysql:8.0.19
```



```
docker run --restart=always -d --name mysql8.0.19 -p 3308:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d -v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/conf.d/:/etc/mysql/conf.d/ -v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/data:/var/lib/mysql mysql:8.0.19

```

```
docker run --restart=always -d --name mysql8.0.19 -p 3308:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d  -v /Users/jasonchan/Workspace/docker/mysql_app/mysql8/data:/var/lib/mysql mysql:8.0.19
```

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY  'my-secret-pw';
```

