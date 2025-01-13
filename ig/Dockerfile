FROM eclipse-temurin:21-alpine
ARG IG_VERSION=2024.11.0

#
# Default install directory for IG. Override this to set a different location.
#
ENV INSTALL_DIR /opt/identity-gateway-${IG_VERSION}

WORKDIR /opt
ADD PingGateway-${IG_VERSION}.zip .
RUN unzip PingGateway-${IG_VERSION}.zip && \
    rm PingGateway-${IG_VERSION}.zip && \
    chown -R root:root "${INSTALL_DIR}" && \
    chmod -R g+rwx "${INSTALL_DIR}"

#
# Default home for IG config. Override this to set a different location.
#
ENV IG_INSTANCE_DIR /var/ig

RUN mkdir -p "${IG_INSTANCE_DIR}" \
    && chown -R root:root "${IG_INSTANCE_DIR}" "${INSTALL_DIR}" \
    && chmod -R g+rwx "${IG_INSTANCE_DIR}" "${INSTALL_DIR}"

USER root

RUN apk update && apk add iputils
RUN apk update && apk add --no-cache \
    netcat-openbsd \
    curl \
    iproute2 \
    busybox-extras

ENV IG_RUN_MODE=development
ENV AGENT_SECRET_ID=UGluZ0FnZW50MjAyNC4=
#ENTRYPOINT ROOT_LOG_LEVEL=DEBUG ${INSTALL_DIR}/bin/start.sh ${IG_INSTANCE_DIR}
ENTRYPOINT ${INSTALL_DIR}/bin/start.sh ${IG_INSTANCE_DIR}