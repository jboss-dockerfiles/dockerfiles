FROM jboss/wildfly
MAINTAINER jpkroehling@redhat.com

ENV KEYCLOAK_VERSION 1.0.1.Final

WORKDIR /opt/jboss/wildfly

RUN curl -L https://downloads.sourceforge.net/project/keycloak/$KEYCLOAK_VERSION/keycloak-war-dist-all-$KEYCLOAK_VERSION.zip | bsdtar -xOf - keycloak-war-dist-all-$KEYCLOAK_VERSION/adapters/keycloak-wildfly-adapter-dist-$KEYCLOAK_VERSION.zip | bsdtar -xf -

# Standalone.xml modifications.
RUN sed -i -e 's/<extensions>/&\n        <extension module="org.keycloak.keycloak-wildfly-subsystem"\/>/' standalone/configuration/standalone.xml && \
    sed -i -e 's/<profile>/&\n        <subsystem xmlns="urn:jboss:domain:keycloak:1.0"\/>/' standalone/configuration/standalone.xml && \
    sed -i -e 's/<security-domains>/&\n                <security-domain name="keycloak">\n                    <authentication>\n                        <login-module code="org.keycloak.adapters.jboss.KeycloakLoginModule" flag="required"\/>\n                    <\/authentication>\n                <\/security-domain>/' standalone/configuration/standalone.xml
