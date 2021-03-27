localhost:9200
localhost:5601

find all indexes
http://localhost:9200/_cat/indices?v

localhost:9200/accounts/person/_search

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
