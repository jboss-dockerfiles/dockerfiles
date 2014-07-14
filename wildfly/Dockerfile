# Use latest Fedora image as the base
FROM fedora

# Install java
RUN yum -y install java-1.7.0-openjdk-devel

# Clean the metadata
RUN yum clean all

# Add the WildFly distribution to /opt
RUN cd /opt && curl http://download.jboss.org/wildfly/8.1.0.Final/wildfly-8.1.0.Final.tar.gz | tar zx

# Make sure the distribution is available from a well-known place
RUN ln -s /opt/wildfly-8.1.0.Final /opt/wildfly

# Create the wildfly user and group
RUN groupadd -r wildfly -g 433 && useradd -u 431 -r -g wildfly -d /opt/wildfly -s /sbin/nologin -c "WildFly user" wildfly

# Change the owner of the /opt/wildfly directory
RUN chown -R wildfly:wildfly /opt/wildfly*

# Expose the ports we're interested in
EXPOSE 8080 9990

# Run everything below as the wildfly user
USER wildfly

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
