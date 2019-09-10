FROM alpine:3.9
LABEL AUTOR="MARTIN VILCHE" PROYECTO="APACHE KAFKA"
ENV KAFKA_URL=http://espejito.fder.edu.uy/apache/kafka/2.3.0/kafka_2.12-2.3.0.tgz
RUN apk add --update --no-cache gawk openjdk8 bash curl && mkdir -p /opt/kafka /opt/kafka-storage
RUN curl $KAFKA_URL --output /tmp/kafka.tgz && tar zxvf /tmp/kafka.tgz --strip-components 1 -C /opt/kafka && rm -rf /tmp/*.tgz
COPY log4j.properties /opt/kafka/config
COPY checkZoo /opt/checkZoo
RUN chmod +x /opt/checkZoo && chown 1001 -R /opt && \
chgrp -R 0 /opt && \
chmod -R g=u /opt
USER 1001
EXPOSE 9092 9093
WORKDIR /opt/kafka/bin