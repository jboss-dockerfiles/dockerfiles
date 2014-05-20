# FROM jboss/wildfly
FROM goldmann/wildfly
MAINTAINER jpkroehling@redhat.com

USER root
RUN yum install -y unzip

USER wildfly
RUN cd /tmp && curl -L http://downloads.sourceforge.net/project/keycloak/1.0-alpha-4/keycloak-war-dist-all-1.0-alpha-4.zip -o keycloak-war-dist-all-1.0-alpha-4.zip && unzip -q keycloak-war-dist-all-1.0-alpha-4.zip
RUN cp -R /tmp/keycloak-war-dist-all-1.0-alpha-4/deployments/ /opt/wildfly-8.1.0.CR2/standalone/deployments/

