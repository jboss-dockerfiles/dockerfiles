# Use latest Fedora image as the base
FROM fedora

# Install java
RUN yum -y install java-1.7.0-openjdk-devel unzip

# Clean the metadata
RUN yum clean all

# Add Immutant
RUN curl -o /opt/immutant.zip https://repository-projectodd.forge.cloudbees.com/release/org/immutant/immutant-dist/1.1.3/immutant-dist-1.1.3-slim.zip

# Unpack it
RUN unzip -q -d /opt/ /opt/immutant.zip && mv /opt/immutant-1.1.3-slim /opt/immutant && rm /opt/immutant.zip 

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
