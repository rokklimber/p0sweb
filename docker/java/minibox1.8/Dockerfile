FROM progrium/busybox
MAINTAINER Ilkka Anttonen version: 0.2

# set jdk name
ARG JAVA_TOKEN=8u121
ARG JAVA_VERSION=1.8.0_121
ARG JDK_VERSION=jdk${JAVA_VERSION}

# Udate wget to support SSL
ADD server-jre-${JAVA_TOKEN}-linux-x64.tar.bz2 /opt
#ADD jre.tar.gz /opt

# Get and install Java
RUN ln -s /opt/${JDK_VERSION}/bin/java /usr/bin/java

# Link Java into use, wget-ssl updates libpthread which causes Java to break
#RUN ln -sf /lib/libpthread-2.18.so /lib/libpthread.so.0 && ln -s /opt/jre1.8.0_40/bin/java /usr/bin/java
 
