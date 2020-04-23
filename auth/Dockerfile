# using this intermediate container to get executable permissions for the script
FROM busybox AS bb

ADD config-kc-for-dr-one /usr/local/bin/
RUN chmod +x /usr/local/bin/config-kc-for-dr-one


FROM jboss/keycloak:9.0.3

ADD drone-realm-export.json /tmp
COPY --from=bb /usr/local/bin/config-kc-for-dr-one /usr/local/bin/config-kc-for-dr-one
