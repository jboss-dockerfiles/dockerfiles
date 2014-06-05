# Use latest Fedora image as the base
FROM fedora

# Upgrade the system
RUN yum -y update

# Install java
RUN yum -y install java-1.7.0-openjdk-devel unzip

# Clean the metadata
RUN yum clean all

# Add the TorqueBox distribution to /opt
RUN cd /opt && curl -L https://d2t70pdxfgqbmq.cloudfront.net/release/org/torquebox/torquebox-dist/3.1.0/torquebox-dist-3.1.0-bin.zip -o torquebox.zip && unzip -q torquebox.zip && rm torquebox.zip

# Create the torquebox user and group
RUN groupadd -r torquebox -g 434 && useradd -u 432 -r -g torquebox -d /opt/torquebox-3.1.0 -s /sbin/nologin -c "TorqueBox user" torquebox

# Change the owner of the /opt/torquebox-3.1.0 directory
RUN chown -R torquebox:torquebox /opt/torquebox-3.1.0

# Expose the ports we're interested in
EXPOSE 8080

# Run everything below as the torquebox user
USER torquebox

# Set the default command to run on boot
# This will boot TorqueBox and bind to all interface
CMD ["/opt/torquebox-3.1.0/jboss/bin/standalone.sh", "-b", "0.0.0.0"]
