FROM jboss/keycloak:14.0.0

ADD cli/TCPPING.cli /opt/jboss/tools/cli/jgroups/discovery/
ADD cli/JDBC_PING.cli /opt/jboss/tools/cli/jgroups/discovery/
HEALTHCHECK --interval=30s --timeout=1s --retries=3 CMD curl -k --fail http://localhost:8080/auth/ || exit 1