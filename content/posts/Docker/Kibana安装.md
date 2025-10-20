```
docker run -d \
--name elk_kibana \
-e ELASTICSEARCH_HOSTS=http://elasticsearch:9200 \
-e ELASTICSEARCH_USERNAME=kibana \
-e ELASTICSEARCH_PASSWORD=ENYflXvFjIFk8k1mkrRK \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/kibana/config:/usr/share/kibana/config \
-p 5601:5601 \
--link elk_elasticsearch:elasticsearch \
kibana:8.19.4

```

参数说明：

- `-d`：以后台模式运行容器。
- `--name kibana`：为容器指定名称为 `kibana`。
- `-e ELASTICSEARCH_HOSTS=http://elasticsearch:9200`：设置环境变量，指定 Kibana 连接的 Elasticsearch 地址为 `http://elasticsearch:9200`。
- `--network=elk-net`：将容器连接到名为 elk-net 的 Docker 网络，确保 Kibana 和 Elasticsearch 可以通过网络通信。
- `-p 5601:5601`：将主机的 5601 端口映射到容器的 5601 端口，用于访问 Kibana 的 Web 界面。
- `kibana:9.1.4`：使用的 Kibana 镜像版本为 9.1.4，需确保与 Elasticsearch 版本匹配。

```
#
# ** THIS IS AN AUTO-GENERATED FILE **
#

# Default Kibana configuration for docker target
server.host: "0.0.0.0"
server.shutdownTimeout: "5s"
elasticsearch.hosts: [ "http://172.17.0.5:9200" ]
monitoring.ui.container.elasticsearch.enabled: true
elasticsearch.username: "kibana"
elasticsearch.password: "ENYflXvFjIFk8k1mkrRK"
i18n.locale: "zh-CN"  # 设置中文
```

