[View on GitHub](https://github.com/jordancrawfordnz/rpi-pydio-docker)

[View on Docker Hub](https://hub.docker.com/r/jordancrawford/rpi-pydio-docker/)

RPi Pydio Docker
=============
This repository allows you to run Pydio on your Raspberry Pi with Docker. This DOESN'T includes a built in MySQL server.

This has been adapted from the x86 version at [kdelfour/pydio-docker](https://github.com/kdelfour/pydio-docker).

# About Pydio

Pydio is like Google Drive for your personal cloud. See the Pydio website at: https://pydio.com/

### [Using this container as part of a Raspberry Pi home server](https://jordancrawford.kiwi/rpi-home-server/)

# Installation
Download from Docker Hub: ``docker pull jordancrawford/rpi-pydio-docker``

(alternatively, you can build an image from Dockerfile: ``docker build -t jordancrawford/rpi-pydio-docker``)

## Usage

    docker run -it -d -p 80:80 -p 443:443 jordancrawford/rpi-pydio-docker
    
You can add a shared directory as a volume directory with the argument *-v /your-path/files/:/pydio-data/files/ -v /your-path/personal/:/pydio-data/personal/* like this :

    docker run -it -d -p 80:80 -p 443:443 -v /your-path/files/:/pydio-data/files/ -v /your-path/personal/:/pydio-data/personal/ jordancrawford/rpi-pydio-docker

A mysql server with a database is ready, you can use it with this parameters : 

  - url : localhost
  - database name : pydio
  - user name : pydio
  - user password : pydio
    
## Build and run with custom config directory

Get the latest version from Github.

    git clone https://github.com/jordancrawford/rpi-pydio-docker
    cd rpi-pydio-docker/

Build it

    sudo docker build --force-rm=true --tag="jordancrawford/rpi-pydio-docker:latest" .
    
And run

    sudo docker run -d -p 80:80 -p 443:443 -v /your-path/files/:/pydio-data/files/ -v /your-path/personal/:/pydio-data/personal/ jordancrawford/rpi-pydio-docker:latest

## Using host folders

Pydio is great to use with host folders. Add these as a Docker volume like:

    sudo docker run -d -p 80:80 -p 443:443 -v /harddrive:/harddrive jordancrawford/rpi-pydio-docker:latest

Then create a file system workspace at ``/harddrive``.

### File ownership

Pydio runs as the ``www-data`` user (with uid of 1000). In an OS like Hypriot OS, this matches up with the ``pi`` user. You must ensure your host folder is accessable to the user with the uid 1000.

## After the installation

To make sure that share feature will work, go to Main Pydio Option and add  :

  * Server URL: https//your_server_name
  * Download folder: /var/www/pydio-core/data/public
  * Server download URL: https//your_server_name/data/public

Enjoy!
