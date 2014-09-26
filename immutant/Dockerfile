# Use latest Fedora image as the base
FROM fedora

# Update base image
RUN yum -y update && yum clean all

# CVE-2014-7169 is not on all mirrors, better install it directly
RUN rpm -Uvh https://kojipkgs.fedoraproject.org//packages/bash/4.2.48/2.fc20/x86_64/bash-4.2.48-2.fc20.x86_64.rpm

# Install java
RUN yum -y install java-1.7.0-openjdk-devel unzip && yum clean all

# Set the IMMUTANT_VERSION env variable
ENV IMMUTANT_VERSION 1.1.4

# Add Immutant
RUN curl -o /opt/immutant.zip https://d33a59li2db06k.cloudfront.net/release/org/immutant/immutant-dist/$IMMUTANT_VERSION/immutant-dist-$IMMUTANT_VERSION-slim.zip

# Unpack it
RUN unzip -q -d /opt/ /opt/immutant.zip && mv /opt/immutant-$IMMUTANT_VERSION-slim /opt/immutant && rm /opt/immutant.zip

# Create the immutant user and group
RUN groupadd -r immutant -g 413 && useradd -u 444 -r -g immutant -d /opt/immutant -s /sbin/nologin -c "Immutant user" immutant

# Change the owner of the /opt/immutant directory
RUN chown -R immutant:immutant /opt/immutant/*

# Set the IMMUTANT_HOME env variable
ENV IMMUTANT_HOME /opt/immutant/

# Expose the ports we're interested in
EXPOSE 8080

# Run everything below as the wildfly user
USER immutant

# Set the default command to run on boot
# This will boot Immutant in the standalone mode and bind to all interfaces
CMD ["/opt/immutant/jboss/bin/standalone.sh", "-b", "0.0.0.0"]
