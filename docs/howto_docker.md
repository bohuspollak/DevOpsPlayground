## Setup IntelliJ
    https://www.jetbrains.com/idea/download/
## Enable Docker Integration in IntelliJ
    Ctrl+Alt+S
    Search: Docker Integration
    Install
## Install Docker Comunity edition
    https://hub.docker.com/search/?type=edition&offering=community
    Enable Docker Settings -> General -> Expose Daemon on tcp://localhost:2375 without TLS
## Create Dockerfile in project

## Install Kinetics

## share drives
# in settings https://rominirani.com/docker-on-windows-mounting-host-directories-d96f3f056a2c
docker run --rm -v c:/Users:/data alpine ls /data


docker image ls
docker image prune
docker container ls



======
docker version
docker run hello-world
docker pull jenkins/jenkins:lts
docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts

docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --env JAVA_OPTS=-Xmx1048m -XX:MaxPermSize=512m -Dhudson.footerURL=http://hcl.com-Djava.util.logging.config.file=/var/jenkins_home/log.properties -v `pwd`/data:/var/jenkins_home jenkins/jenkins:lts
docker logs CONTAINER_ID




