-  创建一个文件
```
touch test.txt
```
-  创建一个文件夹 (-p 创建多级文件夹)
```
mkdir test
```
-  清屏
```
clear
```
-  显示隐藏文件
```
ls -a
```
-  以列表的形式显示
```
ls -l
```
-  在配合-l以列表一起显示的时候-h可以以合适的单位显示文件的大小(-l -h -a 可以缩写成 -lha 顺序无所谓)
```
ls -l -h
```
-  可以格式清晰的显示man 后面所接的命令的文档，但是是一个新的页面，退出按Q键(man 2 open 中间的是后面命令文档对应的查询级别，1-8)
```
man ls
```
-  查看文件里面的内容
```
cat 文件名
```
-  查看历史命令 (!233 感叹号加上历史命令编号可以直接执行该命令)
```
history
```
-  删除命令 （-r 递归删除 文件或者文件夹）
```
rm 文件名
```
-  将原本ls 命令后显示在终端上的内容重定向到后面制定的文件里面，eg:test.txt
```
ls > test.txt
```
-  同上只是两个大于号是可以追加的（如果文件不存在，那么重建，如果有内容则是追加。但是一个大于号就是先删除，再写上内容）。
```
ls >> test.txt
```
-  more命令和cat命令是类似的都是查看文件的内容不同之处在于cat是一次性的查看所有文件内容，但是more却是部分显示(通过d、f)来分页，所以在查看大文件的时候使用more比较好。
```
more test.text
```
-  将上面的6、11、13等命令集成使用，这样可以避免创建重定向储存的临时文件。(竖线 可以理解成管道，并不是所有的命令都有管道)。
```
ls -alh | more
```
-  分号的作用就是将两个命令同时执行（不推荐）
```
； eg: ls ; ls -alh
```
-  回到当前用户的目录
```
cd ~
```
-  回到上一次的目录
```
cd -
```
-  （1） 修改文件名，前面的是老文件名，后面是新文件名（2）剪切并粘贴 文件到某个位置
```
mv today.txt today001.txt
```
- 创建一个文件的软链接，soft_link.txt 被称之为 today.txt的软链接(相当于快捷方式)
```
ln -s today.txt soft_link.txt 
```
- 创建一个文件的硬链接，hard_link.txt称之为硬链接文件（理解为同一个文件多了一个文件名 ）
```
ln today.txt hard_link.txt
```
- 文件搜索
```
grep -n/-v
```
- copy是复制一个文件并且粘贴到一个新的路径，如果复制一个文件夹 提示不能操作，可在后面加上-r。
```
copy （-r） 文件 新的路径
```
- find 特定目录下查找符合条件的文件（1）find ./ -name test.txt 按照名字查找当前目录下名字为test.txt的文件 （2）find /jackyang -size 2M 查找jackyang目录下登录2M大小的文件（-size +2M 大于. -size -2M小于2M的） 如果出现的文件显示没有权限可以在find 前面加上sudo find
-  将当前目录中以.py结尾的文件打包成 tarTest.tar 打包文件
```
tar -cvf tarTest.tar *.py
```
- 将tarTest.tatarTest.ta文件解包
```
tar -xvf tarTest.tar
```
- 压缩文件需要在参数上加上z 和压缩文件名后面加上.gz（tar -jcvf tarTest.tar.bz2 *.py ）
```
tar -zcvf tarTest.py.gz *.py 
```
- tar -zxvf tarTest.py.gz 解压文件. 对于的第二种解压 (tar -jxvf tarTest.tar.bz2) 后面加上 -C jackyang/xxx解压到指定目录
- cal 日历 cal -y 2017 显示2017年的日历。直接cal 显示的是当前月份的日历
- date 显示当前时间 ， date “+%Y 年 %m月 %d日”. ===>2017 年 12月 12日
- ps -aux / top /htop 都是查看电脑的使用情况（注意Mac终端命令）
- kill 进程号 （kill -9 进程号）加了-9强制杀死
- reboot 重启。 shutdown -h 2000 2000秒后关机
- df 显示硬盘的情况。 du 显示当前路径的使用情况
- 查看ip 和设置ip
```
ifconfig
ip addr
```
- ping 加上IP 查看网络是否通畅
- sudo -s 切换超级管理员
- 修改文件读写权限
  - (1.字母法)chmod u(g\o)=rwx aa.py 修改aa.py 这个文件的权限 产生 u\g\o 分别对应着拥有者、同组用户、其他用户
  - （2.数字法） r—>4 w—>2 x—>1 chmod 137 aa.py 表示拥有者可执行，同组者可写可执行、其他用户可读可写可执行。