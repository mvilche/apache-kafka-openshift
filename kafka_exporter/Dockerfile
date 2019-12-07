FROM alpine:3.10
LABEL AUTOR="MARTIN VILCHE" PROYECTO="APACHE KAFKA"
COPY kafka_exporter /opt/kafka_exporter
RUN chmod +x /opt/kafka_exporter && chown 1001 -R /opt && \
chgrp -R 0 /opt && \
chmod -R g=u /opt
USER 1001
EXPOSE 9308
WORKDIR /opt