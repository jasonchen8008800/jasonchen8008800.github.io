##### 启动容器，创建挂载目录

```bash
# 启动容器
docker run -d --name=logstash logstash:9.1.4

# 主机创建文件夹，用于挂载logstash容器的文件
mkdir /soft/logstash/logstash/config

# 复制容器logstash的配置文件出来
docker cp logstash:/usr/share/logstash/config/logstash.yml /soft/logstash/logstash/config/logstash.yml
```

##### 编辑logstash.yml

```yaml
http.host: "0.0.0.0"
#根据实际修改es的ip：port
xpack.monitoring.elasticsearch.hosts: [ "http://elasticsearch:9200" ]
# 主管道的Logstash配置路径，如果指定目录或通配符，配置文件将按字母顺序从目录中读取
# path.config: /usr/share/logstash/config/*.conf
path.config: /usr/share/logstash/config/logstash.conf
#Logstash将其日志写到的目录
path.logs: /usr/share/logstash/logs
```

##### 创建配置文件 logstash.conf

在刚才的config目录下建一个conf文件

`vim /soft/logstash/logstash/config/logstash.conf`

```verilog

# Logstash.conf 配置文件示例  
input {
# 读取文件数据
  file {
    #采集点(注意，由于是docker启动的logstash,这里是容器内的文件，如果要采集外面主机的日志，那么文件的路径一定要挂载正确，docker启动的时候挂载下路径就好)
    path => ["/usr/share/logstash/logFile/*.log"]
    #从文件的开头开始读取，也可以选择'end'从文件末尾开始读取
    start_position => "beginning"
    #扫描间隔时间，默认是1s，建议5s
    stat_interval => "5"
    
    # sincedb文件路径，用于记录读取位置，确保在Logstash重启后不会重复读取数据，
    # 该路径必须指定到文件不能指定到文件的目录 ，不指定会默认创建
    # sincedb_path => "/usr/share/logstash/file/sincedb.txt" 
    
    # 利用linux黑洞可以达到每次重头读取日志文件
    sincedb_path => "/dev/null"
  }
}

output {
  elasticsearch {
  #集群的话，直接添加多个url
    hosts => ["elasticsearch:9200"]
    #es的用户名和密码(无密码则不需要)
    #user =>"logstash_system"
    #password =>"B9u5yJszs6FrKKliQ4AN"
    #建立的索引以日期区分
    index => "logstash-log-%{+YYYY.MM.dd}"
 }
 #在控制台输出logstash的日志
 stdout { codec=> rubydebug }
}
```

```shell
docker run -d \
--name elk_logstash \
-p 9600:9600 \
-p 5044:5044 \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/logstash/config/logstash.conf:/usr/share/logstash/config/logstash.conf \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/logstash/pipeline/logstash.conf:/usr/share/logstash/pipeline/logstash.conf \
-v /Users/jasonchan/Workspace/docker/elasticsearch/elk/logstash/logs:/usr/share/logstash/logFile \
--link elk_elasticsearch:elasticsearch \
logstash:9.1.4


```

- `-d`：以后台模式运行容器。
- `--name logstash`：为容器指定名称为 `logstash`。
- `-p 9600:9600`：将主机的 9600 端口映射到容器的 9600 端口，用于访问 Logstash 的监控接口。
- `-p 5044:5044`：将主机的 5044 端口映射到容器的 5044 端口，用于接收 Filebeat 或其他 Beats 工具发送的数据。
- `--network elk-net`：将容器连接到名为 `elk-net` 的 Docker 网络，确保 Logstash 和 Elasticsearch 可以通过网络通信。
- `-v /soft/logstash/logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml`：将主机路径 `/soft/logstash/logstash/config/logstash.yml` 挂载到容器内的 `/usr/share/logstash/config/logstash.yml`，用于加载 Logstash 的全局配置文件。
- `-v /soft/logstash/logstash/config/logstash.conf:/usr/share/logstash/config/logstash.conf`：将主机路径 `/soft/logstash/logstash/config/logstash.conf` 挂载到容器内的 `/usr/share/logstash/config/logstash.conf`，用于定义 Logstash 的数据处理管道配置。
- `-v /soft/logstash/logstash/config/logFile:/usr/share/logstash/logFile`：将主机路径 `/soft/logstash/logstash/config/logFile` 挂载到容器内的 `/usr/share/logstash/logFile`，用于存储日志文件或其他需要持久化的数据。
- `--link elk_elasticsearch:elasticsearch` 映射host
- `logstash:9.1.4`：使用的 Logstash 镜像版本为 `9.1.4`，需确保与 Elasticsearch 和 Kibana 的版本匹配。