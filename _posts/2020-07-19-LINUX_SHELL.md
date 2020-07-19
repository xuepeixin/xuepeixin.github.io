---
title:     Linux Shell
date:       2020-07-19
author:     XPX
catalog: true
tags:
    - 程序设计
---

## 命令行的用法及bash脚本

### 终端显示输出

#### echo

##### 双引号和单引号

默认情况下，echo在每次调用后会添加一个换行符：echo命令就可以将其中的文本在终端中打印出来。类似地，不使用双引号也可以得到同样的输出结果，实现相同效果的另一种方式是使用单引号：

*双引号允许shell解释字符串中出现的特殊字符。单引号不会对其做任何解释。*

```
$ echo "Welcome to Bash"
$ echo Welcome to Bash
$ echo 'text in quotes'
```

##### 在echo中转义换行符

echo会在输出文本的尾部追加一个换行符。可以使用选项-n来禁止这种行为。

```bash
echo -n "hello "; echo "world" 
echo "hello "; echo "world"
```

结果为：
```
hello world
hello
world
```
##### 包含转义序列的字符串 echo -e

```bash
echo -e "1\t2\t3" # 1  2   3
echo  "1\t2\t3" #1\t2\t3
```

##### 打印彩色输出

```
echo -e "\e[1;31m This is red text \e[0m"
```

对于彩色背景，经常使用的颜色码是：重置=0，黑色=40，红色=41，绿色=42，黄色=43，
蓝色=44，洋红=45，青色=46，白色=47。

#### printf

``` bash
printf "%-5s %-10s %-4s\n" No Name Mark
printf "%-5s %-10s %-4.2f\n" 1 Sarath 80.3456
printf "%-5s %-10s %-4.2f\n" 2 James 90.9989
printf "%-5s %-10s %-4.2f\n" 3 Jeff 77.564
```

结果为：

```
No Name Mark
1 Sarath 80.35
2 James 91.00
3 Jeff 77.56
```

### 使用变量与环境变量

#### 查看环境变量 

可以使用`env`或`printenv`命令查看当前shell中所定义的全部环境变量：

要查看其他进程的环境变量，可以使用如下命令：
```bash
cat /proc/$PID/environ
```
其中，PID是相关进程的进程ID（PID是一个整数）。假设有一个叫作gedit的应用程序正在运行。我们可以使用pgrep命令获得gedit的进程ID：
```bash
$ pgrep gedit
```

#### 变量的赋值和输出

可以使用等号操作符为变量赋值：
```bash
varName=value
```
varName是变量名，value是赋给变量的值。如果value不包含任何空白字符（例如空格，那么就不需要将其放入引号中，否则必须使用单引号或双引号。

我们可以在printf、echo或其他命令的双引号中引用变量值：
```bash
#!/bin/bash
#文件名:variables.sh
fruit=apple
count=5
echo "We have $count ${fruit}(s)"
```
输出如下：
```
We have 5 apple(s)
```

#### export命令设置环境变量

```bash
$ PATH="$PATH:/home/user/bin"
$ export PATH
$ echo $PATH
/home/slynux/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/home/user/bin
```
### 使用shell进行数学运算

- 可以像为变量分配字符串值那样为其分配数值
```bash
#!/bin/bash
no1=4;
no2=5;
```
- let命令可以直接执行基本的算术操作。当使用let时，变量名之前不需要再添加$，
```bash
let result=no1+no2
echo $result
```
- 操作符[]的使用方法和let命令一样：
```bash
result=$[ no1 + no2 ]
result=$[ $no1 + 5 ]
```
- expr同样可以用于基本算术操作
```bash
result=`expr 3 + 4`
result=$(expr $no1 + 5)
```
- bc是一个用于数学运算的高级实用工具，这个精密的计算器包含了大量的选项。
```bash
echo "4 * 0.56" | bc
2.24
no=54;
result=`echo "$no * 1.5" | bc`
echo $result
81.0
```

### 文件描述符与重定向

文件描述符是与某个打开的文件或数据流相关联的整数。文件描述符0、1以及2是系统预留的。
1. 0 —— stdin （标准输入）。
2. 1 —— stdout（标准输出）。
3. 2 —— stderr（标准错误）。

- 使用大于号将文本保存到文件中：
```bash
$ echo "This is a sample text 1" > temp.txt
```

- 使用双大于号将文本追加到文件中：
```bash
$ echo "This is sample text 2" >> temp.txt
```

- 使用cat查看文件内容：
```bash 
$ cat temp.txt
This is sample text 1
This is sample text 2
```

- 使用2>（数字2以及大于号）将stderr重定向:
```bash
ls + 2> out.txt #没有问题
```

- 将stderr和stdout分别重定向到不同的文件中：
```bash
$ cmd 2>stderr.txt 1>stdout.txt
```

- 将stderr转换成stdout，使得stderr和stdout都被重定向到同
一个文件中：
```bash
$ cmd alloutput.txt 2>&1 
$ cmd &> output.txt 
```

- 如果不想看到或保存错误信息，可以将stderr的输出重定向到`dev/null`

### 数组与关联数组

- 在单行中使用数值列表来定义一个数组：
```bash
array_var=(test1 test2 test3 test4)
array_var[0]="test1"
```
- 打印出特定索引的数组元素内容：
```bash
echo ${array_var[0]}
```
- 以列表形式打印出数组中的所有值：
```bash
$ echo ${array_var[*]}
test1 test2 test3 test4 test5 test6
$ echo ${array_var[@]}
test1 test2 test3 test4 test5 test6
```
- 打印数组长度（即数组中元素的个数）：
```bash
$ echo ${#array_var[*]} # 6
```

### 别名

- 创建别名
```bash
$ alias install='sudo apt-get install'
```
- 放入~/.bashrc中
```bash
$ echo 'alias cmd="command seq"' >> ~/.bashrc
```
- 如果需要删除别名，只需将其对应的定义（如果有的话）从~/.bashrc中删除，或者使用unalias命令。也可以使用alias example=，这会取消别名example。
- 对别名进行转义:字符\可以转义命令，从而执行原本的命令。在不可信环境下执行特权命令时，在命令前加上\来忽略可能存在的别名总是一种良好的安全实践。**这是因为攻击者可能已经将一些别有用心的命令利用别名伪装成了特权命令，借此来盗取用户输入的重要信息。**

### 采集终端信息

- 输入密码时，脚本不应该显示输入内容。在下面的例子中，我们将看到如何使用stty来
实现这一需求：
```bash
#!/bin/sh
#Filename: password.sh
echo -e "Enter password: "
# 在读取密码前禁止回显
stty -echo
read password
# 重新允许回显
stty echo
echo
echo Password read.
```

### 获取并设置日期及延时

```bash
$ date
Thu May 20 23:09:04 IST 2010
$ date +%s
1290047248
$ date "+%d %B %Y"
20 May 2010
```

date命令所支持的格式选项：

|日期内容|格式|
|-|-|
|工作日（weekday）|%a（例如：Sat）|
|工作日（weekday） |%A(例如：Saturday)|
|月| %b（例如：Nov）|
|月|%B（例如：November）|
|日| %d（例如：31）|
|特定格式日期（mm/dd/yy）| %D（例如：10/18/10）|
|年| %y（例如：10）|
|年|%Y（例如：2010）|
|小时| %I或%H（例如：08）|
|分钟| %M（例如：33）|
|秒| %S（例如：10）|
|纳秒| %N（例如：695208515）|
|Unix纪元时|（以秒为单位） %s（例如：1290049486）|

### 调试脚本

- 使用选项-x，启用shell脚本的跟踪调试功能：
```bash
$ bash -x script.sh
```

## 常用Linux命令

## 文件操作

## 文本操作

## Shell进行Web交互

## 仓库管理

## Linux备份工具

## 网络配置

## 系统状态查看

## 任务管理

## 查找故障、跟踪库和系统调用过程

## 提升系统性能

## 使用容器、虚拟机和云分发程序和数据