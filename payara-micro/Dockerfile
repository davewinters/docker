# Pull ubuntu base image.
FROM ubuntu 

# Maintainer
# ----------
MAINTAINER David Winters <dwinters@c2b2.co.uk>

ENV PAYARA_PKG https://s3-eu-west-1.amazonaws.com/payara.co/Payara+Downloads/payara-micro-4.1.152.1.jar
ENV PKG_FILE_NAME payara-micro-4.1.152.1.jar

#Install packages on ubuntu base image

RUN \
 apt-get update && \ 
 apt-get install -y wget && \ 
 apt-get install -y software-properties-common python-software-properties


# Install Java 8

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \ 
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# add payara user, download payara micro build. Download sample war app and package on image.

RUN useradd -b /opt -m -s /bin/bash payara && echo payara:payara | chpasswd
RUN cd /opt && wget $PAYARA_PKG
RUN cd /opt && wget http://repository.primefaces.org/org/primefaces/showcase/5.2/showcase-5.2.war
RUN chown -R payara:payara /opt


# Set up payara user and the home directory for the user
USER payara
WORKDIR /opt

