## Openshift Apache Kafka 2.3.0 + Zookeeper Cluster 3.5.5 + Apache Kafka Manager Dashboard 2.0.0.2

  
------------------------------------------------  

### Detalles:

- 3 Zookeeper Cluster

- 3 Apache Kafka broker

- 1 Apache Kafka Manager Dashboard
  
------------------------------------------------
### Openshift Install

```console
oc create -f apache-kafka-openshift-template.yaml \
-p NAMESPACE=${PROJECT_NAME} \
-n ${PROJECT_NAME}
```
  
------------------------------------------------
### Adminsitración Apache Kafka

##### La administración es realizada desde Kafka Manager o por terminal en una de las replicas de Kafka
 ------------------------------------------------
### Escalar cantidad de replicas Apache kafka

 
```console
oc scale statefulset kafka --replicas=${NUMBER_REPLICAS}
```
------------------------------------------------
  
### Escalar cantidad de replicas Zookeeper

  

##### Importante:
----------------------------------------------------------

*  Escalar las instancias de Zookeeper requiere de varios pasos adicionales.
* Zookeeper utiliza el algoritmo Raft (N/2)+1) por lo que es necesaria como minimo 3 instancias de Zookeper para mantener el Cluster operativo.
* Para escalar a más instancias es necesario reiniciar el cluster de Kafka y Zookeeper de forma completa.
----------------------------------------------------------

1  Editar configmap
```console
oc edit configmap zookeeper
```
2  Agregar nueva linea indicando el o los servidor en el archivo "zoo.cfg"

  
```console
zoo.cfg: |-

tickTime=2000

dataDir=/opt/zookeeper-data

clientPort=2181

initLimit=5

syncLimit=2

server.1=zookeeper-0.zookeeper.${NAMESPACE}.svc.cluster.local:2888:3888

server.2=zookeeper-1.zookeeper.${NAMESPACE}.svc.cluster.local:2888:3888

server.3=zookeeper-2.zookeeper.${NAMESPACE}.svc.cluster.local:2888:3888

server.4=zookeeper-3.zookeeper.${NAMESPACE}.svc.cluster.local:2888:3888 # NUEVA LINEA

server.5=zookeeper-4.zookeeper.${NAMESPACE}.svc.cluster.local:2888:3888 # NUEVA LINEA

autopurge.snapRetainCount=3

autopurge.purgeInterval=24
```
  

3 Editar Kafka Statefulset
```console
oc edit statefulset kafka
```  

- Edite la linea zookeeper.connect y agregue las nuevas instancias:

```console
--override zookeeper.connect=zookeeper-0.zookeeper.$NAMESPACE.svc.cluster.local:2181,zookeeper-1.zookeeper.$NAMESPACE.svc.cluster.local:2181,zookeeper-2.zookeeper.$NAMESPACE.svc.cluster.local:2181,zookeeper-3.zookeeper.$NAMESPACE.svc.cluster.local:2181,zookeeper-4.zookeeper.$NAMESPACE.svc.cluster.local:2181
```
4 Ejecutar
```console
oc scale statefulset kafka --replicas=0
```
  ```console
oc scale statefulset zookeeper --replicas=0
```

##### Verifique que ambos servicios estén en 0

  
5 Ejecutar
```console
oc scale statefulset kafka --replicas=${NUMBER_REPLICAS}
```
```console
oc scale statefulset zookeeper --replicas=5
```
#### License
##### Martin Fabrizzio Vilche
