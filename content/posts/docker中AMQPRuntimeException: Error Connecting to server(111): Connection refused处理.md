## docker中AMQPRuntimeException: Error Connecting to server(111): Connection refused处理

## 问题描述

在学习使用rabbitmq的过程中，调用demo一直报一下错误

**Fatal error**: Uncaught PhpAmqpLib\Exception\AMQPRuntimeException: Error Connecting to server(111): Connection refused in /basicfinder/www/material/docinner/code/php/demo/vendor/php-amqplib/php-amqplib/PhpAmqpLib/Wire/IO/StreamIO.php:27 Stack trace: #0

![img](docker中AMQPRuntimeException: Error Connecting to server(111): Connection refused处理.assets/1015716-20220228222715503-1232089061.png)

 解决方案

在docker容器内，因为我配置的host地址为127.0.0.1，肯定是无法找到的。。随后改成本机对外实际地址 172.20.*.* (这里为自己的服务的实际ip地址)就可以了！

![img](docker中AMQPRuntimeException: Error Connecting to server(111): Connection refused处理.assets/1015716-20220228223153580-1098425723.png)

 

![img](docker中AMQPRuntimeException: Error Connecting to server(111): Connection refused处理.assets/1015716-20220228223416634-1721853294.png)

 

对了在此之前，一定要先通过 telnet 来确保rabbitmq服务是可以的

```
telnet 127.0.0.1 5672
```

![img](docker中AMQPRuntimeException: Error Connecting to server(111): Connection refused处理.assets/1015716-20220228223539740-1093863632.png)

 