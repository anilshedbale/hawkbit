#Docker file
FROM openjdk:8u121-jre-alpine

MAINTAINER anil.shedbale@aeris.net

ENV MARIADB_DRIVER_VERSION=2.1.2 
  
# Http port
EXPOSE 8080

# Install mariadb driver
RUN set -x \
    && apk add --no-cache libressl wget \
    && wget -O $JAVA_HOME/lib/ext/mariadb-java-client.jar --no-verbose http://downloads.mariadb.com/Connectors/java/connector-java-$MARIADB_DRIVER_VERSION/mariadb-java-client-$MARIADB_DRIVER_VERSION.jar \
    && wget -O $JAVA_HOME/lib/ext/mariadb-java-client.jar.asc --no-verbose http://downloads.mariadb.com/Connectors/java/connector-java-$MARIADB_DRIVER_VERSION/mariadb-java-client-$MARIADB_DRIVER_VERSION.jar.asc

COPY hawkbit-runtime/hawkbit-update-server/target/hawkbit-update-server-0.2.0-SNAPSHOT.jar /root/hawkbit-update-server-0.2.0-SNAPSHOT.jar

WORKDIR /root
#WORKDIR $HAWKBIT_HOME

ENTRYPOINT ["java","-jar","/root/hawkbit-update-server-0.2.0-SNAPSHOT.jar","--spring.profiles.active=amqp,mysql","-Xmx768m -Xmx768m -XX:MaxMetaspaceSize=250m -XX:MetaspaceSize=250m -Xss300K -XX:+UseG1GC -XX:+UseStringDeduplication -XX:+UseCompressedOops -XX:+HeapDumpOnOutOfMemoryError"]
