# references:
 https://hub.docker.com/r/winlu/docker-git-server/dockerfile

# pre-requisity
- docker
- cygwin - with openssl, openssh
- Dockerfile
- docker-compose.yaml
- remove any known hosts in case you rebuild image: rm /home/Bohus.Pollak/.ssh/known_hosts

# create volume for git-server
docker volume create --name git-data
docker volume inspect git-data


## start docker compose or from intellij docker-compose.yaml
#run the container compose file (if is named docker-compose.yaml)
docker-compose up
#run the same but with rebuilding the image
docker-compose up --build

# generate public key "ssh-keygen -t rsa" and /cygdrive/c/apps/putty/keys/
ssh-keygen -t rsa
cp /home/Bohus.Pollak/.ssh/id_rsa /cygdrive/c/apps/putty/keys/
cp /home/Bohus.Pollak/.ssh/id_rsa.pub /cygdrive/c/apps/putty/keys/

#add user jenkins and its public key
docker exec git-server_web_1 sh add_git_user.sh jenkins "`cat /cygdrive/c/apps/putty/keys/id_rsa.pub`"

# list and validate authorization key on host
docker exec git-server_web_1 cat  /git/data/users/jenkins/.ssh/authorized_keys
# should start with: ssh-rsa AAA...

# init repository
ssh -i /cygdrive/c/apps/putty/keys/id_rsa jenkins@localhost -p 1234 "init jenkins-dev.git"
#Log: Initialized empty Git repository in /git/data/users/jenkins/jenkins-dev.git/


#Add remote to your git repository:
git remote add docker_git_server ssh://localhost:1234/~/my_repo.git
#And push:
git push docker_git_server --set-upstream master


### Debuging
#removing password
docker exec git-server_web_1 passwd -d jenkins
# list config
docker exec git-server_web_1 cat /etc/ssh/sshd_config
#change PasswordAuthentication no
docker exec git-server_web_1 sed -i /etc/ssh/sshd_config -e 's/PasswordAuthentication no/PasswordAuthentication yes/g'
#change PasswordAuthentication yes
docker exec git-server_web_1 sed -i /etc/ssh/sshd_config -e 's/PasswordAuthentication yes/PasswordAuthentication no/g'
# list processes
docker exec git-server_web_1 ps
docker exec git-server_web_1 cat /git/data/users/git_passwd
docker exec git-server_web_1 cat add_git_user.sh

