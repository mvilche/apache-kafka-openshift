FROM centos:7

RUN yum install wget nc -y && \
wget https://dl.grafana.com/oss/release/grafana-6.5.1.linux-amd64.tar.gz  -O /tmp/grafana.tar.gz && \
mkdir -p /opt/grafana /opt/grafana-config /opt/grafana-data /opt/grafana-data/data /opt/grafana-data/plugins /opt/grafana-dashboard  && \
tar zxvf /tmp/grafana.tar.gz --strip-components 1 -C /opt/grafana && \
rm -rf /tmp/grafana.tar.gz

COPY jvm-dashboard_rev17.json /opt/grafana-dashboard/jvm-dashboard_rev17.json
COPY kafka-overview_rev1.json /opt/grafana-dashboard/kafka-overview_rev1.json

RUN adduser -u 1001 grafana && usermod -aG 0 grafana && \
chown -R 1001 /opt && \
chgrp -R 0 /opt  && \
chmod -R g=u /opt

USER 1001

EXPOSE 3000

CMD /opt/grafana/bin/grafana-server -config /opt/grafana-config/grafana.ini -homepath /opt/grafana