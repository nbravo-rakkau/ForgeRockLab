# ForgeRockLab

- am
    - AM-7.5.1.war
    - Amster-7.5.1.zip
    - Dockerfile
- ds
    - DS-7.5.1.zip
    - Dockerfile
- ig
    - .openig/
    - secrets
    - PingGateway-2024.11.0.zip
    - Dockerfile
- tomcat 
    - sample.war
    - Dockerfile

Para levantar el lab ejecutar:
```
docker-compose up --build 
```

Completar la guia (PEM file) https://docs.pingidentity.com/pinggateway/2024.11/installation-guide/securing-connections.html#server-side-tls

Configurar FQDN local
127.0.0.1       ig openam.example.com directory.example.com example.com

Logs:
- AM: /root/openam/var/audit
- IDM: 
    - Arhivo local: /opt/openidm/audit
    - REST: https://docs.pingidentity.com/pingidm/7.5/audit-guide/querying-audit-over-rest.html

Links de referencia:
- Integracion AM - IDM: https://backstage.forgerock.com/docs/platform/7.5/sample-setup/deployment2.html
- Integración AM - IG: https://docs.pingidentity.com/pinggateway/2024.11/gateway-guide/cdsso.html

