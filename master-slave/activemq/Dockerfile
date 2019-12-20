#FROM openjdk:8-jre
FROM openjdk:8u212-jre-alpine3.9 
ENV ACTIVEMQ_HOME /opt/activemq
RUN set -x && \
    mkdir -p /opt && \
    apk --update add --virtual build-dependencies curl && \
    curl -O https://dist.apache.org/repos/dist/release/activemq/5.15.11/apache-activemq-5.15.11-bin.tar.gz 
RUN tar zxvf apache-activemq-5.15.11-bin.tar.gz -C /opt && \
    ln -s /opt/apache-activemq-5.15.11 $ACTIVEMQ_HOME
	COPY activemq.xml /opt/apache-activemq-5.15.11/conf/activemq.xml
RUN addgroup -S activemq && adduser -S -H -G activemq -h $ACTIVEMQ_HOME activemq && \
    chown -R activemq:activemq /opt/apache-activemq-5.15.11 && \
    chown -h activemq:activemq $ACTIVEMQ_HOME && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/*
USER activemq
WORKDIR $ACTIVEMQ_HOME
EXPOSE $ACTIVEMQ_TCP $ACTIVEMQ_AMQP $ACTIVEMQ_STOMP $ACTIVEMQ_MQTT $ACTIVEMQ_WS $ACTIVEMQ_UI
CMD ["/bin/sh", "-c", "bin/activemq console"]
