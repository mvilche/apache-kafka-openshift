FROM alpine:3.10
LABEL AUTOR="MARTIN VILCHE" PROYECTO="APACHE ZOOKEPER"
ENV ZOOKEEPER_URL=http://espejito.fder.edu.uy/apache/zookeeper/zookeeper-3.5.5/apache-zookeeper-3.5.5-bin.tar.gz
RUN apk add --update --no-cache gawk openjdk8 bash curl && mkdir -p /opt/zookeeper /opt/zookeeper-data
RUN curl $ZOOKEEPER_URL --output /tmp/zookeeper.tgz && tar zxvf /tmp/zookeeper.tgz --strip-components 1 -C /opt/zookeeper && \
touch /opt/zookeeper/conf/zoo.cfg && rm -rf /tmp/zookeeper.tgz
COPY run.sh /usr/bin/run.sh
RUN chown -R 1001 /opt /usr/bin/run.sh && \
chgrp -R 0 /opt /usr/bin/run.sh && \
chmod -R g=u /opt /usr/bin/run.sh 
USER 1001
EXPOSE 2181
ENTRYPOINT ["/usr/bin/run.sh"]
CMD ["/opt/zookeeper/conf/zoo.cfg"]
