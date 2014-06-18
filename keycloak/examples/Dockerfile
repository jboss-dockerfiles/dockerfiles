FROM jboss/keycloak
MAINTAINER jpkroehling@redhat.com

USER wildfly
RUN echo 'JAVA_OPTS="$JAVA_OPTS -Dkeycloak.import=/opt/keycloak/testrealm.json"' >> /opt/wildfly/bin/standalone.conf
ADD files/testrealm.json /opt/keycloak/testrealm.json
ADD files/keycloak-standalone-wildfly-8.1.0.Final.xml /opt/wildfly/standalone/configuration/standalone.xml
ADD files/wars/customer-portal-js.war /opt/wildfly/standalone/deployments/customer-portal-js.war
ADD files/wars/customer-portal.war /opt/wildfly/standalone/deployments/customer-portal.war
ADD files/wars/database.war /opt/wildfly/standalone/deployments/database.war
ADD files/wars/oauth-client-cdi.war /opt/wildfly/standalone/deployments/oauth-client-cdi.war
ADD files/wars/oauth-client.war /opt/wildfly/standalone/deployments/oauth-client.war
ADD files/wars/product-portal.war /opt/wildfly/standalone/deployments/product-portal.war
