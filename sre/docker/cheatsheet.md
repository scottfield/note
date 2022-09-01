###setup registry mirror
- centos7 setup
```
vi /etc/docker/daemon.json
 add config as following:
 {
  "registry-mirrors": ["http://ef017c13.m.daocloud.io"],
  "live-restore": true
 }
```
###国内镜像中心
- 网易镜像中心：https://c.163.com/hub#/m/home/ 
- daocloud镜像市场：https://hub.daocloud.io/
###get help doc of docker command
```
man docker command_name
```
###check docker version
```
$ docker --version
```
###build image
```
$ docker build -t docker.hyvesolutions.org/hyve/global-mrp-ui:latest .
```
###run docker image
```
$ docker run hello-world
```
###list docker images
```
docker images
```
###pull image from repository
```
docker pull image_name
```
###list docker containers
```
docker container ls
```

###use bash to explore docker container
```
docker container exec -it container_id bash 
```

###explore image content
```
docker run -it image_name bash
```
###copy file between host machine and docker container
```
docker cp container_id:/file/path .
```
###use docker compose to container
```
#should execute following command in the same directory of docker-compose.yml
docker-compose up -d
```
###use docker compose to check container log
```
docker-compose logs -f
```
###use docker compose to explore docker container
```
docker-compose exec -it container_name bash
```

