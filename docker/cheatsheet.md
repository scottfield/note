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