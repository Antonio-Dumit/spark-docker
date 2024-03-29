FROM ubuntu:18.04
COPY sbt-0.13.16.tgz /

ENV DAEMON_RUN=true
ENV SPARK_VERSION=2.4.2
ENV HADOOP_VERSION=2.7
ENV SCALA_VERSION=2.12.8
ENV SCALA_HOME=/usr/share/scala
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV LANG=en_US.UTF-8    
ENV LC_ALL=en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive

COPY spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz /

RUN apt-get update \
    && apt-get -y install openjdk-8-jdk \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update

RUN apt-get -y install wget ca-certificates && \
    apt-get -y install bash curl && \
    cd "/tmp" && \
    wget --no-check-certificate --no-verbose "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
    tar xzf "scala-${SCALA_VERSION}.tgz" && \
    mkdir "${SCALA_HOME}" && \
    rm "/tmp/scala-${SCALA_VERSION}/bin/"*.bat && \
    mv "/tmp/scala-${SCALA_VERSION}/bin" "/tmp/scala-${SCALA_VERSION}/lib" "${SCALA_HOME}" && \
    ln -s "${SCALA_HOME}/bin/"* "/usr/bin/" && \
    rm -rf "/tmp/"*

RUN apt-get -y install python3

#Scala instalation
RUN export PATH="/usr/local/sbt/bin:$PATH" && \
    apt install ca-certificates wget tar && \
    mkdir -p "/usr/local/sbt" && \
    tar -xzf "/sbt-0.13.16.tgz" -C "/usr/local/sbt" --strip-components=1 && \
    sbt sbtVersion


# RUN wget --no-verbose http://apache.mirror.iphh.net/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
RUN tar -xvzf /spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark && \
    rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
