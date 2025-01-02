FROM eclipse-temurin:17-alpine
ARG IDM_VERSION=7.5.0

ENV INSTALL_DIR /opt/openidm

RUN apk update && apk add --no-cache \
    unzip \
    bash

WORKDIR /opt
ADD IDM-${IDM_VERSION}.zip .
RUN unzip IDM-${IDM_VERSION}.zip && \
    rm IDM-${IDM_VERSION}.zip 

EXPOSE 8080 8443

RUN mkdir -p ${INSTALL_DIR}/logs

ENTRYPOINT ${INSTALL_DIR}/startup.sh
