# Docker images

To build an image run ```docker-compose build``` in image directory. 
	 
- **cassandra-waitable**  - image for a cassandra node which supports waiting for completing bootstrap of an other node. See cassandra-waitable readme with example of usage.

- **rabbitmq-web-stomp** - image for RabbitMq with Web STOMP plugin enabled.

- **spring-boot-service** - basic image for spring boot application. To build an image of concrete application create image based on this one and copy application jar file as application.jar.
	```
	FROM spring-boot-service
	ADD ./target/concrete-application.jar application.jar
	```
