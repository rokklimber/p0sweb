FROM java/alpinejavabox-1.8
MAINTAINER Michael Foy version: 0.1

# set jdk name
ARG MVN_VERSION=3.3.9
ARG MVN_NM=apache-maven-${MVN_VERSION}

# Udate wget to support SSL
ADD ${MVN_NM}.tar.bz2 /opt
ADD settings.xml /root/.m2/settings.xml
ADD osgi.tar.bz2 /opt/felix-ctx
RUN (cd /usr/bin && ln -s /opt/apache-maven-${MVN_VERSION}/bin/mvn mvn)
#ADD jre.tar.gz /opt

# add JAVA_HOME to system shell profile
ADD profile.patch /tmp
RUN (cd /etc && patch profile < /tmp/profile.patch && rm /tmp/profile.patch && source /etc/profile)

# Link Java into use, wget-ssl updates libpthread which causes Java to break
#RUN ln -sf /lib/libpthread-2.18.so /lib/libpthread.so.0 && ln -s /opt/jre1.8.0_40/bin/java /usr/bin/java
 
