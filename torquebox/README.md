# TorqueBox Docker image

This is an example Dockerfile with [TorqueBox application server](http://torquebox.org/).

## Usage

    docker run -it jboss/torquebox

## Extending the image

    FROM jboss/torquebox
    # Do your stuff here

Then you can build the image:

    docker build .

## Building on your own

You don't need to do this on your own, because we prepared an [automated build](https://registry.hub.docker.com/u/jboss/torquebox/) for this repository, but if you really want:

    docker build --tag=jboss/torquebox .

## Source

The source is [available on GitHub](https://github.com/jboss/dockerfiles/tree/master/torquebox).

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss/dockerfiles/issues).
