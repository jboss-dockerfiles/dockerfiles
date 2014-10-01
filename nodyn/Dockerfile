# Use latest Fedora image as the base
FROM fedora:latest
MAINTAINER Bruno Oliveira <bruno@abstractj.org>

# Update base image
RUN yum -y update && yum clean all

# Install OpenJDK, unzip and clean the metadata
RUN yum -y install java-1.7.0-openjdk-devel unzip && yum clean all

# Set the HOME environment variable
ENV HOME /opt/nodyn

# Set the Java environment variable
ENV JAVA_HOME /usr/lib/jvm/java-1.7.0-openjdk

ENV NODYN_VERSION 0.1.1-20140922.164208-175

# General system variable setup
ENV PATH $JAVA_HOME/bin:$M2_HOME/bin:$HOME/nodyn/bin:$PATH

# Create the nodyn user
RUN useradd -m nodyn -d /opt/nodyn -s /sbin/nologin

# Change owner of the /opt/nodyn directory
RUN chown -R nodyn /opt/nodyn

# Change group of the /opt/nodyn directory
RUN chgrp -R users /opt/nodyn

# Run everything below as nodyn user
USER nodyn

# Switch to the working dir /opt/nodyn
WORKDIR /opt/nodyn

RUN curl -O https://oss.sonatype.org/content/repositories/snapshots/io/nodyn/nodyn/0.1.1-SNAPSHOT/nodyn-$NODYN_VERSION-bin.zip && unzip nodyn-$NODYN_VERSION-bin.zip -d $HOME/bin/

# Set the default command to run on boot
CMD ["./bin/nodyn"]


