# SwitchYard Docker image

This is an example Dockerfile with [SwitchYard SCA engine on Wildfly](http://switchyard.jboss.org/).

## Usage

    docker run -it jboss/switchyard-wildfly

## Extending the image

    FROM jboss/switchyard-wildfly
    # Do your stuff here

This image is extending jboss/wildfly so all the extension options that exist for that image, exists also for this one. [Chek it on GitHub](https://github.com/jboss/dockerfiles/tree/master/wildfly)

Then you can build the image:

    docker build .

## Building on your own

You don't need to do this on your own, because we prepared an [automated build](https://registry.hub.docker.com/u/jboss/switchyard-wildfly/) for this repository, but if you really want:

    docker build --tag=jboss/switchyard-wildfly .

## Source

The source is [available on GitHub](https://github.com/jboss/dockerfiles/tree/master/switchyard-wildfly).

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss/dockerfiles/issues).
