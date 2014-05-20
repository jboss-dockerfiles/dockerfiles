# Keycloak Auth Server Docker image

This image prepares a basic Keycloak Auth Server. 

## Usage

To boot in standalone mode

    docker run -it -p 8080:8080 -p 9090:9090 jboss/keycloak-server

To boot in domain mode

    docker run -it -p 8080:8080 -p 9090:9090 jboss/keycloak-server /opt/wildfly-8.1.0.CR2/bin/domain.sh -b 0.0.0.0 -bmanagement 0.0.0.0

Once it boots, you can login using admin/admin for the first login. 

## Other details

This image inherits from the main Wildfly image (jboss/wildfly), and deploys the Keycloak artifacts required to start a new authentication server.
Note that you might want to extend the image to make it use a production-ready database and to setup a Wildfly admin password.
