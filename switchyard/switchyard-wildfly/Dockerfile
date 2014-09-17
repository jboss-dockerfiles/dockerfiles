FROM jboss/wildfly

USER root
RUN yum -y install bsdtar; yum clean all

USER wildfly

#
# Install switchyard
RUN cd $JBOSS_HOME && curl http://downloads.jboss.org/switchyard/releases/v2.0.Alpha2/switchyard-2.0.0.Alpha2-WildFly.zip | bsdtar -xvf- && chown -R wildfly:wildfly /opt/wildfly

#
# Enable port for debugging with --debug
EXPOSE 8787

#ENTRYPOINT ["/opt/wildfly/bin/standalone.sh"]
#CMD []
