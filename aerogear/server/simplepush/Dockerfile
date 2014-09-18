# Use latest jboss/base image as the base
FROM jboss/base

USER root

# Install maven, wget, and git
RUN yum -y install maven wget git && yum clean all

USER jboss

# Clone the SimplePush Server
RUN git clone https://github.com/aerogear/aerogear-simplepush-server aerogear-simplepush-server

WORKDIR aerogear-simplepush-server

# Run a Maven install when installing the image to avoid this cost of downloading the internet (all deps)
RUN mvn --quiet -DskipTests=true -Dmaven.javadoc.skip=true install

WORKDIR server-netty

RUN mvn --quiet dependency:resolve
RUN mvn --quiet dependency:resolve-plugins -DincludeArtifactIds=commons-exec

# Expose the port the SimplePush Server listens to
EXPOSE 7777

CMD ["mvn", "exec:java"]
