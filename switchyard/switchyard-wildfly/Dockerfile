FROM jboss/wildfly

## If this is in base image, remove form here
USER root
RUN yum -y install bsdtar; yum clean all
USER wildfly

#
# Install switchyard
RUN cd $JBOSS_HOME && curl http://downloads.jboss.org/switchyard/releases/v2.0.Alpha2/switchyard-2.0.0.Alpha2-WildFly.zip | bsdtar -xvf- && chown -R wildfly:wildfly /opt/wildfly
