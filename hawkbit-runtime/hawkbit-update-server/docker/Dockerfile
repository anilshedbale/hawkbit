#Docker file
FROM alpine

MAINTAINER anil.shedbale@aeris.net

  
RUN apk update && apk add openjdk8

ENV HAWKBIT_HOME=/root/hawkbit \
	LOGROOT=/root/logs \
	MARIADB_DRIVER_VERSION=2.1.2
  
# Http port
EXPOSE 8080

RUN set -x \
    && apk add --no-cache gnupg unzip \
    && apk add --no-cache libressl wget \
	  && mkdir -p $HAWKBIT_HOME \
    && cd $HAWKBIT_HOME \
    && cp ${workspace}/hawkbit-aeris/hawkbit-runtime/hawkbit-update-server/target/hawkbit-update-server-0.2.0-SNAPSHOT.jar $HAWKBIT_HOME/hawkbit-update-server.jar
    
    
# Install mariadb driver
RUN set -x \
	&& cd $HAWKBIT_HOME \
    && wget -O $JAVA_HOME/lib/ext/mariadb-java-client.jar --no-verbose http://downloads.mariadb.com/Connectors/java/connector-java-$MARIADB_DRIVER_VERSION/mariadb-java-client-$MARIADB_DRIVER_VERSION.jar \
    && wget -O $JAVA_HOME/lib/ext/mariadb-java-client.jar.asc --no-verbose http://downloads.mariadb.com/Connectors/java/connector-java-$MARIADB_DRIVER_VERSION/mariadb-java-client-$MARIADB_DRIVER_VERSION.jar.asc
    
ENTRYPOINT ["java","-jar","$HAWKBIT_HOME/hawkbit-update-server.jar","--spring.profiles.active=amqp,mysql","-Xmx768m -Xmx768m -XX:MaxMetaspaceSize=250m -XX:MetaspaceSize=250m -Xss300K -XX:+UseG1GC -XX:+UseStringDeduplication -XX:+UseCompressedOops -XX:+HeapDumpOnOutOfMemoryError"]
