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