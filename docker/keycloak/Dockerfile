FROM quay.io/keycloak/keycloak:20.0.2 as builder

# Enable health and metrics support
ENV KC_HEALTH_ENABLED=true
ENV KC_METRICS_ENABLED=true

# Configure database vendor
ENV KC_DB=mysql

WORKDIR /opt/keycloak
RUN /opt/keycloak/bin/kc.sh build --http-relative-path=/auth --features=token-exchange,preview,docker  --spi-login-protocol-openid-connect-legacy-logout-redirect-uri=true

FROM quay.io/keycloak/keycloak:20.0.2
COPY --from=builder /opt/keycloak/ /opt/keycloak/

# Configure a database vendor
ENV KC_PROXY=edge
ENV KC_LOG_LEVEL=INFO

ENV KC_DB_URL=jdbc:mysql://onecard-production.cihyqmknokel.eu-west-2.rds.amazonaws.com:3306/keycloakdb
ENV KC_DB_USERNAME=admin
ENV KC_DB_PASSWORD=JehovahTsidkenu3
ENV KC_HOSTNAME=auth.factorialsystems.io
ENV KC_HOSTNAME_STRICT_HTTPS=true
ENV PROXY_ADDRESS_FORWARDING=true
ENV JMS_USER=admin
ENV JMS_PASSWORD=JehovahTsidkenu3

ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]
CMD ["start", "--optimized"]
