FROM tomcat:9.0.98-jre17-temurin
ARG AM_VERSION=7.5.1

RUN apt-get -y update && apt-get install -y procps && apt-get install -y unzip && apt-get -y clean

RUN rm -rf /usr/local/tomcat/webapps/docs/ && \
    rm -rf /usr/local/tomcat/webapps/examples/ && \
    rm -rf /usr/local/tomcat/webapps/manager/

# Expose  /.well-known/assets.json
#COPY ROOT /usr/local/tomcat/webapps/ROOT

#WORKDIR /root
#COPY *.sh ./

ADD Amster-${AM_VERSION}.zip .
RUN unzip Amster*.zip -d /root && rm Amster*.zip

COPY AM-${AM_VERSION}.war /usr/local/tomcat/webapps/openam.war

RUN apt-get update && apt-get install -y vim
RUN apt-get update && apt-get install -y bash

#RUN echo '#!/bin/bash' > /usr/local/tomcat/bin/setenv.sh && \
#    echo 'CATALINA_OPTS="$CATALINA_OPTS -Djavax.net.ssl.trustStore=/root/openam-security/truststore"' >> /usr/local/tomcat/bin/setenv.sh && \
#    echo 'CATALINA_OPTS="$CATALINA_OPTS -Djavax.net.ssl.trustStorePassword=changeit"' >> /usr/local/tomcat/bin/setenv.sh && \
#    echo 'CATALINA_OPTS="$CATALINA_OPTS -Djavax.net.ssl.trustStoreType=jks"' >> /usr/local/tomcat/bin/setenv.sh && \
#    chmod +x /usr/local/tomcat/bin/setenv.sh