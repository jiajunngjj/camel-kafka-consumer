# camel-kafka-consumer
A Camel with Spring Boot Kafka consumer which consumes messages from a Kafka topic via OpenShift routes which exposes the bootstrap server.

## To run locally:
As OpenShift route is used, CA cert is required to enable TLS. Extract the cert from the kafka broker:
```
$ oc extract secret/my-cluster-cluster-ca-cert --keys=ca.crt --to=- > src/main/resources/ca.crt
```
Import the trusted cert to a keystore:
```
$ keytool -import -trustcacerts -alias root -file src/main/resources/ca.crt -keystore src/main/resources/keystore.jks -storepass password -noprompt
```
Run the application with mvn:
```
$ mvn -Drun.jvmArguments="-Dbootstrap.server=my-cluster-kafka-bootstrap-amq-streams.apps.cluster-sgjj-c2bb.sgjj-c2bb.example.opentlc.com:443" clean package spring-boot:run
```