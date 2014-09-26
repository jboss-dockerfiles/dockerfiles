# Use latest Fedora image as the base
FROM fedora

# Update base image
RUN yum -y update && yum clean all

# Install java and clean yum metadata post installation
RUN yum -y install java-1.7.0-openjdk-devel unzip && yum clean all

ENV TORQUEBOX_VERSION 3.1.1

# Add the TorqueBox distribution to /opt
RUN cd /opt && curl -L https://d2t70pdxfgqbmq.cloudfront.net/release/org/torquebox/torquebox-dist/$TORQUEBOX_VERSION/torquebox-dist-$TORQUEBOX_VERSION-bin.zip -o torquebox.zip && unzip -q torquebox.zip && rm torquebox.zip

# Create the torquebox user and group
RUN groupadd -r torquebox -g 434 && useradd -u 432 -r -g torquebox -d /opt/torquebox-$TORQUEBOX_VERSION -s /sbin/nologin -c "TorqueBox user" torquebox

# Change the owner of the /opt/torquebox directory
RUN chown -R torquebox:torquebox /opt/torquebox-$TORQUEBOX_VERSION

# Expose the ports we're interested in
EXPOSE 8080

# Run everything below as the torquebox user
USER torquebox

# Set the default command to run on boot
# This will boot TorqueBox and bind to all interface
CMD /opt/torquebox-$TORQUEBOX_VERSION/jboss/bin/standalone.sh -b 0.0.0.0
