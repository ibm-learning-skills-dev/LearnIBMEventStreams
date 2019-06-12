# Cut and Paste commands and code for WD107

Be sure to substitute the appropriate value for any variable within <> (angle brackets). Note that this is not an exhaustive list of all commands that are used in the course.


## Lab 1

`sudo cloudctl login -a https://10.0.0.1:8443 --skip-ssl-validation`

`sudo docker login mycluster.icp:8500`

`sudo cloudctl catalog load-archive --archive eventstreams.2018.3.1.z_x86.pak.tar.gz`

`sudo kubectl create secret docker-registry regcred --docker-server=mycluster.icp:8500 --docker-username=admin --docker-password=admin --docker-email=<your_email>@ibm.com -n es`

`sudo kubectl apply -f imgpol.yaml`


## Lab 2

`export _JAVA_OPTIONS=-Djdk.net.URLClassPath.disableClassPathURLCheck=true`

`mvn install liberty:run-server`


## Lab 3

`java -jar es-producer.jar -g`

`java -jar es-producer.jar -t eslab -s small`

`java -jar es-producer.jar -t eslab -s large`


## Lab 4

`bin/zookeeper-server-start.sh config/zookeeper.properties`

`bin/kafka-server-start.sh config/server.properties`

`bin/kafka-topics.sh --zookeeper localhost:2181 --create --topic eslab --partitions 1 --replication-factor 1`

`bin/kafka-topics.sh --zookeeper localhost:2181 --describe`

`CLASSPATH=/home/student/kafka-connect-mq-source-1.0.1-jar-with-dependencies.jar bin/connect-standalone.sh config/connect-standalone.properties ~/mq-source.properties`

`bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic eslab`

`bin/kafka-server-stop.sh`

`bin/zookeeper-server-stop.sh`

```
security.protocol=SASL_SSL
ssl.protocol=TLSv1.2
ssl.endpoint.identification.algorithm=
ssl.truststore.location=
ssl.truststore.password=password
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="token" password="";
```
```
producer.security.protocol=SASL_SSL
producer.ssl.protocol=TLSv1.2
producer.ssl.endpoint.identification.algorithm=
producer.ssl.truststore.location=
producer.ssl.truststore.password=password
producer.sasl.mechanism=PLAIN
producer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="token" password="";
```

`bin/kafka-console-consumer.sh --bootstrap-server <address:port> --consumer.config config/mqlab.properties --topic eslab --group eslabtester`


## Lab 5

`consumer.group.id=eslabsink`

`CLASSPATH=/home/student/kafka-connect-mq-sink-1.0.1-jar-with-dependencies.jar bin/connect-standalone.sh config/connect-standalone-sink.properties /home/student/mq-sink.properties`



Lab 6

`https://github.com/IBM/charts/blob/master/stable/ibm-eventstreams-dev/ibm_cloud_pak/pak_extensions/dashboards/ibm-eventstreams-grafanadashboard.json`

