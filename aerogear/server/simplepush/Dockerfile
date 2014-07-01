# Use latest Fedora image as the base
FROM fedora

# Install java
RUN yum -q -y install java-1.7.0-openjdk-devel wget git && yum -q clean all
ENV JAVA_HOME /usr/lib/jvm/java-1.7.0-openjdk

# Download Maven
RUN wget -O /tmp/apache-maven-3.2.2-bin.tar.gz http://mirror.hosting90.cz/apache/maven/maven-3/3.2.2/binaries/apache-maven-3.2.2-bin.tar.gz
RUN cd /usr/local && tar xzf /tmp/apache-maven-3.2.2-bin.tar.gz
RUN ln -s /usr/local/apache-maven-3.2.2 /usr/local/maven
RUN rm /tmp/apache-maven-3.2.2-bin.tar.gz
ENV MAVEN_HOME /usr/local/maven
ENV PATH $MAVEN_HOME/bin:$PATH

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
