FROM amazonlinux:2
FROM amazoncorretto:25
FROM maven:3.9-amazoncorretto-25

RUN yum install -y procps-ng tar gzip

WORKDIR /tmp/
ADD pom.xml /tmp
RUN curl -o ./spark-4.3.0-bin-without-hadoop.tgz https://archive.apache.org/dist/spark/spark-4.3.0/spark-4.3.0-bin-without-hadoop.tgz
RUN tar -xzf spark-4.3.0-bin-without-hadoop.tgz && \
    mv spark-4.3.0-bin-without-hadoop /opt/spark && \
    rm spark-4.3.0-bin-without-hadoop.tgz
RUN mvn dependency:copy-dependencies -DoutputDirectory=/opt/spark/jars/
RUN rm /opt/spark/jars/jsr305-3.0.0.jar && \
    rm /opt/spark/jars/jackson-core-2.21.2.jar && \
    rm /opt/spark/jars/jackson-databind-2.21.2.jar && \
    rm /opt/spark/jars/snappy-java-1.1.10.8.jar && \
    rm /opt/spark/jars/commons-codec-1.11.jar && \
    rm /opt/spark/jars/commons-logging-1.3.0.jar

RUN echo $'\n\
spark.eventLog.enabled                      true\n\
spark.history.ui.port                       18080\n\
' > /opt/spark/conf/spark-defaults.conf

ENTRYPOINT ["/bin/bash", "-c"]:

