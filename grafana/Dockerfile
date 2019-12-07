FROM alpine:3.10

RUN apk add --update --no-cache bashwget nc && \
wget https://dl.grafana.com/oss/release/grafana-6.4.4.linux-amd64.tar.gz  -O /tmp/grafana.tar.gz && \
 mkdir -p /opt/grafana /opt/grafana-config /opt/grafana-data /opt/grafana-data/data /opt/grafana-data/plugins /opt/grafana-dashboard  && \
tar zxvf /tmp/grafana.tar.gz --strip-components 1 -C /opt/grafana && \
rm -rf /tmp/grafana.tar.gz

COPY kafka-exporter-overview_rev5.json /opt/grafana-dashboard/kafka-exporter-overview_rev5.json

RUN chown -R 1001 /opt && \
chgrp -R 0 /opt  && \
chmod -R g=u /opt

USER 1001

EXPOSE 3000

CMD /opt/grafana/bin/grafana-server -config /opt/grafana-config/grafana.ini -homepath /opt/grafana