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

#--deploymentKeyPassword password \
RUN ./setup --rootUserDN uid=admin \
            --rootUserPassword Iden2006 \
            --monitorUserPassword Iden2006 \
            --hostname ds \
            --adminConnectorPort 4444 \
            --ldapPort 389 \
            --enableStartTls \
            --ldapsPort 636 \
            --httpPort 80 \
            --httpsPort 443 \
            --profile am-config \
            --set am-config/amConfigAdminPassword:Iden2006 \
            --profile am-cts \
            --set am-cts/amCtsAdminPassword:Iden2006 \
            --set am-cts/tokenExpirationPolicy:am-sessions-only \
            --profile am-identity-store \
            --set am-identity-store/amIdentityStoreAdminPassword:Iden2006 \
            --acceptLicense \
            --deploymentId $(cat /usr/local/deployment_id.txt) \
            --deploymentIdPassword customTestDS123.

CMD ["/usr/local/opendj/bin/start-ds", "--nodetach"]