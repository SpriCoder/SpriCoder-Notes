Lec2-Shell Programming
---

# 1. What is Shell?
1. Shell:
   1. A command interpreter and programming environment
2. 用户和操作系统之间的接口
3. 作为核外程序而存在

## 1.1. Shell: 用户和操作系统之间的接口
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Linux-Programming/img/lec2/1.png)

## 1.2. Shell：作为核外程序而存在
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Linux-Programming/img/lec2/2.png)

## 1.3. 各种不同的Shell
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Linux-Programming/img/lec2/3.png)

| **shell**名称 | 描述                                             | 位置            |
| ------------- | ------------------------------------------------ | --------------- |
| ash           | 一个小的shell                                    | /bin/ash        |
| ash.static    | 一个不依靠软件库的ash版本                        | /bin/ash.static |
| bsh           | ash的一个符号链接                                | /bin/bsh        |
| bash          | “Bourne Again Shell”。Linux中的主角，来自GNU项目 | /bin/bash       |
| sh            | bash的一个符号链接                               | /bin/sh         |
| csh           | C shell, tcsh的一个符号链接                      | /bin/csh        |
| tcsh          | 和csh兼容的shell                                 | /bin/tcsh       |
| ksh           | Korn Shell                                       | /bin/ksh        |

## 1.4. Shell 的双重角色
1. 命令解释程序
   1. Linux的开机启动过程；进程树
   2. Shell的工作步骤
      1. 打印提示符；得到命令行；解析命令；查找文件；准备参数；执行命令
2. 独立的程序设计语言解释器
   1. KISS (Keep It Small and Stupid)
   2. Reusable tools
   3. Redirection and pipe

## 1.5. UNIX的哲学（示例）
1. 重定向
   1. 使用"echo"创建文件吗？
2. 管道
   1. 获取目录中文件的数量？
   2. 仅显示子目录？
   3. ar t /usr/lib/libc.a | grep printf | pr -4 -t(?)

# 2. 脚本

## 2.1. 脚本是能在命令行直接输入的
1. 但仅会执行一次

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Linux-Programming/img/lec2/4.png)

## 2.2. 编写脚本文件
1. 脚本文件
   1. 注释
   2. 退出码(exit code)

```bash
#!/bin/bash
# Here is comments
for file in *; do
  if grep –l POSIX $file; then
    more $file
  fi
done
exit 0
```

## 2.3. 执行脚本文件
1. Method 1: `sh script_file`
2. Method 2: 
   1. `chmod +x script_file (chown, chgrp optionally)`
   2. `./script_file`
3. Method 3: 
   1. `source script_file, or`
   2. `./script_file`

## 2.4. 用户环境
1. `.bash_profile`, `.bash_logout`, `.bashrc files`
   1. `.bash_profile`: 用户登录时被读取，其中包含的命令被bash执行
   2. `.bashrc`: 启动一个新的shell时读取并执行
   3. `.bash_logout`: 登录退出时读取执行
2. Alias
   1. alias/unaliascommand
3. 环境变量
   1. export command
   2. export, env & set command

## 2.5. 变量
1. 用户变量
2. 环境变量
3. 参数变量和内部变量

### 2.5.1. 用户变量
1. 用户变量：
   1. 用户在shell脚本里定义的变量
2. 变量的赋值和使用
   1. `var=value`
   2. `echo $var`
3. read命令
   1. 用法：`read var` 或`read`
   2. `REPLY variable`
4. 引号的用法
   1. 双引号，单引号
   2. 转义符"\"

### 2.5.2. read 用法
```bash
#! /bin/bash
echo -n "Enter your name: "       # 参数-n的作用是不换行，echo默认是换行
read name                         #从键盘输入
echo "hello $name, welcome to my program"
exit 0                            #退出shell程序。
```
```SH
read -p "Enter your name:" name   #-p参数，允许在read命令行中直接指定一个提示

read -p "Enter a number:" number
echo $number
exit 0
```
```sh
#! /bin/bash
# 5s内输入
if read -t 5 -p "please enter your name:" name
then
  echo "hello $name， welcome to my script"
else
  echo "sorry, too slow"
fi
exit 0
```
```sh
#! /bin/bash
# 只读取一个字符
read -n1 -p "DO you want to continue[ Y/N] ?" answer
case $answer in
Y|y)
  echo "fine, continue";;
N|n)
  echo "ok, good bye";;
*)
  echo "error choice";;
esac
exit 0
```

```sh
#! /bin/bash
# 不显示输入
read -s -p "Enter your password: " pass
echo "your password is $pass"
exit 0
```
```sh
#! /bin/bash
count=1
cat viewFile.sh| while read line
do
  echo "Scount:$line"
  count=$(($count + 1))
done
echo "Total Count:$count"
exit 0
```

## 2.6. 引号的用法
1. 单引号内的所有字符都保持它本身字符的意思，而不会被bash进行解释，例如，`$`就是`$`本身而不再是bash的变量引用符；\就是\本身而不再是bash的转义字符。
2. 除了$、``（不是单引号）和\外，双引号内的所有字符将保持字符本身的含义而不被bash解释

## 2.7. 环境变量
1. 环境变量：Shell环境提供的变量。通常使用大写字母做名字

| 环境变量 | 说明                                                                                                  |
| -------- | ----------------------------------------------------------------------------------------------------- |
| $HOME    | 当前用户的登陆目录                                                                                    |
| $PATH    | 以冒号分隔的用来搜索命令的目录清单                                                                    |
| $PS1     | 命令行提示符，通常是”$”字符                                                                           |
| $PS2     | 辅助提示符，用来提示后续输入，通常是”>”字符                                                           |
| $IFS     | 输入区分隔符。当shell读取输入数据时会把一组字符看成是单词之间的分隔符，通常是空格、制表符、换行符等。 |

1. env：显示全部环境变量
2. set：设置环境变量


```shell
sed 's/ A  /  B /g' code1.cpp
正则表达式
```

## 2.8. 参数变量和内部变量
1. 调用脚本程序时如果带有参数，对应的参数和额外产生的一些变量。


| 环境变量      | 说明                                                                                      |
| ------------- | ----------------------------------------------------------------------------------------- |
| `$#`          | 传递到脚本程序的参数个数                                                                  |
| `$0`          | 脚本程序的名字                                                                            |
| `$1`, `$2`, … | 脚本程序的参数                                                                            |
| `$*`          | 一个全体参数组成的清单，它是一个独立的变量，各个参数之间用环境变量IFS中的第一个字符分隔开 |
| `$@`          | “$*”的一种变体，它不使用IFS环境变量。                                                     |

## 2.9. 条件测试
1. 退出码
2. test命令：`test expression` 或 `[ expression ]`
3. test命令支持的条件测试
   1. 字符串比较
   2. 算术比较
   3. 与文件有关的条件测试
   4. 逻辑操作

## 2.10. 字符串比较

| 字符串比较  | 结果                       |
| ----------- | -------------------------- |
| str1 = str2 | 两个字符串相同则结果为真   |
| str1!=str2  | 两个字符串不相同则结果为真 |
| -z str      | 字符串为空则结果为真       |
| -n str      | 字符串不为空则结果为真     |

## 2.11. 算术比较

| 算术比较        | 结果                             |
| --------------- | -------------------------------- |
| expr1 –eq expr2 | 两个表达式相等则结果为真         |
| expr1 –ne expr2 | 两个表达式不等则结果为真         |
| expr1 –gt expr2 | expr1 大于expr2 则结果为真       |
| expr1 –ge expr2 | expr1 大于或等于expr2 则结果为真 |
| expr1 –lt expr2 | expr1 小于expr2 则结果为真       |
| expr1 –le expr2 | expr1 小于或等于expr2 则结果为真 |

## 2.12. 与文件有关的条件测试

| 文件条件测试 | 结果                         |
| ------------ | ---------------------------- |
| -e file      | 文件存在则结果为真           |
| -d file      | 文件是一个子目录则结果为真   |
| -f file      | 文件是一个普通文件则结果为真 |
| -s file      | 文件的长度不为零则结果为真   |
| -r file      | 文件可读则结果为真           |
| -w file      | 文件可写则结果为真           |
| -x file      | 文件可执行则结果为真         |

## 2.13. 逻辑操作

| 逻辑操作       | 结果                        |
| -------------- | --------------------------- |
| ! expr         | 逻辑表达式求反              |
| expr1 –a expr2 | 两个逻辑表达式“And”（“与”） |
| expr1 –o expr2 | 两个逻辑表达式“Or”（“或”）  |


## 2.14. 条件操作

### 2.14.1. if语句
1. 形式

```shell
if [ expression ]
then
statements
elif [ expression ]
then
statements
elif …
else
statements
fi
```

2. 紧凑形式:`;` 同一行上多个命令的分隔符

```bash
# eg.1 .bash_profile
if [ -f ~/.bashrc ]; then
. ~/.bashrc
fi

# eg.2
# !/bin/sh
echo "Is this morning? Please answer yes or no."
read answer
if [ "$answer" = "yes" ]; then
  echo "Good morning"
elif [ "$answer" = "no" ]; then
  echo "Good afternoon"
else
  echo "Sorry, $answer not recognized. Enter yes or no"
  exit 1
fi
exit 0
```

### 2.14.2. case语句
1. 形式

```bash
case str in
  str1 | str2) statements;;
  str3 | str4) statements;;
  *) statements;;
esac
```

2. 例子Eg

```bash
#!/bin/sh
echo "Is this morning? Please answer yes or no."
read answer
case "$answer" in
yes | y | Yes | YES) echo "Good morning!" ;;
no | n | No | NO) echo "Good afternoon!" ;;
*) echo "Sorry, answer not recognized." ;;
esac
exit 0
```

## 2.15. 重复语句

### 2.15.1. for语句
1. 形式

```bash
for var in list
do
  statements
done
```

2. 适用于对一系列字符串循环处理

```bash
#!/bin/sh
for file in $(ls f*.sh); do
  lpr $file
done
exit 0
```

### 2.15.2. while语句
1. 形式

```bash
while condition
do
  statements
done
```

2. 例子

```bash
quit=n
while [ "$quit" != "y" ]; do
  read menu_choice
  case "$menu_choice" in
    a) do_something;;
    b) do_anotherthing;;
    …
    q|Q) quit=y;;
    *) echo "Sorry, choice not recognized.";;
  esac
done

a=0
while [ "$a" -le "$LIMIT" ]
do
  a=$(($a+1))
  if [ "$a" -gt 2 ]
  then
    break # Skip entire rest of loop.
  fi
  echo -n "$a"
done
```

### 2.15.3. until语句
1. 形式

```bash
until condition
do
  statements
done
```

2. Not recommended (while statement is preferred)

### 2.15.4. select语句
1. 形式

```bash
select item in itemlist
do
  statements
done
```

2. 作用：生成菜单列表
3. Eg. 一个简单的菜单选择程序

```bash
#!/bin/sh
clear
select item in Continue Finish
do
  case "$item" in
    Continue) ;;
    Finish) break ;;
    *) echo "Wrong choice! Please select again!" ;;
  esac
done
```

## 2.16. 补充read
```shell
read [-rs] [-a ARRAY] [-d delim] [-n nchars] [-N nchars] [-p prompt] [-t timeout] [var_name1 var_name2 ...]

选项说明：
-a：将分裂后的字段依次存储到指定的数组中，存储的起始位置从数组的index=0开始。
-d：指定读取行的结束符号。默认结束符号为换行符。
-n：限制读取N个字符就自动结束读取，如果没有读满N个字符就按下回车或遇到换行符，则也会结束读取。
-N：严格要求读满N个字符才自动结束读取，即使中途按下了回车或遇到了换行符也不结束。其中换行符或回车算一个字符。
-p：给出提示符。默认不支持"\n"换行，要换行需要特殊处理，见下文示例。例如，"-p 请输入密码："
-r：禁止反斜线的转义功能。这意味着"\"会变成文本的一部分。
-s：静默模式。输入的内容不会回显在屏幕上。
-t：给出超时时间，在达到超时时间时，read退出并返回错误。也就是说不会读取任何内容，即使已经输入了一部分。
```

```shell
read num
[ $num -eq 2 ]
```

如果输入的是纯数值的话，那么比较的时候，可以使用算数比较，也可以使用字符串比较。


## 2.17. 命令表和语句块
1. 命令表(命令组合)
2. 语句块

### 2.17.1. 命令表
1. 命令组合
   1. 分号串联：`command1 ; command2 ;`
   2. 条件组合
      1. AND命令表，格式：statement1 && statement2 && statement3
      2. OR命令表，格式：statement1 || statement2 || statement3 || …

### 2.17.2. 语句块
1. 形式

```bash
{
statement1
statement2
}

# or

{ statement1; statement2 ;}
```

### 2.17.3. 函数
1. 形式
```bash
func()
{
statements
}
```

2. 局部变量:local关键字
3. 函数的调用:func para1 para2
4. 返回值:return
5. 例子

```bash
yesno()
{
  msg="$1"
  def="$2"
  while true; do
    echo " "
    echo "$msg"
    read answer
    if [ -n "$answer" ]; then
      case "$answer" in
        y|Y|yes|YES)
        return 0
        ;;
        n|N|no|NO)
        return 1
        ;;
        *)
        echo " "
        echo "ERROR: Invalid response,
        expected \"yes\" or \"no\"."
        continue
        ;;
        esac
    else
      return $def
  fi
  done
}

if yesno "Continue installation? [n]" 1 ; then
  :
  else
    exit 1
f
```

## 2.18. 其他
1. 杂项命令：`break, continue, exit, return, export, set, unset, trap, ":", ".", …`
2. 捕获命令输出
3. 算术扩展
4. 参数扩展
5. 即时文档

### 2.18.1. 杂项命令
1. break: 从for/while/until循环退出
2. continue: 跳到下一个循环继续执行
3. exit n: 以退出码"n"退出脚本运行
4. return: 函数返回
5. export: 将变量导出到shell，使之成为shell的环境变量
6. set: 为shell设置参数变量
7. unset: 从环境中删除变量或函数
8. trap: 指定在收到操作系统信号后执行的动作
9. ":"(冒号命令): 空命令
10. "."(句点命令)或source: 在当前shell中执行命令

### 2.18.2. 捕获命令输出
1. 语法
   1. $(command)
   2. \`command\`
2. 举例

```bash
#!/bin/sh
echo "The current directory is $PWD"
echo "The current directory is $(pwd)"
exit 0
```

### 2.18.3. 算术扩展
1. $(())扩展

```bash
#!/bin/sh
x=0
while [ "$x" –ne 10 ]; do
  echo $x
  x=$(($x+1))
done
exit 0
```

### 2.18.4. 参考扩展
1. 问题:
   1. 批处理 1_tmp, 2_tmp, …
2. 方法

```bash
#!/bin/sh
i=0
while [ "$i" –ne 10 ]; do
  touch "${i}_tmp"
  i=$(($i+1))
done
exit 0
```

### 2.18.5. 参数扩展更复杂的形式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Linux-Programming/img/lec2/11.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Linux-Programming/img/lec2/12.png)

### 2.18.6. 即时文档
1. 在shell脚本中向一条命令传送输入数据
2. Example

```bash
#!/bin/bash
cat >> file.txt << !CATINPUT!
Hello, this is a here document.
!CATINPUT!
```