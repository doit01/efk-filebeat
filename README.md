output.elasticsearch:
  hosts: ["http://localhost:9200"]
  indices:
    - index: "warning-%{[agent.version]}-%{+yyyy.MM.dd}"
      when.contains:
        message: "WARN"
    - index: "error-%{[agent.version]}-%{+yyyy.MM.dd}"
      when.contains:
        message: "ERR"
        
        
        

/var/lib/docker/volumes
docker-compose up --build --force-recreate
查看docker container 的挂载
docker inspect -f "{{.Mounts}}" d00272a0525b


docker inspect d00272a0525b   | grep Mounts -A 10
"Mounts": [
{
"Type": "volume",
"Name": "efk-filebeat-195_data01",
"Source": "/var/lib/docker/volumes/efk-filebeat-195_data01/_data",
"Destination": "/usr/share/elasticsearch/data",
"Driver": "local",
"Mode": "rw",
"RW": true,
"Propagation": ""
}




http://10.128.29.195:9200/

// install ik https://www.jianshu.com/p/d8b0c736070f


localhost:9200
localhost:5601
curl -I -X DELETE http://10.128.29.160:5000/v2/_catalog/sha256:4228b7a8ef40b7593b1a7493bebf68022f0562446cef75dbff49f3af3c1d044d
http://10.128.29.161:5601/app/home#/
find all indexes
http://10.128.29.161:9200/_cat/indices?v
http://10.128.29.160:9200/_cat/indices?v

http://localhost:9200/_cat/indices?v


localhost:9200/accounts/person/_search
http://10.128.29.161:5601/app/discover#/?_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-15m,to:now))&_a=(columns:!(_id,_index,'@timestamp',agent.hostname,message),filters:!(),index:'0d3cada0-91e9-11eb-b979-7dfc591efe21',interval:auto,query:(language:kuery,query:username),sort:!(!('@timestamp',asc)))



Elastic 的查询非常特别，使用自己的查询语法，要求 GET 请求带有数据体。
 $ curl 'localhost:9200/accounts/person/_search'  -d '
    {
      "query" : { "match" : { "desc" : "软件" }}
    }'


列出每个 Index 所包含的 Type。$ curl 'localhost:9200/_mapping?pretty=true

docker-compose 一键部署elasticsearch、kibana、filebeat
            
启动步骤：
chmod 755 filebeat/config/filebeat.yml
1、将.env.example文件改名为.env文件

2、将GLOBAL_APP_PATH的路径修改为本项目路径

3、docker-compose build    #构建容器

4、docker-compose start    #一键启动elasticsearch、filebeat、kibana容器


docker run -p 9201:9100 mobz/elasticsearch-head:5

docker-compose up --force-recreate --build -d


    方案二：开启9200端口

# 查询9200端口是否开放
firewall-cmd --query-port=9200/tcp
# 开放9200端口
firewall-cmd --permanent --add-port=9200/tcp
# 移除9200端口
firewall-cmd --permanent --remove-port=9200/tcp
# 重启防火墙(修改配置后要重启防火墙)
firewall-cmd --reload
