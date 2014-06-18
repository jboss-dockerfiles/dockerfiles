FROM jboss/wildfly
MAINTAINER jpkroehling@redhat.com

USER root
RUN yum install -y unzip && yum clean all
RUN mkdir -p /opt/keycloak
ADD https://downloads.sourceforge.net/project/keycloak/1.0-beta-2/keycloak-war-dist-all-1.0-beta-2.zip /tmp/keycloak-war-dist-all-1.0-beta-2.zip
RUN cd /tmp && unzip -q keycloak-war-dist-all-1.0-beta-2.zip && cp /tmp/keycloak-war-dist-all-1.0-beta-2/adapters/keycloak-wildfly-adapter-dist-1.0-beta-2.zip /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-beta-2.zip && cp -R /tmp/keycloak-war-dist-all-1.0-beta-2/deployments /opt/keycloak/ && rm -rf /tmp/keycloak-war-dist-all-1.0-beta-2 && chown wildfly:wildfly -R /opt/keycloak 
USER wildfly
RUN cd /opt/wildfly && unzip -q /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-beta-2.zip
