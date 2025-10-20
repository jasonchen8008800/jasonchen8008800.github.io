`curl -L -O https://raw.githubusercontent.com/elastic/beats/9.1/deploy/docker/filebeat.docker.yml`

```
docker run -d \
--name=elk_filebeat \
--user=root \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/config/filebeat.docker.yml:/usr/share/filebeat/filebeat.yml:ro" \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/containers:/var/lib/docker/containers:ro" \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/run/docker.sock:/var/run/docker.sock:ro" \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/registry:/usr/share/filebeat/data:rw" \
-e --strict.perms=false \
-E output.elasticsearch.hosts=["elasticsearch:9200"] \
--link elk_elasticsearch:elasticsearch \
elastic/filebeat:9.1.4 filebeat 

```



```docker run -d \
docker run -d \
--name=elk_filebeat \
--user=root \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/config/filebeat.docker.yml:/usr/share/filebeat/filebeat.yml:ro" \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/containers:/var/lib/docker/containers:ro" \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/run/docker.sock:/var/run/docker.sock:ro" \
-v="/Users/jasonchan/Workspace/docker/elasticsearch/elk/filebeat/registry:/usr/share/filebeat/data:rw" \
elastic/filebeat:9.1.4 filebeat -e --strict.perms=false \
-E output.elasticsearch.hosts=["elasticsearch:9200"]
