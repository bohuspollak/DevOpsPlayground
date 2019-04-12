###Gitlab runner
##Status working but without runner

# list images
docker -H tcp://0.0.0.0:2375 images

# create volume for docker-compose
docker volume list
docker volume create --name gitlabrunnervol --driver local
docker inspect gitlabrunnervol

docker volume create --name dockersock --driver local
docker inspect dockersock

# configure toml file
#https://docs.gitlab.com/runner/configuration/advanced-configuration.html
#/etc/gitlab-runner/config.toml

# register runner:
# get token and ip from page: http://10.0.75.1:10080/admin/runners

# run from terminal
docker run --rm -t -i -v gitlabrunnervol:/etc/gitlab-runner gitlab/gitlab-runner register --registration-token "ujCSv_6KCz9_x6pc1DDw" --url "http://10.0.75.1:10080/" --name gitlab-runner --non-interactive --executor "docker" --docker-image alpine:3   --run-untagged="true" --locked="false"

docker run --rm -t -i -v gitlabrunnervol:/etc/gitlab-runner gitlab/gitlab-runner register --registration-token "gDMDqxCxZcBnsXVyGtsn" --url "http://172.18.0.1:10080/" --name gitlab-runner --non-interactive --executor "docker" --docker-image alpine:3   --run-untagged="true" --locked="false"


# on linux
docker network ls
docker network inspect docker-gitlab_default
docker run --rm -t -i -v gitlabrunnervol:/etc/gitlab-runner gitlab/gitlab-runner register --registration-token "gDMDqxCxZcBnsXVyGtsn" --url "http://172.18.0.1:10080/" --name gitlab-runner --non-interactive --executor "docker" --docker-image alpine:3   --run-untagged="true" --locked="false"


docker run --rm -t -i -v gitlabrunnervol:/etc/gitlab-runner gitlab/gitlab-runner register --registration-token "gDMDqxCxZcBnsXVyGtsn" --url "http://10.222.222.170:10080/" --name gitlab-runner --non-interactive --executor "docker" --docker-image alpine:3   --run-untagged="true" --locked="false"


# error on linux:
ERROR: Registering runner... failed                 runner=gDMDqxCx status=couldn't execute POST against http://172.18.0.1:10080/api/v4/runners: Post http://172.18.0.1:10080/api/v4/runners: dial tcp 172.18.0.1:10080: getsockopt: no route to host
PANIC: Failed to register this runner. Perhaps you are having network problems
#solved with stopping firewall
systemctl stop firewalld

# errors
ERROR: Registering runner... failed                 runner=ujCSv_6K status=couldn't execute POST against http://localhost:10080/api/v4/runne
rs: Post http://localhost:10080/api/v4/runners: dial tcp 127.0.0.1:10080: getsockopt: connection refused
PANIC: Failed to register this runner. Perhaps you are having network problems
#solution used different ip internal in docker
docker run --rm -t -i -v gitlabrunnervol:/etc/gitlab-runner gitlab/gitlab-runner register --registration-token "ujCSv_6KCz9_x6pc1DDw" --url "http://10.0.75.1:10080/" --name gitlab-runner --non-interactive --executor "docker" --docker-image alpine:3   --run-untagged="true" --locked="false"

# error socke
WARNING: Preparation failed: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running? (executor_docker.go:1172:0s)  job=1 project=1 runner=GsXUHrW2
Will be retried in 3s ...                           job=1 project=1 runner=GsXUHrW2
ERROR: Job failed (system failure): Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running? (executor_docker.go:1172:0s)  duration=9.0065598s job=1 project=1 runner=GsXUHrW2

# error 
Using Docker executor with image alpine:latest ...
ERROR: Preparation failed: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running? (executor_docker.go:1172:0s)

variables:
  DOCKER_HOST: tcp://docker:2375/
  DOCKER_DRIVER: overlay2

solution:
make docker sock shareable:
/var/run/docker.sock:/var/run/docker.sock

#https://forums.docker.com/t/cannot-connect-to-the-docker-daemon-is-the-docker-daemon-running-on-this-host/8925/3
sudo nohup docker daemon -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock &

#####solution: - /var/run/docker.sock:/var/run/docker.sock


Inside file /lib/systemd/system/docker.service change:
ExecStart=/usr/bin/dockerd fd://
with
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375

Inside file /etc/init.d/docker change:
DOCKER_OPTS=
with
DOCKER_OPTS="-H tcp://0.0.0.0:2375"

systemctl daemon-reload
systemctl start docker



#error web_1  | Checking for jobs... received                       job=8 repo_url=http://localhost:10080/root/lottomania.games.git runner=DyU_SP-8
       web_1  | WARNING: Job failed: exit code 1                    duration=37.951006104s job=8 project=1 runner=DyU_SP-8

fatal: unable to access 'http://gitlab-ci-token:xxxxxxxxxxxxxxxxxxxx@localhost:10080/root/lottomania.games.git/': Failed to connect to localhost port 10080: Connection refused

https://gitlab.com/gitlab-org/gitlab-development-kit/blob/master/doc/howto/runner.md
gitlab/config/gitlab.yml

docker ps
docker exec -it bf076f607618 /bin/bash
