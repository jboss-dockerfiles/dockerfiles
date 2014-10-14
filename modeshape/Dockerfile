FROM jboss/wildfly:latest

# Temporary until we get base image
USER root
RUN yum install -y unzip && yum clean all
USER wildfly

ENV MODESHAPE_VERSION 4.0.0.Final

WORKDIR /opt/wildfly

RUN curl -o modeshape.zip http://downloads.jboss.org/modeshape/$MODESHAPE_VERSION/modeshape-$MODESHAPE_VERSION-jboss-wf8-dist.zip && unzip -q modeshape.zip && rm modeshape.zip

CMD ["/opt/wildfly/bin/standalone.sh", "-c", "standalone-modeshape.xml", "-b", "0.0.0.0"]
