- 使用${VARIABLE_NAME}方式来明确指定所引用的变量
- 使用${myname:-"hello world"}获取默认值
- 使用${myname:=John Doe}来对变量设置默认值
- 将命令放入后台运行
```
ls &
```
- 字符串比较
```
String equal	                if [ "$foo" = "bar" ]
String not equal                if [ "$foo" != "bar" ]
-z	String is zero length	    if [ -z "$foo" ]
-n	String is not zero length	if [ -n "$foo" ]
```
- 整数比较
```
-eq	Numeric Equality	         if [ "$foo" -eq "9" ]
-ne	Numeric Inquality	         if [ "$foo" -ne "9" ]
-lt	Less Than	                 if [ "$foo" -lt "9" ]
-le	Less Than or Equal	         if [ "$foo" -le "9" ]
-gt	Greater Than	             if [ "$foo" -gt "9" ]
-ge	Greater Than or Equal	     if [ "$foo" -ge "9" ]
```
- 文件和目录比较
```
-nt	Newer Than	            if [ "$file1" -nt "$file2" ]
-d	Is a Directory	        if [ -d /bin ]
-f	Is a File	            if [ -f /bin/ls ]
-r	Is a readable file	    if [ -r /bin/ls ]
-w	Is a writable file	    if [ -w /bin/ls ]
-x	Is an executable file	if [ -x /bin/ls ]
```
- 逻辑运算符
```
&& 逻辑与
|| 逻辑或
! 逻辑非
```
- for循环
```
for i in 1 2 3 4 5
do
  echo "Looping ... number $i"
done
```
- while循环,在while循环的条件中可以使用冒号来实现无线循环
```
INPUT_STRING=hello
while [ "$INPUT_STRING" != "bye" ]
do
  echo "Please type something in (bye to quit)"
  read INPUT_STRING
  echo "You typed: $INPUT_STRING"
done
```
```
#使用while循环读取文件进行逐行的处理
while f=`line`
do
  .. process f ..
done < myfile
或
while read f
do
   .. process f ..
done < myfile
```
- 使用if判断
```
if  [ something ]; then
 echo "Something"
 elif [ something_else ]; then
   echo "Something else"
 else
   echo "None of the above"
fi
```
- 使用switch-case判断
```
#!/bin/sh
read INPUT_STRING
case $INPUT_STRING in
hello)
    echo "Hello yourself!"
    ;;
bye)
    echo "See you again!"
    break
    ;;
*)
    echo "Sorry, I don't understand"
    ;;
esac
```
- function中常用的变量含义
```
$0 当前程序的名称
$1 .. $9 函数的第1..9个参数
$@ 函数的所有参数
$* 与$@类似,只是会忽略掉参数中的空白字符(推荐使用$@)
$# 函数参数的个数
$? 最后一个命令执行后的退出码的值
$$ 当前运行shell的pid
$! 最后一个后台运行进程的pid
IFS 字段分割符号,系统默认为SPACE TAB NEWLINE
```
