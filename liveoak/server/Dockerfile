FROM jboss/base

USER root
RUN yum -y install java-1.8.0-openjdk-devel && yum clean all
USER jboss

ENV LIVEOAK_VERSION 1.0.0.Alpha02
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0

RUN curl -L http://repository.liveoak.io/io/liveoak/liveoak-dist/$LIVEOAK_VERSION/liveoak-dist-$LIVEOAK_VERSION.tar.gz | tar zx

# Expose the ports we're interested in
EXPOSE 8080 8383 9990

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/jboss/liveoak/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
