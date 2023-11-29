
# Tech World With Nana (Docker)

## Containers are portable pack dependencies and configurations

### Portable artifact easily shared and moved around

### Make development and deployment more effiencent

## Where do containers live
### container repos
### Private repos
### Public repos (docker hub)

## How cantainer improves development process?
### Before?
### install most of the service on the each os
### Multiple steps where something might go wrong (due to the no. of steps involved)
## After
### Own isolated environment
### packed with all needed configurations
### one command to install the app
### run the same app with 2 different versions

## How containers improves deployment process
## Before
### development team gives artifacts and textual guide of deployment to operations team to deployment
### rasies dependency version conflicts and misunderstandings
## After
### Developers and operations working in one team to package the application in a container
### No environmental configurations need on the server (except docker runtime)

## other container technologies?
### cotainerd, cri-o

## What is a Container?
### Layers of images
### Mostly linux base image, because small in size (base image)
### application image on top (e.g. nginx)


## public repos does not require login or authentication

```
docker run postgres:9.6
```

#### it tries first to fetch the image locally then goes to dockerhub

## adavantage of spliting the application image to layers allows for versioning (e.g. changing only the changed layers)

```
docker ps
```

#### allows you to see running containers

## Image vs container
### Image
#### image is the actual package (containing the app, dependencies, start script)
### container
#### is when i pull the image and start it (conatiner environmentis started)

```
docker run postgres:10.10
```

#### you can run multiple versions of the same image on the same machine

## Docker vs VMs

## Operating systems have 2 layers
### Applications (layer 2)
### OS Kernel (layer 1)
### Hardware

## Docker
### Applications (layer 1)
### OS Kernel
### Hardware

## Size of docker image is much smaller
## Docker containers start and run much faster
## VM of any OS can run on any host
### you can't run linux images on windows OS (windows 10 and before)
### a workaround is using docker toolbox which abstracts the kernel to make the host run different docker images

## docker architecture and its componenets

### when you install docker you install docker engine which has 3 parts:
#### Docker Server
##### Pulling Images
##### Managing Containers
#### Docker API
##### Interacting with docker server
#### Docker CLI
##### Command line interface to execute docker commands

## Docker Server has 3 components:
### Container runtime
#### pulling images
#### managing container lifecycle
### Volumes
#### presisting data
### Network
#### configuring netwotk for conatiner communication
### Build images
#### build own docker images

## Docker is very powerful (many functionality in 1 application)

### Docker Main Commands

#### Container is the running environment for the image (filesystem, env vars, application image, port binding)

### Container port vs Host port
##### Multiple containers can run on the same hosts
##### You laptop only has certian ports available
##### conflict when same port on same machine
##### you can bind host ports to container ports (ex. 3001 on machine to 3000 on container)

## debuging docker containers
### basic docker commands

```
docker pull
docker run -d -p6000:6379 --name ${container_name} ${image}
docker start
docker stop
docker ps -a
docker images
docker logs ${container_id}
docker exec -it ${container_id} /bin/bash or /bin/sh
docker rmi ${image_id}
docker rm ${containe_id}
```

## Workflow with docker

### Developing the application (Mongo and JS)
### Committing it in git
### Continous integration with Jenking (building JS app & create docker image)
### push to the private Repo
### deployment to your server (server pulls the image from the private repo and the public repo

## Demo Project

### Develop simple node app with mongodb
### Deploy MongoExpress to see UI of mongodb

### Docker Netwrok

#### docker containers can talk to each other using just the container name, host run apps will have to talk through ports

```
docker network ls
docker network create ${network name}
```

## Docker compose

### Mapping docker commands to a yaml file


## What is a docker file?
### A blue print for building a docker image

```
FROM node

ENV MONGO_DB_USERNAME= admin \
        MONGO_DB_PWD=password

RUN mkdir -p /home/app

COPY . /home/app

CMD ["node","server.js"]
```

## Docker Volumes

Data is lost when container is restarted

Data should be replicated on the host machine filesystem

### Host Volume
```
docker run -v /home/mount/data:/var/lib/mysql/data

```

### Anonymous Volume

```
docker run -v /var/lib/mysql/data
```

### Named Volumes

```
docker run -v name:/var/lib/mysql/data
```

## Docker Volume

### Where are docker volumes located on machine
#### Windows: C:\ProgramData\docker\volumes
#### Linux: /var/lib/docker/volumes
