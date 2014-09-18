FROM jboss/base

# Set the IMMUTANT_VERSION env variable
ENV IMMUTANT_VERSION 1.1.4

# Set the IMMUTANT_HOME env variable
ENV IMMUTANT_HOME /opt/jboss/immutant

# Add Immutant
RUN curl https://d33a59li2db06k.cloudfront.net/release/org/immutant/immutant-dist/$IMMUTANT_VERSION/immutant-dist-$IMMUTANT_VERSION-slim.zip | bsdtar -xf - && mv immutant-$IMMUTANT_VERSION-slim immutant && chmod +x /opt/jboss/immutant/jboss/bin/standalone.sh

EXPOSE 8080

# Set the default command to run on boot
# This will boot Immutant in the standalone mode and bind to all interfaces
CMD ["/opt/jboss/immutant/jboss/bin/standalone.sh", "-b", "0.0.0.0"]
