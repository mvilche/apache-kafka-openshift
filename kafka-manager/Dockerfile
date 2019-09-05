FROM alpine:3.10
LABEL AUTOR="MARTIN VILCHE" PROYECTO="APACHE KAFKA"
ENV MANAGER_REPO=https://github.com/mvilche/kafka-manager.git
RUN apk add --update --no-cache gawk openjdk8 bash curl unzip && mkdir  -p /opt && \
git clone $MANAGER_REPO /opt/kafka-manager
WORKDIR /opt/kafka-manager
RUN ./sbt clean dist && cd /opt/kafka-manager/target/universal && unzip kafka-manager-2.0.0.2.zip && rm -rf kafka-manager-2.0.0.2.zip
RUN chown 1001 -R /opt && \
chgrp -R 0 /opt && \
chmod -R g=u /opt 
USER 1001
EXPOSE 8080
