FROM jboss/wildfly
MAINTAINER jpkroehling@redhat.com

ENV KEYCLOAK_VERSION 1.0-rc-2

USER root
RUN yum install -y unzip && yum clean all
RUN mkdir -p /opt/keycloak
ADD https://downloads.sourceforge.net/project/keycloak/$KEYCLOAK_VERSION/keycloak-war-dist-all-$KEYCLOAK_VERSION.zip /tmp/keycloak-war-dist-all-$KEYCLOAK_VERSION.zip
RUN cd /tmp && \
    unzip -q keycloak-war-dist-all-$KEYCLOAK_VERSION.zip && \
    cp /tmp/keycloak-war-dist-all-$KEYCLOAK_VERSION/adapters/keycloak-wildfly-adapter-dist-$KEYCLOAK_VERSION.zip /opt/keycloak/keycloak-wildfly-adapter-dist-$KEYCLOAK_VERSION.zip && \
    cp -R /tmp/keycloak-war-dist-all-$KEYCLOAK_VERSION/deployments /opt/keycloak/ && \
    rm -rf /tmp/keycloak-war-dist-all-$KEYCLOAK_VERSION && chown wildfly:wildfly -R /opt/keycloak
USER wildfly
RUN cd /opt/wildfly && \
    unzip -q /opt/keycloak/keycloak-wildfly-adapter-dist-$KEYCLOAK_VERSION.zip
# Standalone.xml modifications.
RUN sed -i -e 's/<extensions>/&\n        <extension module="org.keycloak.keycloak-wildfly-subsystem"\/>/' /opt/wildfly/standalone/configuration/standalone.xml && \
    sed -i -e 's/<profile>/&\n        <subsystem xmlns="urn:jboss:domain:keycloak:1.0"\/>/' /opt/wildfly/standalone/configuration/standalone.xml && \
    sed -i -e 's/<security-domains>/&\n                <security-domain name="keycloak">\n                    <authentication>\n                        <login-module code="org.keycloak.adapters.jboss.KeycloakLoginModule" flag="required"\/>\n                    <\/authentication>\n                <\/security-domain>/' /opt/wildfly/standalone/configuration/standalone.xml
