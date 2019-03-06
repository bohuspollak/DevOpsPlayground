### This document describes how to get Jenkins running on local docker machine

## Create volume for jenkins home
docker volume create --name jenkinsvol --driver local
docker inspect jenkinsvol

## Run docker-compose.yaml
This will build image and configure it. Then it will run it and expose ports and mount volume

#run the jenkins compose file if is named docker-compose.yaml
docker-compose up
#run the same but with rebuilging the image
docker-compose --build up

## List docker image running
 docker ps
## Access jenkins over browser
    http://localhost:8080/login?from=%2F
## Unlock Jenkins using generated password
  523b3c88121346fdb5dd71cc1da4dc9c


###References
https://docs.docker.com/compose/overview/
