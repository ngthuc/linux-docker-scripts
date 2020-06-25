# Linux and Docker Scripts

## Package Used

```shell
sudo apt-get install -y git curl wget make apt-transport-https ca-certificates curl software-properties-common
```

## Linux
* Install docker private certificate and login to private docker registry

```shell
sudo mkdir /usr/local/share/ca-certificates/docker-dev-cert

cd /usr/local/share/ca-certificates/docker-dev-cert

nano <certificate-name>.crt

update-ca-certificates

systemctl daemon-reload

service docker restart

docker login <registry.example.com>
```

* Install docker

```shell
sudo apt-get install -y git curl wget

curl -fsSL https://get.docker.com -o get-docker.sh

sudo sh get-docker.sh

sudo usermod -aG docker $USER

docker -v
```

## Windows SubSystem for Linux - Ubuntu 18.04
* Setup WSL to use docker in Windows 10

```shell
sudo apt-get update

sudo apt-get install -y git curl wget make apt-transport-https ca-certificates curl software-properties-common

export PATH="$HOME/bin:$HOME/.local/bin:$PATH"

export PATH="$PATH:/mnt/c/Program\ Files/Docker/Docker/resources/bin"

alias docker=docker.exe

alias docker-compose=docker-compose.exe

sudo groupadd docker

sudo usermod -aG docker $USER

newgrp docker

sudo gpasswd -a $USER docker
```

## Docker
* Push image to docker registry

```shell
docker push <image-name>:<tag>
```

* Run background

```shell
docker run -d -it <image-name>:<tag>
```

* Run and build arguments

```shell
docker build -t <image-name>:<tag> --build-arg <argument-key>=<argument-value> .

usage in Dockerfile: 
ARG <argument-key>
# or with a default:
#ARG <argument-key>=default_value

RUN echo "Oh dang look at that $<argument-key>"
# or with ${<argument-key>}
```

* Executive in container

```shell
docker exec -it <container-ID> bash
```

* Remove images intelligent (^^^)

```shell
docker rmi $(docker images | grep <anything-you-want-search> | awk '{print $3}')
```

* Remove container intelligent

```shell
docker rm -f $(docker ps -a | grep <anything-you-want-search> | awk '{print $1}')
```
