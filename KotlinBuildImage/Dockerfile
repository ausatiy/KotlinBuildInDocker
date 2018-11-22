FROM ubuntu:18.04

## Install additional software
RUN apt-get update
RUN apt-get install -y mc unzip git openssh-server
RUN service ssh start
RUN echo "root:Docker!" | chpasswd

## Create directory with JDK
RUN mkdir /jdk
WORKDIR /jdk
RUN wget https://cdn.azul.com/zulu/bin/zulu6.22.0.3-jdk6.0.119-linux_x64.tar.gz
RUN wget https://cdn.azul.com/zulu/bin/zulu7.25.0.5-jdk7.0.201-linux_x64.tar.gz
RUN wget https://cdn.azul.com/zulu/bin/zulu8.33.0.1-jdk8.0.192-linux_x64.tar.gz
RUN wget https://cdn.azul.com/zulu/bin/zulu9.0.7.1-jdk9.0.7-linux_x64.tar.gz

## Untar files
RUN for a in `ls -1 *.tar.gz`; do gzip -dc $a | tar xf -; done
RUN rm -f /jdk/*.gz
RUN ln -s `cd /jdk/zulu6*&&pwd` jdk_6
RUN ln -s `cd /jdk/zulu7*&&pwd` jdk_7
RUN ln -s `cd /jdk/zulu8*&&pwd` jdk_8
RUN ln -s `cd /jdk/zulu9*&&pwd` jdk_9

## Set environment variables
ENV JDK_16=/jdk/jdk_6
ENV JDK_17=/jdk/jdk_7
ENV JDK_18=/jdk/jdk_8
ENV JDK_9=/jdk/jdk_9

ENV JAVA_HOME=/jdk/jdk_8

#WORKDIR /
#RUN git clone https://github.com/JetBrains/kotlin.git
#WORKDIR /kotlin
#RUN ./gradlew clean dist

