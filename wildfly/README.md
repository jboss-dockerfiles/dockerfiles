# WildFly Docker image

This is an example Dockerfile with [WildFly application server](http://wildfly.org/).

## Usage

To boot in standalone mode

    docker run -it jboss/wildfly

To boot in domain mode

    docker run -it jboss/wildfly /opt/wildfly/bin/domain.sh -b 0.0.0.0 -bmanagement 0.0.0.0

## Application deployment

With the WildFly server you can [deploy your application in multiple ways](https://docs.jboss.org/author/display/WFLY8/Application+deployment):

1. You can use CLI
2. You can use the web console
3. You can use the management API directly
4. You can use the deployment scanner

The most popular way of deploying an application is using the deployment scanner. In WildFly this method is enabled by default and the only thing you need to do is to place your application inside of the `deployments/` directory. It can be `/opt/wildfly/standalone/deployments/` or `/opt/wildfly/domain/deployments/` depending on [which mode](https://docs.jboss.org/author/display/WFLY8/Operating+modes) you choose (standalone is default in the `jboss/wildfly` image -- see above).

The best way to deploy an application with the `jboss/wildfly` image is to extend it. Just place your application inside the `deployments/` directory with the `ADD` command. You can also do the changes to the configuration (if any) as additional steps (`RUN` command).  Make sure to include the trailing slash on the deployment folder path.

    FROM jboss/wildfly
    ADD your-awesome-app.war /opt/wildfly/standalone/deployments/

Then you can build the image:

    docker build --tag=wildfly-application .

This way of deployment is great because of a few things:

1. It utilizes Docker as the build tool providing stable builds
2. Rebuilding image this way is very fast (once again: Docker)
3. You only need to do changes to the base WildFly image that are required to run your application

## Extending the image

To be able to create a management user to access the administration console create a Dockerfile with the following content

    FROM jboss/wildfly
    RUN /opt/wildfly/bin/add-user.sh admin Admin#70365 --silent

Then you can build the image:

    docker build --tag=jboss/wildfly-admin .

Run it:

    docker run -it -p 9990:9990 jboss/wildfly-admin

The administration console should be available at http://localhost:9990.

## Building on your own

You don't need to do this on your own, because we prepared a trusted build for this repository, but if you really want:

    docker build --rm=true --tag=jboss/wildfly .

## Source

The source is [available on GitHub](https://github.com/jboss/dockerfiles/tree/master/wildfly).

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss/dockerfiles/issues).
