FROM bitnami/spark:3.4

USER root

RUN apt-get update && apt-get install -y curl

RUN curl -O https://repo1.maven.org/maven2/software/amazon/awssdk/s3/2.18.41/s3-2.18.41.jar \
    && curl -O https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk/1.12.367/aws-java-sdk-1.12.367.jar \
    && curl -O https://repo1.maven.org/maven2/io/delta/delta-core_2.12/2.2.0/delta-core_2.12-2.2.0.jar \
    && curl -O https://repo1.maven.org/maven2/io/delta/delta-storage/2.2.0/delta-storage-2.2.0.jar \
    && mv s3-2.18.41.jar /opt/bitnami/spark/jars \
    && mv aws-java-sdk-1.12.367.jar /opt/bitnami/spark/jars \
    && mv delta-core_2.12-2.2.0.jar /opt/bitnami/spark/jars \
    && mv delta-storage-2.2.0.jar /opt/bitnami/spark/jars

COPY spark-defaults.conf /usr/local/spark/conf/

RUN echo 'spark.jars                                          /opt/bitnami/spark/jars/delta-core_2.12-2.2.0.jar,/opt/bitnami/spark/jars/hadoop-aws-3.3.2.jar,/opt/bitnami/spark/jars/delta-storage-2.2.0.jar,/opt/bitnami/spark/jars/aws-java-sdk-1.12.367.jar,/opt/bitnami/spark/jars/s3-2.18.41.jar,/opt/bitnami/spark/jars/aws-java-sdk-bundle-1.11.1026.jar' >> /usr/local/spark/conf/spark-defaults.conf \
 && chown -Rf 1001:root /opt/bitnami/spark

WORKDIR /opt/bitnami/spark

EXPOSE 8080 7077

LABEL \
  org.opencontainers.image.vendor="Apache Spark" \
  org.opencontainers.image.description="Ambiente Apache Spark" \
  org.opencontainers.image.version="1.0.0" \
  org.opencontainers.image.licenses="MIT" \
  org.opencontainers.image.maintainer="Erivando Sena"