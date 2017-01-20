FROM gliderlabs/alpine
MAINTAINER Michael Foy version: 0.1

# set jdk name
ARG JAVA_TOKEN=8u121
ARG JAVA_VERSION=1.8.0_121
ARG JDK_VERSION=jdk${JAVA_VERSION}

# add bzip2 pkg
#RUN opkg-install bzip2
RUN apk add --no-cache bzip2

# Udate wget to support SSL
ADD server-jre-${JAVA_TOKEN}-linux-x64.tar.bz2 /opt
RUN chown -R root:root /opt
#ADD jre.tar.gz /opt

# That's an 1.8.0_60 JRE from OpenJDK.net
# Courtesy to https://github.com/frol/docker-alpine-oraclejdk8 from where the setup of glibc is borrowed
RUN apk add --update wget ca-certificates && \
    cd /tmp && \
    wget "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.21-r2/glibc-2.21-r2.apk" \
         "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.21-r2/glibc-bin-2.21-r2.apk" && \
    apk add --allow-untrusted glibc-2.21-r2.apk glibc-bin-2.21-r2.apk && \
    /usr/glibc/usr/bin/ldconfig /lib /usr/glibc/usr/lib && \
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf && \
    ln -s /opt/${JDK_VERSION} /opt/jre && \
    ln -s /opt/jre/bin/java /usr/bin/java && \
    apk del wget ca-certificates && \
    cd /opt/jre/lib/amd64 && \
    cd /opt/jre/lib/ && rm -rf ext/jfxrt.jar jfxswt.jar javafx.properties font* && \
    rm /tmp/* /var/cache/apk/*

# Get and install Java
#RUN ln -s /opt/${JDK_VERSION}/bin/java /usr/bin/java
#RUN apk add --no-cache strace
#RUN apk add --allow-untrusted glibc-2.21-r2.apk
RUN ls -l /bin /usr/bin /opt /opt/${JDK_VERSION}/bin
#RUN "strace /opt/jdk1.8.0_121/bin/java -version"
RUN which java
RUN /usr/bin/java -version

# Link Java into use, wget-ssl updates libpthread which causes Java to break
#RUN ln -sf /lib/libpthread-2.18.so /lib/libpthread.so.0 && ln -s /opt/jre1.8.0_40/bin/java /usr/bin/java
 
