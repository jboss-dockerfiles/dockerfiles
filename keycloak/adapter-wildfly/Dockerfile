FROM jboss/wildfly
MAINTAINER jpkroehling@redhat.com

USER root
RUN yum install -y unzip && yum clean all
RUN mkdir -p /opt/keycloak
ADD https://downloads.sourceforge.net/project/keycloak/1.0-beta-3/keycloak-war-dist-all-1.0-beta-3.zip /tmp/keycloak-war-dist-all-1.0-beta-3.zip
RUN cd /tmp && \
    unzip -q keycloak-war-dist-all-1.0-beta-3.zip && \
    cp /tmp/keycloak-war-dist-all-1.0-beta-3/adapters/keycloak-wildfly-adapter-dist-1.0-beta-3.zip /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-beta-3.zip && \
    cp -R /tmp/keycloak-war-dist-all-1.0-beta-3/deployments /opt/keycloak/ && \
    rm -rf /tmp/keycloak-war-dist-all-1.0-beta-3 && chown wildfly:wildfly -R /opt/keycloak
USER wildfly
RUN cd /opt/wildfly && \
    unzip -q /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-beta-3.zip
# Standalone.xml modifications.
RUN sed -i -e 's/<extensions>/&\n        <extension module="org.keycloak.keycloak-wildfly-subsystem"\/>/' /opt/wildfly/standalone/configuration/standalone.xml && \
    sed -i -e 's/<profile>/&\n        <subsystem xmlns="urn:jboss:domain:keycloak:1.0"\/>/' /opt/wildfly/standalone/configuration/standalone.xml && \
    sed -i -e 's/<security-domains>/&\n                <security-domain name="keycloak">\n                    <authentication>\n                        <login-module code="org.keycloak.adapters.jboss.KeycloakLoginModule" flag="required"\/>\n                    <\/authentication>\n                <\/security-domain>/' /opt/wildfly/standalone/configuration/standalone.xml
