FROM eclipse-temurin:17-alpine

EXPOSE 389
EXPOSE 636
EXPOSE 80
EXPOSE 443
EXPOSE 4444
EXPOSE 8989

WORKDIR /usr/local
ADD DS*.zip .
RUN apk add bash && \
    echo -e "fs.file-max=65536\nfs.inotify.max_user_watches=524288" >> /etc/sysctl.conf && \
    unzip DS*.zip && \
    rm DS*.zip

WORKDIR /usr/local/opendj

# Crear el deploymentId usando dskeymgr
RUN ./bin/dskeymgr create-deployment-id --deploymentIdPassword customTestDS123. > /usr/local/deployment_id.txt

# HEALTHCHECK --start-period=30s CMD bin/status -h localhost -p 4444 -D "uid=admin" -w Iden2006 --trustAll

RUN ./setup --deploymentId $(cat /usr/local/deployment_id.txt) \
            --deploymentIdPassword customTestDS123. \
            --rootUserDN uid=admin \
            --rootUserPassword str0ngAdm1nPa55word \
            --monitorUserPassword str0ngMon1torPa55word \
            --hostname directory.example.com \
            --adminConnectorPort 4444 \
            --ldapPort 1389 \
            --enableStartTls \
            --ldapsPort 1636 \
            --profile am-config \
            --set am-config/amConfigAdminPassword:5up35tr0ng \
            --profile am-cts \
            --set am-cts/amCtsAdminPassword:5up35tr0ng \
            --set am-cts/tokenExpirationPolicy:am-sessions-only \
            --profile am-identity-store \
            --set am-identity-store/amIdentityStoreAdminPassword:5up35tr0ng \
            --profile idm-repo \
            --set idm-repo/domain:forgerock.io \
            --acceptLicense

CMD ["/usr/local/opendj/bin/start-ds", "--nodetach"]