# Use latest Fedora image as the base
FROM fedora
MAINTAINER Bruno Oliveira <bruno@abstractj.org>

# Install OpenJDK, unzip and clean the metadata
RUN yum -q -y install java-1.7.0-openjdk-devel unzip && yum -q clean all

# Set the HOME environment variable
ENV HOME /opt/nodyn

# Set the Java environment variable
ENV JAVA_HOME /usr/lib/jvm/java-1.7.0-openjdk

ENV NODYN_VERSION 0.1.1-20140811.131823-77-bin

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

RUN curl -O https://oss.sonatype.org/content/repositories/snapshots/io/nodyn/nodyn/0.1.1-SNAPSHOT/nodyn-$NODYN_VERSION.zip && unzip nodyn-$NODYN_VERSION.zip -d $HOME/bin/

# Set the default command to run on boot
CMD ["./bin/nodyn"]


