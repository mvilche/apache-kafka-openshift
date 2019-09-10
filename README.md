# Openshift Apache Kafka 2.3.0 + Zookeeper Cluster 3.5.5 + Apache Kafka Manager Dashboard 2.0.0.2

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


# Detalles:

- 3 Zookeeper Cluster 3
- 3 Apache Kafka broker
- 1 Apache Kafka Manager Dashboard

### Openshift Install

```console

oc create -f apache-kafka-openshift-template.yaml \
-p NAMESPACE=${PROJECT_NAME} \
 -n ${PROJECT_NAME} 

```



License
----

Martin vilche
