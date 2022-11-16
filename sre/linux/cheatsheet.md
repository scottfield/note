-  判断命令是否是bash内置命令
    ```
    type cd
    ```
-  查看bash内置命令的帮助信息
    ```
    help cd
    ```
-  查看系统版本信息
    ```
    uname -a
    ```
- 查看内核版本
    ```
    cat /proc/version
   ```   
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
- 文件夹查看
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
-  查看命令的帮助文档,退出按q键
    ```
    man ls
    man 2 open //中间的是后面命令文档对应的查询级别，1-8
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
- 部分显示文档内容(通过d、f)来分页，适合查看大文件
    ```
    more test.text
    ```
-  使用管道来查看文件列表内容
    ```
    ls -alh | more
    ```
-  分号的作用就是将两个命令同时执行（不推荐）
    ```
    ls ; ls -alh
    ```
- 当前工作目录切换
    -  回到当前用户的目录
        ```
        cd ~
        ```
    -  回到上一次的目录
        ```
        cd -
       ```
    -  切换到指定目录
       ```
       cd /path/to/dir
      ```
- 修改文件名
    ```
    mv today.txt today001.txt //前面的是老文件名，后面是新文件名
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
- 复制一个文件并且粘贴到一个新的路径，如果复制一个文件夹 提示不能操作，可在后面加上-r。
    ```
    copy （-r） 文件 新的路径
    ```
- 特定目录下查找符合条件的文件  如果出现的文件显示没有权限可以在find 前面加上sudo find
    - 按照名字查找
        ```
        find ./ -name test.txt //查看当前目录及其子目录下文件名为test.txt的文件
        find ./ -name test* //查看当前目录及其子目录下已test开头的文件
        ``` 
    - 按文件大小查找
        ```
        find /home/jackie -size 2M //文件大小等于2M 
        find /home/jackie -size +2M //文件大小大于2M
        find /home/jackie -size -2M //文件大小小于2M
        ```
- 文件解压缩
    - tar包解压缩
        -  将当前目录中以.py结尾的文件打包成 tarTest.tar 打包文件
            ```
            tar -cvf tarTest.tar *.py
            ```
        - 解压文件,后面加上 -C src/bin 解压到指定目录
            ```
            tar -xvf tarTest.tar
            ```
    - gz包解压缩
        - 压缩文件需要在参数上加上z 和压缩文件名后面加上.gz
            ```
            tar -zcvf tarTest.py.gz *.py 
            ```
        - 解压文件,后面加上 -C src/bin 解压到指定目录
            ```
            tar -zxvf tarTest.py.gz 
            ```
    - bz2包解压缩
        - 压缩文件
            ```
            tar -jcvf tarTest.tar.bz2 *.py
            ```
        - 解压文件,后面加上 -C src/bin 解压到指定目录
            ```
            tar -jxvf tarTest.tar.bz2
            ```
- 查看日历
    ```
    cal //当前月份日历
    cal -y //当年日历
    ```
- 查看时间
    ```
   date //显示当前时间
   date "+%Y 年 %m月 %d日" //格式化显示日期
    ```
- 查看电脑的使用情况
    ```
    top
    ```
- 查看进程
    ```
    ps -aux
    ```
- 强制结束进程
    ```
    kill -9 processId
    ```
- 重启
    ```
    reboot
    ```
- 2000秒后关机
    ```
    shutdown -h 2000
    ```
- 查看硬盘使用情况
    ```
    df
    ```
- 显示当前路径下各个文件的硬盘使用情况
    ```
    du -sh ./*
    ```
- 查看ip 和设置ip
    ```
    ifconfig
    ip addr
    ```
- 查看网络是否通畅
    ```
    ping baidu.com
    ```
- 切换超级管理员
    ```
    sudo -s
    ```
- 修改文件读写权限
    ```
    r(读)—>4 w(写)—>2 x(执行)—>1
    chmod 755 app.py
    ```
- 复制远程服务器文件到本地
  ```
  rsync -av --rsh=ssh app@10.37.17.57:/secrets .
  or
  scp username@remote_host:/remote_dir/* ./local_dir
  ```
  
- tcpdump抓包并保存为pcap文件
```
#抓取网卡eth0上的2000条tcp协议的packets并保存为文件tcpanalyze.pcap
tcpdump -i eth0 -c 2000 -w tcpanalyze.pcap tcp
```
