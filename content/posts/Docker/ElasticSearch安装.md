```sh
docker run -d \
--name elk_elasticsearch \
-p 9200:9200 \
-p 9300:9300 \
-e "ES_JAVA_OPTS=-Xms512m -Xmx512m" \
-e "discovery.type=single-node" \
-e "http.host=0.0.0.0" \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/data:/usr/share/elasticsearch/data \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/plugins:/usr/share/elasticsearch/plugins \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/logs:/usr/share/elasticsearch/logs \
--privileged \
elasticsearch:8.19.4
```

参数说明

- `-d`：以后台模式运行容器。
- `--name elasticsearch`：为容器指定名称。
- `-p 9200:9200`：将主机的 9200 端口映射到容器的 9200 端口（HTTP API 接口）。
- `-p 9300:9300`：将主机的 9300 端口映射到容器的 9300 端口（节点间通信端口，适用于集群模式）。
- `-e "ES_JAVA_OPTS=-Xms512m -Xmx512m"`：设置 Elasticsearch 的 JVM 堆内存大小为 512MB（可根据需求调整）。
- `-e "discovery.type=single-node"`：配置为单节点模式，适用于开发或测试环境。
- `-e "http.host=0.0.0.0"`：允许 Elasticsearch 监听所有网络接口上的请求。
- `-v /soft/es/data:/usr/share/elasticsearch/data`：将主机的 `./es-data` 目录挂载到容器的数据目录，用于持久化存储数据。
- `-v /soft/es/plugins:/usr/share/elasticsearch/plugins`：将主机的 `./es-plugins` 目录挂载到容器的插件目录，用于存放自定义插件。
- `-v /soft/es/logs:/usr/share/elasticsearch/logs`：将主机的 `./es-logs` 目录挂载到容器的日志目录，用于持久化存储日志文件。
- `--privileged`：赋予容器更高的权限，避免因权限不足导致的问题。
- `--network elk-net`：将容器连接到名为 `elk-net` 的 Docker 网络，便于与其他容器通信。
- `elasticsearch:7.13.4`：使用的 Elasticsearch 镜像版本
- 

> [!IMPORTANT]
>
> - **初始化密码**
>     启用后运行设置密码命令（bash）：
>
> bin/elasticsearch-setup-passwords auto # 自动生成随机密码
>
> bin/elasticsearch-reset-password -u elastic # 重置 elastic 用户密码（bash）
>
> 
>
> Changed password for user apm_system
> PASSWORD apm_system = UJBObDhJd6klAB6Rbve9
>
> Changed password for user kibana_system
> PASSWORD kibana_system = ENYflXvFjIFk8k1mkrRK
>
> Changed password for user kibana
> PASSWORD kibana = ENYflXvFjIFk8k1mkrRK
>
> Changed password for user logstash_system
> PASSWORD logstash_system = B9u5yJszs6FrKKliQ4AN
>
> Changed password for user beats_system
> PASSWORD beats_system = ugDs7XEJWAeivlD3ItFO
>
> Changed password for user remote_monitoring_user
> PASSWORD remote_monitoring_user = Hn2l7jHNDPx3j7pltx69
>
> Changed password for user elastic
> PASSWORD elastic = ay2baECXwicvLP7Dxk7T



