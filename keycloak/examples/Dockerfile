# FROM jboss/keycloak-server
FROM jpkroehling/keycloak-server
MAINTAINER jpkroehling@redhat.com

USER wildfly
RUN echo 'JAVA_OPTS="$JAVA_OPTS -Dkeycloak.import=/opt/keycloak/testrealm.json"' >> /opt/wildfly-8.1.0.CR2/bin/standalone.conf
RUN cd /opt/wildfly-8.1.0.CR2 && unzip /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-alpha-4.zip

ADD files/testrealm.json /opt/keycloak/testrealm.json
ADD files/keycloak-standalone-wildfly-8.1.0.CR2.xml /opt/wildfly-8.1.0.CR2/standalone/configuration/standalone.xml
ADD files/wars/customer-portal-js.war /opt/wildfly-8.1.0.CR2/standalone/deployments/customer-portal-js.war
ADD files/wars/customer-portal.war /opt/wildfly-8.1.0.CR2/standalone/deployments/customer-portal.war
ADD files/wars/database.war /opt/wildfly-8.1.0.CR2/standalone/deployments/database.war
ADD files/wars/oauth-client-cdi.war /opt/wildfly-8.1.0.CR2/standalone/deployments/oauth-client-cdi.war
ADD files/wars/oauth-client.war /opt/wildfly-8.1.0.CR2/standalone/deployments/oauth-client.war
ADD files/wars/product-portal.war /opt/wildfly-8.1.0.CR2/standalone/deployments/product-portal.war
