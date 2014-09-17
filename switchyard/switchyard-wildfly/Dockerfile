FROM jboss/wildfly

ENV JBOSS_SY_VERSION 2.0.0.Alpha2
ENV JBOSS_SY_VERSION_MAIN 2.0.Alpha2

#
# Install switchyard
RUN cd $JBOSS_HOME && curl http://downloads.jboss.org/switchyard/releases/v$JBOSS_SY_VERSION_MAIN/switchyard-$JBOSS_SY_VERSION-WildFly.zip | bsdtar -xvf- && chown -R wildfly:wildfly /opt/wildfly
