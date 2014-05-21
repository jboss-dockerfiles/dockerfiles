# Keycloak Auth Server Docker image with Examples

This image prepares a basic Keycloak Auth Server and deploys the examples.

## Usage

To boot in standalone mode

    docker run -it -p 8080:8080 -p 9090:9090 jboss/keycloak-examples

Domain mode is not supported on this version, as this image ships with a custom standalone.xml file. 

Once it boots, you can login using admin/admin for the first login on the [Auth server](http://localhost:8080/auth/admin/) or as bburke@redhat.com/password on the [Customer Portal sample application](http://localhost:8080/customer-portal/customers/view.jsp) 

## Other details

This image inherits from the main Keycloak Auth Server image (jboss/keycloak-server), and deploys the Keycloak artifacts required to start a new authentication server, as well as the examples. Additionally, it configures a testrealm and ships with a custom standalone.xml , with the required changes for an application to authenticate using Keycloak as authentication mechanism. 

Note that you might want to extend the image to make it use a production-ready database and to setup a Wildfly admin password.
