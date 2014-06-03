# FROM jboss/wildfly
FROM goldmann/wildfly
MAINTAINER jpkroehling@redhat.com

USER root
RUN yum install -y unzip && yum clean all
RUN mkdir -p /opt/keycloak
ADD http://downloads.sourceforge.net/project/keycloak/1.0-alpha-4/keycloak-war-dist-all-1.0-alpha-4.zip /tmp/keycloak-war-dist-all-1.0-alpha-4.zip
RUN chown wildfly:wildfly /tmp/keycloak-war-dist* /opt/keycloak

USER wildfly
RUN cd /tmp && unzip -q keycloak-war-dist-all-1.0-alpha-4.zip
RUN cp /tmp/keycloak-war-dist-all-1.0-alpha-4/adapters/keycloak-wildfly-adapter-dist-1.0-alpha-4.zip /opt/keycloak/keycloak-wildfly-adapter-dist-1.0-alpha-4.zip
RUN cp -R /tmp/keycloak-war-dist-all-1.0-alpha-4/deployments/ /opt/wildfly-8.1.0.CR2/standalone/deployments/
RUN rm -rf /tmp/keycloak-war-dist-all-*
