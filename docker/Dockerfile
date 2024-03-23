# Base image
FROM openjdk:11

# Define versions
ARG SPARK_VERSION=3.2.0
ARG HADOOP_VERSION=3.3.1

# Download and install Hadoop
RUN mkdir -p /opt/hadoop && \
    curl -fSL "http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz" -o /tmp/hadoop.tar.gz && \
    tar -xzf /tmp/hadoop.tar.gz -C /opt/hadoop --strip-components=1 && \
    rm /tmp/hadoop.tar.gz && \
    ln -s /opt/hadoop /opt/hadoop-${HADOOP_VERSION} && \
    echo "Hadoop ${HADOOP_VERSION} installed in /opt/hadoop"

# Download and install Spark
RUN mkdir -p /opt/spark && \
    curl -fSL "http://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz" -o /tmp/spark.tgz && \
    tar -xzf /tmp/spark.tgz -C /opt/spark --strip-components=1 && \
    rm /tmp/spark.tgz && \
    ln -s /opt/spark /opt/spark-${SPARK_VERSION} && \
    echo "Spark ${SPARK_VERSION} installed in /opt/spark"

# Add scripts and update Spark default config
ADD common.sh spark-master spark-worker /
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf

# Add Spark and Hadoop binaries to the PATH
ENV PATH $PATH:/opt/spark/bin:/opt/hadoop/bin
