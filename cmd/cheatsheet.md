##window 常用命令
###查看服务
```
net start
```
###删除服务
```
sc delete 服务名称
```
###查看网络端口
```
netstat -aon | find /i "8080"
```
###根据进程pid终止进程
```
taskkill /f /pid 15140
```
###开启远程桌面
```
mstsc
```
###更新可执行文件的最后修改时间
```
切换到可执行文件的所在的文件夹执行如下命令:
copy /b fileName+
```