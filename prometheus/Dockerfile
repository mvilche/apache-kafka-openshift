FROM alpine:3.10

RUN apk add --no-cache --update wget bash curl && \
mkdir -p /opt/prometheus /opt/prometheus-config /opt/prometheus-data && \
wget https://github.com/prometheus/prometheus/releases/download/v2.14.0/prometheus-2.14.0.linux-amd64.tar.gz -O /tmp/prometheus.tar.gz && \
tar zxvf /tmp/prometheus.tar.gz --strip-components 1 -C /opt/prometheus && \
rm -rf /tmp/prometheus.tar.gz

RUN chown -R 1001 /opt && \
chgrp -R 0 /opt  && \
chmod -R g=u /opt

USER 1001

EXPOSE 9090

CMD /opt/prometheus/prometheus --config.file=/opt/prometheus-config/prometheus.yml --storage.tsdb.path=/opt/prometheus-data