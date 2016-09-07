# Syncthing
Syncthing is an Open Source distributed file sharing solution. This repository contains all the files needed to build and run Syntching inside a Docker container.

[![](https://images.microbadger.com/badges/image/ppizzo/syncthing.svg)](https://microbadger.com/images/ppizzo/syncthing "Get your own image badge on microbadger.com")

## Build
Pre-built images are available on the DockerHub, but if you want to build it by yourself, just grab the Dockerfile from the repository, modify to suit your needs and build the image using the standard ```docker build``` command.

The provided Dockerfile creates a regular user with UID 1000. This UID should be the same of the user on the Docker engine who is the owner of the files to be synced. Please change it to adapt to your environment.

## Run
The source repository contains a ```docker-compose.yml``` file you can use to run the container. Please modify it accordingly to your requirements.

You should mount at least two volumes: one to hold the configuration, one to hold data. The two volumes are already declared in the  ```docker-compose.yml```, please modify them to suit your environment.

Start the container with ```docker-compose up -d``` command. At the first run, the application creates the required certificates and configuration files in the declared configuration directory. In order to access the web interface, you must open the ```config.xml``` file with a text editor and modify the content of the tag ```<address>``` included in the tag ```<gui>``` by changing the default ```127.0.0.1``` address with ```0.0.0.0``` or the internal IP of the container (if you want to access the web interface from localhost only). You must then restart the container in order for the changes to make effect.

The web interface will be available at the following URL: http://localhost:8384/.

We recommend to switch to HTTPS protocol and set up an username and password for the web interface.

You should also delete the default folder because it maps to a directory inside the container and create as many sync folders you want: each folder should be a subdirectory of the mounted data volume.

The provided ```docker-compose.yml``` file requires docker-compose version 1.6 or newer.

You can find pre-built images for this repository on the DockerHub at the following URL: https://hub.docker.com/r/ppizzo/syncthing/.

## References
https://syncthing.net/
