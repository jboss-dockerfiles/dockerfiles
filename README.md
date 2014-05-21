# JBoss Dockerfiles

This repository contains examples of Dockerfiles that can be used to build Docker images with [JBoss Community projects](http://www.jboss.org/).

## Usage

### Trusted builds

This repository will eventually be hooked with [docker.io trusted builds feature](https://index.docker.io/help/docs/#trustedbuilds). This will ensure that https://index.docker.io/ will always have up to date images. We're working on it.

### Building locally

You can assume that running following command should build the image for you:

    docker build --rm=true .

    If it fails, please take a look at the `README.md`, there may be some instructions how to build it. If you think you found an issue -- [let us know](https://github.com/jboss/dockerfiles/issues/new).

### Running

Every image is different. See instructions in `README.md` located next to the `Dockerfile` you want to build.

## Contribution

You don't see your project here? Just create a pull request -- we're happy to merge it. If you need help with creating the `Dockerfile` for tour project -- just open an issue and we'll see what we can do :) 

## License

All files listed in this repository are licensed under [MIT license](http://opensource.org/licenses/MIT).
