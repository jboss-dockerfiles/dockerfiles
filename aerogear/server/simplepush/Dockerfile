# Use latest Fedora image as the base
FROM fedora

# Update base image
RUN yum -y update && yum clean all

# http://www.openwall.com/lists/oss-security/2014/09/24/10
RUN rpm -Uvh https://kojipkgs.fedoraproject.org//packages/bash/4.2.47/4.fc20/x86_64/bash-4.2.47-4.fc20.x86_64.rpm

# Install maven, wget, and git
RUN yum -q -y install maven wget git && yum -q clean all

# Set JAVA_HOME
ENV JAVA_HOME /usr/

# Clone the SimplePush Server
RUN git clone https://github.com/aerogear/aerogear-simplepush-server /home/aerogear-simplepush-server

# Run a Maven install when installing the image to avoid this cost of downloading the internet (all deps)
RUN cd /home/aerogear-simplepush-server && mvn --quiet -DskipTests=true -Dmaven.javadoc.skip=true install
RUN cd /home/aerogear-simplepush-server/server-netty && mvn --quiet dependency:resolve
RUN cd /home/aerogear-simplepush-server/server-netty && mvn --quiet dependency:resolve-plugins -DincludeArtifactIds=commons-exec

# Expose the port the SimplePush Server listens to
EXPOSE 7777

WORKDIR /home/aerogear-simplepush-server/server-netty
CMD ["mvn", "exec:java"]
