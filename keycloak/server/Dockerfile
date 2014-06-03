# FROM jboss/wildfly
FROM goldmann/wildfly
MAINTAINER jpkroehling@redhat.com

USER root
RUN yum install -y unzip && yum clean all
RUN mkdir -p /opt/keycloak
ADD https://downloads.sourceforge.net/project/keycloak/1.0-beta-2/keycloak-war-dist-all-1.0-beta-2.zip /tmp/keycloak-war-dist-all-1.0-beta-2.zip
RUN chown wildfly:wildfly /tmp/keycloak-war-dist* /opt/keycloak

USER wildfly
RUN cd /tmp && unzip -q keycloak-war-dist-all-1.0-beta-2.zip
RUN cp /tmp/keycloak-war-dist-all-1.0-beta-2/adapters/keycloak-wildfly-adapter-dist-1.0-beta-2.zip /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-beta-2.zip
RUN cp -R /tmp/keycloak-war-dist-all-1.0-beta-2/deployments/ /opt/wildfly/standalone/deployments/
RUN rm -rf /tmp/keycloak-war-dist-all-*
