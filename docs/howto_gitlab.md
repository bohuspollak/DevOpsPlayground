#https://docs.gitlab.com/omnibus/docker/README.html

#setup persisent volume
#https://docs.docker.com/compose/compose-file/#volumes-for-services-swarms-and-stack-files

docker volume create --name gitlabvol --driver local
docker inspect gitlabvol

#run docker file: Dockerfile
FROM gitlab/gitlab-ce:rc

#with yaml compose
docker-compose.yaml

##todo issue with runsv start
docker exec -it 67d2de8b26b6 update-permissions
docker restart 67d2de8b26b6


#read the logs
docker logs -f a3cbc184d45f

sudo docker exec -it gitlab /bin/bash



docker pull store/gitlab/gitlab-ce:10.2.4-ce.0


sudo docker run --detach \
	--hostname localhost \
	--publish 443:443 --publish 80:80 --publish 22:22 \
	--name gitlab \
	--restart always \
	--volume /srv/gitlab/config:/etc/gitlab \
	--volume /srv/gitlab/logs:/var/log/gitlab \
	--volume /srv/gitlab/data:/var/opt/gitlab \
	gitlab/gitlab-ce:latest

