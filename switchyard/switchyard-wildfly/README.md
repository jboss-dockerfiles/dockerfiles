# SwitchYard Docker image

This is an example Dockerfile with [SwitchYard SCA engine on Wildfly](http://switchyard.jboss.org/).

## Usage

    docker run -it jboss/switchyard-wildfly

## To boot in domain mode:

    docker run -it jboss/switchyard-wildfly /opt/wildfly/bin/domain.sh -b 0.0.0.0 -bmanagement 0.0.0.0   

## Extending the image

    FROM jboss/switchyard-wildfly
    # Do your stuff here

## Application deployment

With the SwitchYard server you can deploy your application in multiple ways:

- You can use CLI
- You can use the web console
- You can use the management API directly
- You can use the deployment scanner
 
The most popular way of deploying an application is using the deployment scanner. In SwitchYard this method is enabled by default and the only thing you need to do is to place your application inside of the deployments/ directory. It can be /opt/wildfly/standalone/deployments/ or /opt/wildfly/domain/deployments/ depending on which mode you choose (standalone is default in the jboss/switchyard-wildfly image -- see above).
 
The simplest and cleanest way to deploy an application to SwitchYard running in a container started from the jboss/switchyard-wildfly image is to use the deployment scanner method mentioned above.
 
To do this you just need to extend the jboss/switchyard-wildfly image by creating a new one. Place your application inside the deployments/ directory with the ADD command (but make sure to include the trailing slash on the deployment folder path, more info). You can also do the changes to the configuration (if any) as additional steps (RUN command).
 
A simple example was prepared to show how to do it, but the steps are following:

Create Dockerfile with following content:

    FROM jboss/switchyard-wildfly  
    ADD your-switchyard-app.jar /opt/wildfly/standalone/deployments/  

Place your your-switchyard-app.jar file in the same directory as your Dockerfile.  

Run the build:

    docker build --tag=switchyard-app ."  

Run the container with

    docker run -it switchyard-app  

Application will be deployed on the container boot.
 
 
This way of deployment is great because of a few things:
- It utilizes Docker as the build tool providing stable builds
- Rebuilding image this way is very fast (once again: Docker)

You only need to do changes to the base SwitchYard image that are required to run your application
 
## Extending the image examples

To be able to create a management user to access the administration console create a Dockerfile with the following content

    FROM jboss/switchyard-wildfly  
    RUN /opt/wildfly/bin/add-user.sh admin Admin#70365 --silent  
 
Then you can build the image:

    docker build --tag=jboss/switchyard-wildfly-admin .  
 
Run it:

    docker run -it -p 9990:9990 jboss/switchyard-wildfly-admin  
 
The administration console should be available at http://localhost:9990.
 
## Debug in a container

If you want to debug an application deployed in this SwitchYard container, create a Dockerfile with the following conte

    FROM jboss/switchyard-wildfly  
    RUN /opt/wildfly/bin/add-user.sh admin Admin#70365 --silent  
    # Default wildfly debug port  
    EXPOSE 8787  
 
 
Then you can build the image:

    docker build --tag=jboss/switchyard-debug .  
 
Run it:

    docker run -it -p 8787:8787 jboss/switchyard-debug  /opt/wildfly/bin/domain.sh --debug  

## Working with file based gateways

If you are working with applications that need access to file, and want to access these files from the host machine, you can add some volumes to your container, and use those paths in your applications.

    docker run -it -v /tmp/input:/input -v /tmp/output:/output jboss/switchyard-wildfly-admin  
    
_NOTE_: These paths must exist and be readable/writable by the jboss user used in the container.

## Building on your own

You don't need to do this on your own, because we prepared an [automated build](https://registry.hub.docker.com/u/jboss/switchyard-wildfly/) for this repository, but if you really want:

    docker build --tag=jboss/switchyard-wildfly .

## Source

The source is [available on GitHub](https://github.com/jboss/dockerfiles/tree/master/switchyard-wildfly).

## Version

Current/Latest SwitchYard release is: 2.0.Alpha3

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss/dockerfiles/issues).
