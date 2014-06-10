# WildFly Docker image

This is an example Dockerfile with [WildFly application server](http://wildfly.org/).

## Usage

To boot in standalone mode

    docker run -it jboss/wildfly

To boot in domain mode

    docker run -it jboss/wildfly /opt/wildfly/bin/domain.sh -b 0.0.0.0 -bmanagement 0.0.0.0

## Extending the image

To be able to create a management user to access the administration console create a Dockerfile with the following content

    FROM jboss/wildfly
    RUN /opt/wildfly/bin/add-user.sh admin Admin#70365 --silent

Then you can build the image:

    docker build --rm=true --tag=jboss/wildfly-admin .

Run it:

    docker run -it -p 9990:9990 jboss/wildfly-admin

The administration console should be available at http://localhost:9990.

## Building on your own

You don't need to do this on your own, because we prepared a trusted build for this repository, but if you really want:

    docker build --rm=true --tag=jboss/wildfly .

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss/dockerfiles/issues).
