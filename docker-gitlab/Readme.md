### Gitlab 
## Status: working without runner

# Download and install "Docker Desktop for Windows"
#https://hub.docker.com/editions/community/docker-ce-desktop-windows

# create some working directory and place docker directory "gitlabci"

# in command line create volumes
docker volume list

docker volume create --name postgresqlvol --driver local
docker inspect postgresqlvol

#mkdir -p /data_docker/docker-gitlab/postgresqlvol
#docker volume create --name postgresqlvol -o type=none -o device=/docker_data/docker-gitlab/postgresqlvol -o o=bind
#docker inspect postgresqlvol

docker volume create --name redisvol --driver local
docker inspect redisvol

docker volume create --name gitlabvol --driver local
docker inspect gitlabvol


docker volume create --name gitlabvol --driver local
docker inspect gitlabvol

#run docker file composer file from IntelliJ Idea or manually
docker-compose up 

#Access at url:
http://localhost:10080/

# set password
