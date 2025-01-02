FROM tomcat:9.0.98

RUN apt-get update && apt-get install -y iputils-ping
RUN apt-get update && apt-get install -y \
    netcat-openbsd \
    curl \
    iproute2 \
    telnet

WORKDIR /usr/local/tomcat/webapps/
ADD sample.war ./