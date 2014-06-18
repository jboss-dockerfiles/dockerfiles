# Immutant Docker image

This is an example Dockerfile with [Immutant application server](http://immutant.org/).

## Usage

    docker run -it jboss/immutant

## Extending the image

    FROM jboss/immutant
    # Do your stuff here

Then you can build the image:

    docker build .

## Building on your own

You don't need to do this on your own, because we prepared an [automated build](https://registry.hub.docker.com/u/jboss/immutant/) for this repository, but if you really want:

    docker build --rm=true --tag=jboss/immutant .

## Source

The source is [available on GitHub](https://github.com/jboss/dockerfiles/tree/master/immutant).

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss/dockerfiles/issues).
