# ModeShape Docker image
This image prepares the environment required to run [ModeShape](http://modeshape.jboss.org/) on top of WildFly 8.

## Install Docker

Follow the [instructions](http://docs.docker.com/installation/)

## Running the image

`docker run -it jboss/modeshape`

## Building the image (alternative)

Clone the repo and build yourself:

`docker build -t jboss/modeshape .`

## Contributing

Patches are welcome, just send a pull request and I will be happy on merging it. If you want more images, [open issues
with the request](https://github.com/jboss/dockerfiles/issues).
