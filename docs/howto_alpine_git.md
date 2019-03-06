### https://hub.docker.com/r/alpine/git

#create Dockerfile
 FROM alpine/git
# create 


docker volume create --name gitvol --driver local
docker inspect gitvol