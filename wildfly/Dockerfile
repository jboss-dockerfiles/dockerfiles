# Use latest Fedora image as the base
FROM fedora

# Upgrade the system
RUN yum -y update

# Install java
RUN yum -y install java-1.7.0-openjdk-devel

# Clean the metadata
RUN yum clean all

# Add the WildFly distribution to /opt
RUN cd /opt && curl http://download.jboss.org/wildfly/8.1.0.CR2/wildfly-8.1.0.CR2.tar.gz | tar zx

# Create the wildfly user and group
RUN groupadd -r wildfly -g 433 && useradd -u 431 -r -g wildfly -d /opt/wildfly-8.1.0.CR2 -s /sbin/nologin -c "WildFly user" wildfly

# Change the owner of the /opt/wildfly directory
RUN chown -R wildfly:wildfly /opt/wildfly-8.1.0.CR2

# Expose the ports we're interested in
EXPOSE 8080 9990

# Run everything below as the wildfly user
USER wildfly

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/wildfly-8.1.0.CR2/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
