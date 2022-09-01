####端口映射 
```
netsh interface portproxy add v4tov4 listenport=80 connectaddress=127.0.0.1 connectport=1017
```

### 账号密码管理
Windows+S==> Credential Manager==>update the account and password
###update file timestamp by powershell
```
$(Get-Item ).creationtime=$(Get-Date "mm/dd/yyyy hh:mm am/pm")
$(Get-Item ).lastaccesstime=$(Get-Date "mm/dd/yyyy hh:mm am/pm")
$(Get-Item ).lastwritetime=$(Get-Date "mm/dd/yyyy hh:mm am/pm")
e.g.
$(Get-Item aaa.csv).lastwritetime=$(Get-Date)
```
###automatically startup a program  when system booting
```
all you need to do is that open startup folder and add the program's shortcut to this folder
for current login user:
shell:startup
for all users
shell:common startup
```
###clear DNS cache
```
ipconfig /flushdns
```