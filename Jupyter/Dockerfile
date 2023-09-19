FROM jupyter/all-spark-notebook:python-3.8

USER root 

RUN curl -O https://archive.apache.org/dist/spark/spark-3.4.1/spark-3.4.1-bin-hadoop3.tgz \
    && tar zxvf spark-3.4.1-bin-hadoop3.tgz \
    && rm -rf spark-3.4.1-bin-hadoop3.tgz \
    && mv spark-3.4.1-bin-hadoop3/ /usr/local/ \
    && rm -rf /usr/local/spark/* \
    && mv /usr/local/spark-3.4.1-bin-hadoop3/* /usr/local/spark/ \
    && rm -rf /usr/local/spark-3.4.1-bin-hadoop3
    
RUN curl -O https://repo1.maven.org/maven2/software/amazon/awssdk/s3/2.18.41/s3-2.18.41.jar \
    && curl -O https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk/1.12.367/aws-java-sdk-1.12.367.jar \
    && curl -O https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/1.11.1026/aws-java-sdk-bundle-1.11.1026.jar \
    && curl -O https://repo1.maven.org/maven2/io/delta/delta-core_2.12/2.2.0/delta-core_2.12-2.2.0.jar \
    && curl -O https://repo1.maven.org/maven2/io/delta/delta-storage/2.2.0/delta-storage-2.2.0.jar \
    && curl -O https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/3.3.2/hadoop-aws-3.3.2.jar \
    && mv s3-2.18.41.jar /usr/local/spark/jars \
    && mv aws-java-sdk-1.12.367.jar /usr/local/spark/jars \
    && mv aws-java-sdk-bundle-1.11.1026.jar /usr/local/spark/jars \
    && mv delta-core_2.12-2.2.0.jar /usr/local/spark/jars \
    && mv delta-storage-2.2.0.jar /usr/local/spark/jars \
    && mv hadoop-aws-3.3.2.jar /usr/local/spark/jars

COPY spark-defaults.conf /usr/local/spark/conf/

RUN echo 'spark.jars                                          /usr/local/spark/jars/delta-core_2.12-2.2.0.jar,/usr/local/spark/jars/hadoop-aws-3.3.2.jar,/usr/local/spark/jars/delta-storage-2.2.0.jar,/usr/local/spark/jars/aws-java-sdk-1.12.367.jar,/usr/local/spark/jars/s3-2.18.41.jar,/usr/local/spark/jars/aws-java-sdk-bundle-1.11.1026.jar' >> /usr/local/spark/conf/spark-defaults.conf \
 && echo 'c.NotebookApp.trust_xheaders = True' >> /etc/jupyter/jupyter_notebook_config.py \
 && chown -Rf jovyan:1000 /usr/local/spark

WORKDIR /home/jovyan/work

COPY Jupyter/notebook/ .

EXPOSE 8888 4040

LABEL \
  org.opencontainers.image.vendor="Jupyter Notebook" \
  org.opencontainers.image.description="Ambiente Apache Spark" \
  org.opencontainers.image.version="1.0.0" \
  org.opencontainers.image.licenses="MIT" \
  org.opencontainers.image.maintainer="Erivando Sena"