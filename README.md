Example code for connecting to a Apache Kafka cluster and authenticate with SASL/SCRAM 

Configure:
You configure Spring boot in the application.properties file, here you set the brokers to connect to and the credentials for authentication.

Here is an example of the properties file

server.port=9000
spring.kafka.consumer.bootstrap-servers: ## a comma-separated list of all the brokers, the URL must include the port, for example:velomobile-01.srvs.cloudkafka.com:9094,velomobile-02.srvs.cloudkafka.com:9094,velomobile-03.srvs.cloudkafka.com:9094
spring.kafka.consumer.group-id: group-id
spring.kafka.consumer.auto-offset-reset: earliest
spring.kafka.consumer.key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.value-deserializer: org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.properties.spring.json.trusted.packages=*

spring.kafka.properties.security.protocol=SASL_SSL
spring.kafka.properties.sasl.mechanism=SCRAM-SHA-512
spring.kafka.properties.sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username="CLOUDKARAFKA_USERNAME" password="CLOUDKARAFKA_PASSWORD";
 (update the CLOUDKARAFKA_USERNAME/CLOUDKARAFKA_PASSWORD values with the SCRAM usr/password)
spring.kafka.consumer.ssl.truststore-location= classpath:/xxx.p12
spring.kafka.consumer.ssl.truststore-password= xxxxx

spring.kafka.template.default-topic=TEST-TOPIC

spring.kafka.producer.bootstrap-servers: 
spring.kafka.producer.key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.producer.value-deserializer: org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.producer.ssl.truststore-location= classpath:/xx.p12
spring.kafka.producer.ssl.truststore-password= xxxxx

Run:
git clone https://github.com/gudipatinrao/spring-boot-kafka-app.git

cd springboot-kafka-example

mvn clean install

mvn spring-boot:run

Test:
Use any REST API tester and post few messages to API http://localhost:9000/kafka/publish in query parameter "message".

Message post : http://localhost:9000/kafka/publish?message=IBMCloud

Observe the console logs: