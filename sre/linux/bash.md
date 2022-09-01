- 设置命令别名
```
alias lm='ls -la'
```
- 判断命令是否是bash内置的命令
```
type cd
```
- 变量操作
    - 查看变量
    ```
    echo $PATH
    ```
    - 设置变量（如果变量值中有空格可以用单引号或双引号，并且双引号内的值可以进行变量替换）
    ```
    JAVA_HOME=/usr/java/bin
    PATH="$PATH:$JAVA_HOME"
    version=$(uname -r)
    ```
    - 取消变量
    ```
    unset JAVA_HOME
    ```
    - 导出环境变量，使变量能在其他程序中可见
    ```
    export JAVA_HOME
    ```
    - 查看系统中已有的环境变量
    ```
    env
    ```
    - 查看除环境变量以外的变量
    ```
    set
    ```
- 查看系统信息
```
uname -a
```