# LiveOak Server Docker Image

This image provides basic distribution of LiveOak. 

## Usage

To boot in standalone mode

    docker run -it -p 8080:8080 -p 9090:9090 jboss/liveoak-server

Once it boots go to http://<host>:8080/admin/

You can login using admin/admin for the first login. 

