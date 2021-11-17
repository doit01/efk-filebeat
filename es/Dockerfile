ARG ELK_VERSION

# https://www.docker.elastic.co/
FROM docker.elastic.co/elasticsearch/elasticsearch:${ELK_VERSION}
USER root
# Add your elasticsearch plugins setup here
# Example: RUN elasticsearch-plugin install analysis-icu
# ADD elasticsearch-analysis-ik-7.11.1 /usr/share/elasticsearch/plugins/
# RUN mv /usr/share/elasticsearch/plugins/elasticsearch-analysis-ik-7.11.1 /usr/share/elasticsearch/plugins/ik
# RUN chmod 777 /usr/share/elasticsearch/plugins/ik -R


#生成证书，密码可自己配置
RUN bin/elasticsearch-certutil ca --out config/elastic-stack-ca.p12 --pass 123456

#生成证书，密码可自己配置
RUN bin/elasticsearch-certutil cert --ca config/elastic-stack-ca.p12 --ca-pass 123456 --out config/elastic-certificates.p12 --pass 123456

#创建keystore
RUN bin/elasticsearch-keystore create

#将密码添加至keystore
RUN sh -c '/bin/echo -e "123456" | sh bin/elasticsearch-keystore add xpack.security.transport.ssl.keystore.secure_password'
RUN sh -c '/bin/echo -e "123456" | sh bin/elasticsearch-keystore add xpack.security.transport.ssl.truststore.secure_password'

#文件赋权限
RUN chmod 777 /usr/share/elasticsearch/config/elastic-certificates.p12
RUN chmod 777 /usr/share/elasticsearch/config/elastic-stack-ca.p12
