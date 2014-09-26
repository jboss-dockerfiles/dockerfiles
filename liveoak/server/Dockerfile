# Use latest Fedora image as the base
FROM fedora

# Upgrade the system
RUN yum -y update && yum clean all

# Install java
RUN yum -y install java-1.8.0-openjdk-devel wget && yum clean all

# Add the LiveOak distribution to /opt
RUN cd /opt && wget http://repository.liveoak.io/io/liveoak/liveoak-dist/1.0.0.Alpha02/liveoak-dist-1.0.0.Alpha02.tar.gz && tar -zxf liveoak-dist-1.0.0.Alpha02.tar.gz

# Create the wildfly user and group
RUN groupadd -r liveoak -g 433 && useradd -u 431 -r -g liveoak -d /opt/liveoak -s /sbin/nologin -c "LiveOak user" liveoak

# Change the owner of the /opt/liveoak directory
RUN chown -R liveoak:liveoak /opt/liveoak

# Expose the ports we're interested in
EXPOSE 8080 8383 9990

# Run everything below as the liveoak user
USER liveoak

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/liveoak/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]

