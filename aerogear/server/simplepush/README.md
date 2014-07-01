# AeroGear SimplePush Server Docker image
This project contains a Docker file for [AeroGear SimplePush Server](https://github.com/aerogear/aerogear-simplepush-server).

## Usage 

    docker run -p 7777:7777 -it jboss/aerogear-simplepush

Opening a web browser with the url [http://localhost:7777/simplepush](http://localhost:7777/simplepush) should display the SockJS welcome screen:

    Welcome to SockJS!

### Port forwarding for Mac OS X
You'll need to configure your VirtualBox to support port forwarding for port ```7777```:

```VBoxManage modifyvm "boot2docker-vm" --natpf1 "guestnginx,tcp,,7777,,7777"```

## Building locally

    docker build -t aerogear-simplepush .

And to run the locally built image:

    docker run -p 7777:7777 -it aerogear-simplepush

You can also run a shell instead of executing the SimplePush Server to investigate the container:
    
    docker run -p 7777:7777 -it aerogear-simplepush /bin/bash
