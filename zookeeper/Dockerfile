FROM alpine:3.11
LABEL AUTOR="MARTIN VILCHE" PROYECTO="APACHE ZOOKEPER"
ENV ZOOKEEPER_URL=https://downloads.apache.org/zookeeper/zookeeper-3.6.0/apache-zookeeper-3.6.0-bin.tar.gz
RUN apk add --update --no-cache gawk openjdk11 bash curl && mkdir -p /opt/zookeeper /opt/zookeeper-data /opt/prometheus
RUN curl $ZOOKEEPER_URL --output /tmp/zookeeper.tgz && tar zxvf /tmp/zookeeper.tgz --strip-components 1 -C /opt/zookeeper && \
touch /opt/zookeeper/conf/zoo.cfg && rm -rf /tmp/zookeeper.tgz
COPY jmx_prometheus_javaagent-0.12.0.jar /opt/zookeeper/jmx_prometheus_javaagent-0.12.0.jar
RUN chmod +x /opt/zookeeper/bin/* && \
chown -R 1001 /opt && \
chgrp -R 0 /opt && \
chmod -R g=u /opt
USER 1001
EXPOSE 2181 2888 3888 9998
WORKDIR /opt/zookeeper