# Shell基本运算符
Shell 和其他编程语言一样，支持多种运算符，包括：

- 算数运算符
- 关系运算符
- 布尔运算符
- 字符串运算符
- 文件测试运算符

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

```txt
#!/bin/bash

val=`expr 2 + 2`
echo "两数之和为 : $val"
```

执行脚本，输出结果如下所示：

```txt
两数之和为 : 4
```

两点注意：

- 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2。
- 完整的表达式要被 ` ` 包含，这个字符是反引号在 Esc 键下边。

## 算术运算符
下表列出了常用的算术运算符，假定变量 a 为 10，变量 b 为 20：

![image](https://github.com/user-attachments/assets/c98ca917-e0d9-4e90-8617-3746e2cd58f0)


算术运算符实例如下：

```txt
#!/bin/bash

a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
   echo "a 等于 b"
fi
if [ $a != $b ]
then
   echo "a 不等于 b"
fi
```

执行脚本，输出结果如下所示：

```txt
a + b : 30
a - b : -10
a * b : 200
b / a : 2
b % a : 0
a 不等于 b
```

**注意：**

- 乘号(*)前边必须加反斜杠\才能实现乘法运算；
- if…then…fi 是条件语句，后续将会讲解。
- 在 MAC 中 shell 的 expr 语法是：$((表达式))，此处表达式中的 “*” 不需要转义符号 \ 。

```txt
let varName=算术表达式
varName=$[算术表达式]
varName=$((算术表达式))
```

## 关系运算符
关系运算符只支持数字，不支持字符串，除非字符串的值是数字。

下表列出了常用的关系运算符，假定变量 a 为 10，变量 b 为 20：

![image](https://github.com/user-attachments/assets/dd4c777a-dd18-491d-a418-211f98335a73)


关系运算符实例如下：

```txt
#!/bin/bash

a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : a 等于 b"
else
   echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b: a 不等于 b"
else
   echo "$a -ne $b : a 等于 b"
fi
if [ $a -gt $b ]
then
   echo "$a -gt $b: a 大于 b"
else
   echo "$a -gt $b: a 不大于 b"
fi
if [ $a -lt $b ]
then
   echo "$a -lt $b: a 小于 b"
else
   echo "$a -lt $b: a 不小于 b"
fi
if [ $a -ge $b ]
then
   echo "$a -ge $b: a 大于或等于 b"
else
   echo "$a -ge $b: a 小于 b"
fi
if [ $a -le $b ]
then
   echo "$a -le $b: a 小于或等于 b"
else
   echo "$a -le $b: a 大于 b"
fi
```

执行脚本，输出结果如下所示：

```txt
10 -eq 20: a 不等于 b
10 -ne 20: a 不等于 b
10 -gt 20: a 不大于 b
10 -lt 20: a 小于 b
10 -ge 20: a 小于 b
10 -le 20: a 小于或等于 b
```

## 布尔运算符
下表列出了常用的布尔运算符，假定变量 a 为 10，变量 b 为 20：

![image](https://github.com/user-attachments/assets/c0941f75-4a42-4a6d-8252-c63d5b5b9dd2)

布尔运算符实例如下：

```txt
#!/bin/bash

a=10
b=20

if [ $a != $b ]
then
   echo "$a != $b : a 不等于 b"
else
   echo "$a == $b: a 等于 b"
fi
if [ $a -lt 100 -a $b -gt 15 ]
then
   echo "$a 小于 100 且 $b 大于 15 : 返回 true"
else
   echo "$a 小于 100 且 $b 大于 15 : 返回 false"
fi
if [ $a -lt 100 -o $b -gt 100 ]
then
   echo "$a 小于 100 或 $b 大于 100 : 返回 true"
else
   echo "$a 小于 100 或 $b 大于 100 : 返回 false"
fi
if [ $a -lt 5 -o $b -gt 100 ]
then
   echo "$a 小于 5 或 $b 大于 100 : 返回 true"
else
   echo "$a 小于 5 或 $b 大于 100 : 返回 false"
fi
```

执行脚本，输出结果如下所示：

```txt
10 != 20 : a 不等于 b
10 小于 100 且 20 大于 15 : 返回 true
10 小于 100 或 20 大于 100 : 返回 true
10 小于 5 或 20 大于 100 : 返回 false
```

## 逻辑运算符
以下介绍 Shell 的逻辑运算符，假定变量 a 为 10，变量 b 为 20:

![image](https://github.com/user-attachments/assets/42dc1068-d2e3-44c6-842b-368e375fff4f)


逻辑运算符实例如下：

```txt
#!/bin/bash

a=10
b=20

if [[ $a -lt 100 && $b -gt 100 ]]
then
   echo "返回 true"
else
   echo "返回 false"
fi

if [[ $a -lt 100 || $b -gt 100 ]]
then
   echo "返回 true"
else
   echo "返回 false"
fi
```

执行脚本，输出结果如下所示：

```txt
返回 false
返回 true
```

## 字符串运算符
下表列出了常用的字符串运算符，假定变量 a 为 “abc”，变量 b 为 “efg”：

![image](https://github.com/user-attachments/assets/a0d19054-6abc-49fd-b246-cca6b30c34c8)

字符串运算符实例如下：

```txt
#!/bin/bash

a="abc"
b="efg"

if [ $a = $b ]
then
   echo "$a = $b : a 等于 b"
else
   echo "$a = $b: a 不等于 b"
fi
if [ $a != $b ]
then
   echo "$a != $b : a 不等于 b"
else
   echo "$a != $b: a 等于 b"
fi
if [ -z $a ]
then
   echo "-z $a : 字符串长度为 0"
else
   echo "-z $a : 字符串长度不为 0"
fi
if [ -n "$a" ]
then
   echo "-n $a : 字符串长度不为 0"
else
   echo "-n $a : 字符串长度为 0"
fi
if [ $a ]
then
   echo "$a : 字符串不为空"
else
   echo "$a : 字符串为空"
fi
```

执行脚本，输出结果如下所示：

```txt
abc = efg: a 不等于 b
abc != efg : a 不等于 b
-z abc : 字符串长度不为 0
-n abc : 字符串长度不为 0
abc : 字符串不为空
```

## 文件测试运算符
文件测试运算符用于检测 Unix 文件的各种属性。

属性检测描述如下：

![image](https://github.com/user-attachments/assets/e5e4c805-581d-4d68-8c96-2dc2075f9780)


其他检查符：

- **-S**: 判断某文件是否 socket。
- **-L**: 检测文件是否存在并且是一个符号链接。

变量 file 表示文件 /var/www/runoob/test.sh，它的大小为 100 字节，具有 rwx 权限。下面的代码，将检测该文件的各种属性：

```txt
#!/bin/bash

file="/var/www/runoob/test.sh"
if [ -r $file ]
then
   echo "文件可读"
else
   echo "文件不可读"
fi
if [ -w $file ]
then
   echo "文件可写"
else
   echo "文件不可写"
fi
if [ -x $file ]
then
   echo "文件可执行"
else
   echo "文件不可执行"
fi
if [ -f $file ]
then
   echo "文件为普通文件"
else
   echo "文件为特殊文件"
fi
if [ -d $file ]
then
   echo "文件是个目录"
else
   echo "文件不是个目录"
fi
if [ -s $file ]
then
   echo "文件不为空"
else
   echo "文件为空"
fi
if [ -e $file ]
then
   echo "文件存在"
else
   echo "文件不存在"
fi
```

执行脚本，输出结果如下所示：

```txt
文件可读
文件可写
文件可执行
文件为普通文件
文件不是个目录
文件不为空
文件存在
```

# test命令
Shell中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。

## 数值测试

![image](https://github.com/user-attachments/assets/87da019f-674d-46b9-90cb-0d07802b9a77)

实例演示：

```txt
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
```

输出结果：

```txt
两个数相等！
```

代码中的 [] 执行基本的算数运算，如：

```txt
#!/bin/bash

a=5
b=6

result=$[a+b] # 注意等号两边不能有空格
echo "result 为： $result"
```

结果为:

```txt
result 为： 11
```

## 字符串测试

![image](https://github.com/user-attachments/assets/a1fad32b-06e8-4b03-9f89-49f811afb088)


实例演示：

```txt
num1="ru1noob"
num2="runoob"
if test $num1 = $num2
then
    echo '两个字符串相等!'
else
    echo '两个字符串不相等!'
fi
```

输出结果：

```txt
两个字符串不相等!
```

## 文件测试

![image](https://github.com/user-attachments/assets/c1a4c97e-b967-4b79-9ffa-2fdb7c4772f8)


实例演示：

```txt
cd /bin
if test -e ./bash
then
    echo '文件已存在!'
else
    echo '文件不存在!'
fi
```

输出结果：

```txt
文件已存在!
```

另外，Shell还提供了与( -a )、或( -o )、非( ! )三个逻辑操作符用于将测试条件连接起来，其优先级为："!“最高，”-a"次之，"-o"最低。例如：

```txt
cd /bin
if test -e ./notFile -o -e ./bash
then
    echo '至少有一个文件存在!'
else
    echo '两个文件都不存在'
fi
```

输出结果：

```txt
至少有一个文件存在!
```

# Shell 流程控制
## if else判断语句
if 语句语法格式：

```txt
if condition
then
    command1 
    command2
    ...
    commandN 
fi
```

写成一行（适用于终端命令提示符）：

```txt
if [ $(ps -ef | grep -c "ssh") -gt 1 ]; then echo "true"; fi
```

if else 语法格式：

```txt
if condition
then
    command1 
    command2
    ...
    commandN
else
    command
fi
```

if else-if else 语法格式：

```txt
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

以下实例判断两个变量是否相等：

```txt
a=10
b=20
if [ $a == $b ]
then
   echo "a 等于 b"
elif [ $a -gt $b ]
then
   echo "a 大于 b"
elif [ $a -lt $b ]
then
   echo "a 小于 b"
else
   echo "没有符合的条件"
fi
```

输出结果：

```txt
a 小于 b
```

if else语句经常与test命令结合使用，如下所示：

```txt
num1=$[2*3]
num2=$[1+5]
if test $[num1] -eq $[num2]
then
    echo '两个数字相等!'
else
    echo '两个数字不相等!'
fi
```

输出结果：

```txt
两个数字相等!
```

## for循环
for循环一般格式为：

```txt
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

写成一行：

```txt
for var in item1 item2 ... itemN; do command1; command2… done;
```

例如，顺序输出当前列表中的数字：

```txt
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done
```

输出结果：

```txt
The value is: 1
The value is: 2
The value is: 3
The value is: 4
The value is: 5
```

顺序输出字符串中的字符：

```txt
for str in 'This is a string'
do
    echo $str
done
```

输出结果：

```txt
This is a string
```

## while循环
while循环格式为：

```txt
while condition
do
    command
done
```

示例：

```txt
#!/bin/bash
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```

运行脚本，输出：

```txt
1
2
3
4
5
```

while循环可用于读取键盘信息。下面的例子中，输入信息被设置为变量FILM，按Ctrl-D结束循环。

```txt
echo '按下 <CTRL-D> 退出'
echo -n '输入你最喜欢的网站名: '
while read FILM
do
    echo "是的！$FILM 是一个好网站"
done
```

运行脚本，输出类似下面：

```txt
按下 <CTRL-D> 退出
输入你最喜欢的网站名:淘宝
是的！淘宝 是一个好网站
```

## 无限循环
无限循环语法格式：

```txt
while :
do
    command
done
```

或者

```txt
while true
do
    command
done
```

或者

```txt
for (( ; ; ))
```


## until 循环
until 循环执行一系列命令直至条件为 true 时停止。

until 循环与 while 循环在处理方式上刚好相反。

一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用。

until 语法格式:

```txt
until condition
do
    command
done
```

condition 一般为条件表达式，如果返回值为 false，则继续执行循环体内的语句，否则跳出循环。

以下实例我们使用 until 命令来输出 0 ~ 9 的数字：

```txt
#!/bin/bash

a=0

until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```

运行结果：

输出结果为：

```txt
0
1
2
3
4
5
6
7
8
9
```

## case
Shell case语句为多选择语句。可以用case语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。case语句格式如下：

```txt
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2）
    command1
    command2
    ...
    commandN
    ;;
esac
```

下面的脚本提示输入1到4，与每一种模式进行匹配：

```txt
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

输入不同的内容，会有不同的结果，例如：

```txt
输入 1 到 4 之间的数字:
你输入的数字为:
3
你选择了 3
```

## 跳出循环
在循环过程中，有时候需要在未达到循环结束条件时强制跳出循环，Shell使用两个命令来实现该功能：break和continue。

break命令允许跳出所有循环（终止执行后面的所有循环）。

下面的例子中，脚本进入死循环直至用户输入数字大于5。要跳出这个循环，返回到shell提示符下，需要使用break命令。

```txt
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

执行以上代码，输出结果为：

```txt
输入 1 到 5 之间的数字:3
你输入的数字为 3!
输入 1 到 5 之间的数字:7
你输入的数字不是 1 到 5 之间的! 游戏结束
```

continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。



# Shell输入/输出重定向
重定向命令列表如下：

![image](https://github.com/user-attachments/assets/2d3b0256-f96e-44f3-a09b-c1db29bb4c72)


## 输出重定向
重定向一般通过在命令间插入特定的符号来实现。特别的，这些符号的语法如下所示:

```txt
command1 > file1
```

上面这个命令执行command1然后将输出的内容存入file1。

注意任何file1内的已经存在的内容将被新内容替代。如果要将新内容添加在文件末尾，请使用>>操作符。

输出重定向会覆盖文件内容：

```txt
$ echo "www.baidu.com" > users
$ cat users
www.baidu.com
$
```

如果不希望文件内容被覆盖，可以使用 >> 追加到文件末尾，例如：

```txt
$ echo "www.baidu.com" >> users
$ cat users
www.baidu.com
www.baidu.com
$
```

## 输入重定向
和输出重定向一样，Unix 命令也可以从文件获取输入，语法为：

```txt
command1 < file1
```

这样，本来需要从键盘获取输入的命令会转移到文件读取内容。

注意：输出重定向是大于号(>)，输入重定向是小于号(<)。

统计 users 文件的行数,执行以下命令：

```txt
python@ubuntu:~/test$ wc -l test 
4 test
```

也可以将输入重定向到 users 文件：

```txt
python@ubuntu:~/test$ wc -l <test
4
```

注意：上面两个例子的结果不同：第一个例子，会输出文件名；第二个不会，因为它仅仅知道从标准输入读取内容。

同时替换输入和输出，执行command1，从文件infile读取内容，然后将输出写入到outfile中:

```txt
command1 < infile > outfile
```

## 重定向深入讲解
一般情况下，每个 Unix/Linux 命令运行时都会打开三个文件：

- 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。
- 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。
- 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。

默认情况下，command > file 将 stdout 重定向到 file，command < file 将stdin 重定向到 file。

如果希望 stderr 重定向到 file，可以这样写：

```txt
$ command 2 > file
```

如果希望 stderr 追加到 file 文件末尾，可以这样写：

```txt
$ command 2 >> file
```

2 表示标准错误文件(stderr)。

如果希望将 stdout 和 stderr 合并后重定向到 file，可以这样写：

```txt
$ command > file 2>&1
或者
$ command >> file 2>&1
```

如果希望对 stdin 和 stdout 都重定向，可以这样写：

```txt
$ command < file1 >file2
```

command 命令将 stdin 重定向到 file1，将 stdout 重定向到 file2。

## Here Document
Here Document 是 Shell 中的一种特殊的重定向方式，用来将输入重定向到一个交互式 Shell 脚本或程序。

它的基本的形式如下：

```txt
command << delimiter
    document
delimiter
```

它的作用是将两个 delimiter 之间的内容(document) 作为输入传递给 command。

注意：结尾的delimiter 一定要顶格写，前面不能有任何字符，后面也不能有任何字符，包括空格和 tab 缩进。

在命令行中通过 wc -l 命令计算 Here Document 的行数：

```txt
$ wc -l << EOF
    欢迎来到
    菜鸟教程
    www.runoob.com
EOF
3          # 输出结果为 3 行
$
```

## /dev/null 文件
如果希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null：

```txt
$ command > /dev/null
```

/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果。

如果希望屏蔽 stdout 和 stderr，可以这样写：

```txt
$ command > /dev/null 2>&1
```

0 是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。

# 实例
## 杨辉三角：

```txt
#!/bin/bash

if (test -z $1) ;then 
 read -p "Input high Int Lines:" high 
else 
 high=$1 
fi 
if (test -z $2) ;then 
 space=4
else 
 space=$2
fi

printspace(){
  #空位填充
  for((z=1;z<=$1;z++));do
    echo -n " "
  done
}

a[0]=1     
for((i=0;i<=high;i++));do
  #产生当前列数据数组
  for ((j=$i;j>0;j--));do 
    ((a[$j]+=a[$j-1])) 
  done
  printspace $((($high-$i)*$space/2))
  for ((j=0;j<=$i;j++));do
    num=$(($space-${#a[$j]}))
    printspace $(($num/2))
    echo -n ${a[$j]}
    printspace $(($num-$num/2))
  done
  echo ""
done
```

## sum()&max():

```txt
#!/bin/bash

echo "shell的函数返回值只能为0~255的整数，高位自动丢弃"
sum(){
 sum=0
 for i in $@
 do
  if test $i -ne $1;then
   echo -n "+"
  fi
  echo -n "$i"
  sum=$(($sum+$i))
 done
 echo "=$sum"
 return $(($sum))
}
sum $@
echo "‘sum()’函数返回值："$?

max(){
 max=0
 for i in $@;do
  if test $i -ge $max;then
    max=$i
  fi
 done
 echo "参数最大值：$max"
 return $(($max))
}

max $@

echo "‘max()’函数返回值："$?
```

## 99乘法表：

```txt
#!/bin/bash

for i in {1..9};do
 for((j=1;j<=i;j++));do
  echo -en "$i*$j=$(($i*$j))\t"
 done
 echo ""
done

for a in {1..9};do
    for b in {0..9};do
        for c in {0..9};do
            number1=$((a*100+b*10+c))
            number2=$((a**3+b**3+c**3))
            if test $number1 -eq $number2; then
                echo "Found number $number1"
            fi
        done
    done
done
```

# 文本编辑命令
## cut命令

```txt
选项与参数：
-d  ：后面接分隔字符。与 -f 一起使用；
-f  ：依据 -d 的分隔字符将一段信息分割成为数段，用 -f 取出第几段的意思；
-c  ：以字符 (characters) 的单位取出固定字符区间；
```

cut以行为单位，根据分隔符把行分成若干列，这样就可以指定选取哪些列了。

```txt
cut -d '分隔字符' -f 选取的列数
echo $PATH|cut -d ':' -f 2  	--选取第2列
echo $PATH|cut -d ':' -f 3,5  	--选取第3列和第5列
echo $PATH|cut -d ':' -f 3-5  	--选取第3列到第5列
echo $PATH|cut -d ':' -f 3-   	--选取第3列到最后1列
echo $PATH|cut -d ':' -f 1-3,5	--选取第1到第3列还有第5列
```

只显示/etc/passwd的用户和shell：

```txt
#cat /etc/passwd | cut -d ':' -f 1,7 
root:/bin/bash
daemon:/bin/sh
bin:/bin/sh
```


## sed命令
sed 可依照脚本的指令来处理、编辑文本文件。

Sed 主要用来自动编辑一个或多个文件、简化对文件的反复操作、编写转换程序等。

语法:

```txt
sed [-e<script>][-f<script文件>][文本文件]
```


**参数说明：**

- -e <script>以指定的script来处理输入的文本文件。
- -f<script文件>以指定的script文件来处理输入的文本文件。
- -n仅显示script处理后的结果，一般跟p动作搭配使用。
- -i使用处理后的结果修改文件。

**动作说明：**

- a：在指定行后面插入内容
- i：在指定行前面插入内容
- d：删除指定行
- c ：替换指定行
- p ：打印指定行的数据，通常需要跟-n选项搭配使用
- s ：替换指定字符，兼容vim的替换语法，例如 1,20s/old/new/g

## 元字符集
sed支持一般的正则表达式，下面是支持的正则语法：

![image](https://github.com/user-attachments/assets/342908c4-cfab-4ede-a321-a3c7c00f1bcc)

## a|i:在指定行位置添加行

```txt
python@xxx:~/test$ cat testfile              
 LINUX!  
 Linux is a free unix-type opterating system.  
 This is a linux testfile!  
 Linux test 

python@xxx:~/test$ sed -e 2a\newline testfile 
 LINUX!  
 Linux is a free unix-type opterating system.  
newline
 This is a linux testfile!  
 Linux test 
 ```

默认情况下-e参数可以省略：

```txt
python@xxx:~/test$ cat testfile|sed '2a\newline'
 LINUX!  
 Linux is a free unix-type opterating system.  
newline
 This is a linux testfile!  
 Linux test 

python@xxx:~/test$ sed '2a newline' testfile
 LINUX!  
 Linux is a free unix-type opterating system.  
newline
 This is a linux testfile!  
 Linux test 
 ```

![image](https://github.com/user-attachments/assets/ef069c97-6b65-4ebb-a5e3-82f72e21bac0)


最后一行加入 # This is a test:

![image](https://github.com/user-attachments/assets/921cf4ac-95df-4644-8f12-c0babbba0b9e)

同时添加多行：

![image](https://github.com/user-attachments/assets/5fc33bc3-8283-442c-8f08-bbb5c0595b31)

## d:删除指定行

```txt
[root@www ~]# nl /etc/passwd | sed '2,5d'
1 root:x:0:0:root:/root:/bin/bash
6 sync:x:5:0:sync:/sbin:/bin/sync
7 shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
.....(后面省略).....
 ```

只删除第2行：

```txt
nl /etc/passwd | sed '2d' 
 ```

删除第3到最后一行：

```txt
nl /etc/passwd | sed '3,$d' 
 ```

![image](https://github.com/user-attachments/assets/8a18ddd7-bfed-4f61-afd4-57c8a14b7a67)

## c:替换指定行

![image](https://github.com/user-attachments/assets/20169617-9fc8-4d41-9604-02248b36e764)


## p:仅显示指定行
不加-n选项时，除了输出匹配行，还同时会输出所有行，所以需要加-n选项。

仅列出 /etc/passwd 文件内的第 5-7 行：

![image](https://github.com/user-attachments/assets/4fa882c9-ad38-46df-9798-27f29f627e9a)


## s:字符串替换
语法：

![image](https://github.com/user-attachments/assets/7e7886f3-d425-4c36-a32a-6c7b2e2e6834)

## y:单字符替换
跟s一样也用于替换，不过s替换的是整体，y替换的是每一字母对应的单个字母

把data中的第一行至第三行中的a替换成A，b替换成B，c替换成C：

```txt
sed '1,3y/abc/ABC/' data 
 ```

示例：

```txt
python@ubuntu:~/test$ echo "123" | sed 'y/13/34/' 
324
python@ubuntu:~/test$ echo "axxbxxcxx" | sed 'y/abc/123/'
1xx2xx3xx
 ```

## hHgG模式空间&保持空间
h命令是将当前模式空间中内容覆盖至保持空间，H命令是将当前模式空间中的内容追加至保持空间

g命令是将当前保持空间中内容覆盖至模式空间，G命令是将当前保持空间中的内容追加至模式空间

模拟tac命令：

```txt
python@ubuntu:~/test$ cat log.txt 
2 this is a test
3 Are you like awk
This's a test
10 There are orange,apple,mongo
python@ubuntu:~/test$ cat log.txt |sed '1!G;h;$!d'
10 There are orange,apple,mongo
This's a test
3 Are you like awk
2 this is a test
 ```

1!G第1行不 执行“G”命令，从第2行开始执行。

$!d，最后一行不删除（保留最后1行）

下图P表示模式空间，H代表保持空间：

![image](https://github.com/user-attachments/assets/2228f5f6-6f11-4035-a2ee-203c9f1c2a05)


递增序列：

```txt
python@ubuntu:~/test$ seq 3
1
2
3
python@ubuntu:~/test$ seq 3|sed 'H;g'
1

1
2

1
2
3
 ```

## 多次指定-e选项进行多点编辑
删除/etc/passwd第三行到末尾的数据，并把bash替换为blueshell：

```txt
nl /etc/passwd | sed -e '3,$d' -e 's/bash/blueshell/'
1  root:x:0:0:root:/root:/bin/blueshell
2  daemon:x:1:1:daemon:/usr/sbin:/bin/sh
 ```

删除一个文件以#开头的行和空行：

```txt
python@xxx:~/test$ nl abc -ba
     1
     2  b
     3  a
     4
     5  # aaaa
     6
     7  ddd
     8
     9  # sss
    10  eeee
    11
python@xxx:~/test$ sed -e '/^#/d' -e '/^$/d' abc
b
a
ddd
eeee
 ```

也可以通过;实现

```txt
python@ubuntu:~/test$ nl /etc/passwd | sed '3,$d;s/bash/blueshell/'
     1  root:x:0:0:root:/root:/bin/blueshell
     2  daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
python@ubuntu:~/test$ sed '/^#/d;/^$/d' abc
b
a
ddd
eeee
 ```

## 选项-i直接修改文件内容
默认情况下sed命令仅仅只是将处理结果显示在控制台，加-i选项则会修改文件内容。

将 regular_express.txt 内每一行结尾若为 . 则换成 !

```txt
[root@www ~]# cat regular_express.txt 
taobao.
google.
taobao.
facebook.
zhihu-
weibo-
[root@www ~]# sed -i 's/\.$/\!/g' regular_express.txt
[root@www ~]# cat regular_express.txt 
taobao!
google!
taobao!
facebook!
zhihu-
weibo-
```

# awk命令
AWK是一种处理文本文件的语言，是一个强大的文本分析工具。

之所以叫AWK是因为其取了三位创始人 Alfred Aho，Peter Weinberger, 和 Brian Kernighan 的 Family Name 的首字符。

语法：

```txt
awk [选项参数] 'script' var=value file(s)
或
awk [选项参数] -f scriptfile var=value file(s)
```


**选项参数说明：**

- -F fs or --field-separator fs 指定输入文件折分隔符，fs是一个字符串或者是一个正则表达式，如-F:。
- -v var=value or --asign var=value 赋值一个用户定义变量。
- -f scripfile or --file scriptfile 从脚本文件中读取awk命令。


## 基本用法

```txt
awk '{[pattern] action}' file
```

每行按空格或TAB分割，输出文本中的1、4列：

```txt
python@ubuntu:~/test$ cat log.txt 
2 this is a test
3 Are you like awk
This's a test
10 There are orange,apple,mongo
python@ubuntu:~/test$ awk '{print $1,$4}' log.txt
2 a
3 like
This's 
10 orange,apple,mongo
```

格式化输出：

```txt
python@ubuntu:~/test$ awk '{printf "%-8s %-10s\n",$1,$4}' log.txt
2        a         
3        like      
This's             
```

### -F指定分割字符

```txt
awk -F  #-F相当于内置变量FS, 指定分割字符
```

使用:分割,取/etc/passwd文件每个用户对应shell：

```txt
python@ubuntu:~/test$ awk -F: '{print $1,$7}'  /etc/passwd 
root /bin/bash
daemon /usr/sbin/nologin
bin /usr/sbin/nologin
sys /usr/sbin/nologin
sync /bin/sync
# 或者使用内建变量
python@ubuntu:~/test$ awk 'BEGIN{FS=":"} {print $1,$7}'  /etc/passwd  
root /bin/bash
daemon /usr/sbin/nologin
bin /usr/sbin/nologin
```

同时使用:和/l两个分隔符分割/etc/passwd文件

```txt
python@ubuntu:~/test$ awk -F '[:\/]' '{print $1,$7}'  /etc/passwd      
root root
daemon usr
bin bin
```

### -v设置变量

```txt
awk -v  # 设置变量
```

例子：

```txt
python@ubuntu:~/test$ cat log.txt 
2 this is a test
3 Are you like awk
This's a test
10 There are orange,apple,mongo
python@ubuntu:~/test$ awk -va=1 '{print $1,$1+a}' log.txt
2 3
3 4
This's 1
10 11
python@ubuntu:~/test$ awk -va=1 -vb=s '{print $1,$1+a,$1b}' log.txt
2 3 2s
3 4 3s
This's 1 This'ss
10 11 10s
```

### -f指定awk脚本

```txt
awk -f {awk脚本} {文件名}
```

脚本模块：

- BEGIN{ 这里面放的是执行前的语句 }
- END {这里面放的是处理完所有的行后要执行的语句 }
- {这里面放的是处理每一行时要执行的语句}

假设有这么一个文件（学生成绩表）：

```txt
$ cat score.txt
Marry   2143 78 84 77
Jack    2321 66 78 45
Tom     2122 48 77 71
Mike    2537 87 97 95
Bob     2415 40 57 62
```

awk脚本如下：

```txt
$ cat cal.awk
#!/bin/awk -f
#运行前
BEGIN {
    math = 0
    english = 0
    computer = 0
 
    printf "NAME    NO.   MATH  ENGLISH  COMPUTER   TOTAL\n"
    printf "---------------------------------------------\n"
}
#运行中
{
    math+=$3
    english+=$4
    computer+=$5
    printf "%-6s %-6s %4d %8d %8d %8d\n", $1,$2,$3,$4,$5,$3+$4+$5
}
#运行后
END {
    printf "---------------------------------------------\n"
    printf "  TOTAL:%10d %8d %8d \n", math, english, computer
    printf "AVERAGE:%10.2f %8.2f %8.2f\n", math/NR, english/NR, computer/NR
}
```

我们来看一下执行结果：

```txt
$ awk -f cal.awk score.txt
NAME    NO.   MATH  ENGLISH  COMPUTER   TOTAL
---------------------------------------------
Marry  2143     78       84       77      239
Jack   2321     66       78       45      189
Tom    2122     48       77       71      196
Mike   2537     87       97       95      279
Bob    2415     40       57       62      159
---------------------------------------------
  TOTAL:       319      393      350
AVERAGE:     63.80    78.60    70.00
```

## AWK工作原理
AWK 工作流程可分为三个部分：

- 读输入文件之前执行的代码段（由BEGIN关键字标识）。
- 主循环执行输入文件的代码段。
- 读输入文件之后的代码段（由END关键字标识）。

命令结构:

```txt
awk 'BEGIN{ commands } pattern{ commands } END{ commands }'
```

下面的流程图描述出了 AWK 的工作流程：

![image](https://github.com/user-attachments/assets/5526cf8d-2315-4f6b-941b-990ba39e14f4)


- 1、通过关键字 BEGIN 执行 BEGIN 块的内容，即 BEGIN 后花括号 {} 的内容。
- 2、完成 BEGIN 块的执行，开始执行body块。
- 3、读入有 \n 换行符分割的记录。
- 4、将记录按指定的域分隔符划分域，填充域，$0 则表示所有域(即一行内容)，1 ∗ ∗ 表 示 第 一 个 域 ， ∗ ∗ 1** 表示第一个域，**1∗∗表示第一个域，∗∗n 表示第 n 个域。
- 5、依次执行各 BODY 块，pattern 部分匹配该行内容成功后，才会执行 awk-commands 的内容。
- 6、循环读取并执行各行直到文件结束，完成body块执行。
- 7、开始 END 块执行，END 块可以输出最终结果。

### 运算符

![image](https://github.com/user-attachments/assets/f04b07e8-c563-4976-a524-edf30701bad1)


#### 过滤第一列大于2的行

```txt
$ awk '$1>2' log.txt    #命令
3 Are you like awk
This's a test
10 There are orange,apple,mongo
```

#### 过滤第一列等于2的行

```txt
$ awk '$1==2 {print $1,$3}' log.txt    #命令
#输出
2 is
```

#### 过滤第一列大于2并且第二列等于’Are’的行

```txt
$ awk '$1>2 && $2=="Are" {print $1,$2,$3}' log.txt    #命令
#输出
3 Are you
```

#### 内建变量

![image](https://github.com/user-attachments/assets/136749a0-4cf4-4a5a-858a-7a57d7393e46)

格式化变量说明：

- %s 输出字符串
- %i 输出整数
- %f 输出浮点数

%-5s 格式为左对齐且宽度为5的字符串代替（-表示左对齐），不使用则是又对齐。

%-4.2f 格式为左对齐宽度为4，保留两位小数。

```txt
python@ubuntu:~/test$ awk 'BEGIN{printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n","FILENAME","ARGC","FNR","FS","NF","NR","OFS","ORS","RS";printf "---------------------------------------------\n"} {printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n",FILENAME,ARGC,FNR,FS,NF,NR,OFS,ORS,RS}'  log.txt
FILENAME ARGC  FNR   FS   NF   NR  OFS  ORS   RS
---------------------------------------------
log.txt    2    1         5    1         
log.txt    2    2         5    2         
log.txt    2    3         3    3          
log.txt    2    4         4    4         

python@ubuntu:~/test$ awk -F: 'BEGIN{printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n","FILENAME","ARGC","FNR","FS","NF","NR","OFS","ORS","RS";printf "---------------------------------------------\n"} {printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n",FILENAME,ARGC,FNR,FS,NF,NR,OFS,ORS,RS}'  log.txt
FILENAME ARGC  FNR   FS   NF   NR  OFS  ORS   RS
---------------------------------------------
log.txt    2    1    :    1    1         
log.txt    2    2    :    1    2         
log.txt    2    3    :    1    3         
log.txt    2    4    :    1    4    
```

#### 输出顺序号 NR, 匹配文本行号

```txt
python@ubuntu:~/test$ awk '{print NR,FNR,$1,$2,$3}' log.txt
1 1 2 this is
2 2 3 Are you
3 3 This's a test
4 4 10 There are
```

#### 指定输出分割符

```txt
python@ubuntu:~/test$ cat log.txt 
2 this is a test
3 Are you like awk
This's a test
10 There are orange,apple,mongo
python@ubuntu:~/test$ awk '{print $1,$2,$5}' OFS=" $ "  log.txt
2 $ this $ test
3 $ Are $ awk
This's $ a $ 
10 $ There $ 
```

#### 忽略大小写

```txt
$ awk 'BEGIN{IGNORECASE=1} /this/' log.txt
---------------------------------------------
2 this is a test
This's a test
```

## 正则字符串匹配
#### ~ 表示模式开始。// 中是模式。

输出第二列包含 “th”，并打印第二列与第四列：

```txt
python@ubuntu:~/test$ awk '$2 ~ /th/ {print $2,$4}' log.txt
this a
```

输出包含"re"的行：

```txt
python@ubuntu:~/test$ awk '/re/' log.txt
3 Are you like awk
10 There are orange,apple,mongo
```

**!表示取反**

输出第二列不包含 “th”，并打印第二列与第四列：

```txt
python@ubuntu:~/test$ awk '$2 !~ /th/ {print $2,$4}' log.txt
Are like
a 
There orange,apple,mongo
```

输出不包含"re"的行：

```txt
python@ubuntu:~/test$ awk '!/re/' log.txt
2 this is a test
This's a test
```

## 一些实例
#### 计算文件大小

```txt
$ ls -l *.txt | awk '{sum+=$6} END {print sum}'
--------------------------------------------------
666581
```

#### 从文件中找出长度大于80的行

```txt
awk 'length>80' log.txt
```

#### 打印九九乘法表

```txt
seq 9 | sed 'H;g' | awk -v RS='' '{for(i=1;i<=NF;i++)printf("%dx%d=%d%s", i, NR, i*NR, i==NR?"\n":"\t")}'
```

#### 访问日志分析

日志格式

```txt
python@ubuntu:~/test$ head access.log -n1
42.236.10.75 "changtou.xiaoxiaoming.xyz" [14/Oct/2019:12:47:18 +0800] "GET /logo/8@3x.png HTTP/1.1" 200 26053 "https://changtou.xiaoxiaoming.xyz/" "Mozilla/5.0 (Linux; U; Android 8.1.0; zh-CN; EML-AL00 Build/HUAWEIEML-AL00) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/57.0.2987.108 baidu.sogo.uc.UCBrowser/11.9.4.974 UWS/2.13.1.48 Mobile Safari/537.36 AliApp(DingTalk/4.5.11) com.alibaba.android.rimet/10487439 Channel/227200 language/zh-CN" "42.236.10.75" rt="0.000" uct="-" uht="-" urt="-"
```

示例：

```txt
1.数据清洗
awk '($6 ~ /.html/) && ($8 ~ /200/)  {print $0}' access.log > clean.log

2.统计PV
python@ubuntu:~/test$ awk '{print $0}'  clean.log | wc -l
700
python@ubuntu:~/test$ cut -d ' ' -f 1 clean.log|wc -l    
700

3:UV
python@ubuntu:~/test$ awk '{print $1}'  clean.log |sort|uniq| wc -l
155
python@ubuntu:~/test$ cut -d ' ' -f 1 clean.log|sort|uniq| wc -l
155

4:获取每天访问网站最多的前10名用户
awk '{print $1}' clean.log|sort|uniq -c|sort -k 1nr|head
或
cut -d ' ' -f 1 clean.log|sort|uniq -c|sort -k 1nr|head
```

# awk编程
## 条件语句IF&ELSE
IF 条件语句语法格式如下：

```txt
if (condition)
    action
```

也可以使用花括号来执行一组操作：

```txt
if (condition)
{
    action-1
    action-1
    .
    .
    action-n
}
```

判断数字是奇数还是偶数：

```txt
python@ubuntu:~/test$ awk 'BEGIN {num = 10; if (num % 2 == 0) printf "%d 是偶数\n", num }'
10 是偶数
```

IF - ELSE 条件语句语法格式如下：

if (condition)
    action-1
else
    action-2
```

在条件语句 condition 为 true 时只需 action-1，否则执行 action-2。

```txt
python@ubuntu:~/test$ awk 'BEGIN {
>     num = 11; 
>     if (num % 2 == 0) printf "%d 是偶数\n", num; 
>     else printf "%d 是奇数\n", num 
> }'
11 是奇数
python@ubuntu:~/test$ awk 'BEGIN {num = 11; if (num % 2 == 0) printf "%d 是偶数\n", num; else printf "%d 是奇数\n", num }'
11 是奇数
```

可以创建多个 IF - ELSE 格式的判断语句来实现多个条件的判断：

```txt
$ awk 'BEGIN {
a=30;
if (a==10)
  print "a = 10";
else if (a == 20)
  print "a = 20";
else if (a == 30)
  print "a = 30";
}'
```

输出结果：

```txt
python@ubuntu:~/test$ awk 'BEGIN {
> a=30;
> if (a==10)
>   print "a = 10";
> else if (a == 20)
>   print "a = 20";
> else if (a == 30)
>   print "a = 30";
> }'
a = 30
```

## 循环语句For&While
For 循环的语法如下：

```txt
for (initialisation; condition; increment/decrement)
    action
```

下面的例子使用 For 循环输出数字 1 至 5：

```txt
python@ubuntu:~/test$ awk 'BEGIN { for (i = 1; i <= 5; ++i) print i }'
1
2
3
4
5
```

While 循环的语法如下：

```txt
while (condition)
    action
```

下面是使用 While 循环输出数字 1 到 5 的例子：

```txt
python@ubuntu:~/test$ awk 'BEGIN {i = 1; while (i < 6) { print i; ++i } }'
1
2
3
4
5
```

在下面的示例子中，当计算的和大于 50 的时候使用 break 结束循环：

```txt
$ awk 'BEGIN {
   sum = 0; for (i = 0; i < 20; ++i) { 
      sum += i; if (sum > 50) break; else print "Sum =", sum 
   } 
}'
```

输出结果为：

```txt
python@ubuntu:~/test$ awk 'BEGIN {
>    sum = 0; for (i = 0; i < 20; ++i) { 
>       sum += i; if (sum > 50) break; else print "Sum =", sum 
>    } 
> }'
Sum = 0
Sum = 1
Sum = 3
Sum = 6
Sum = 10
Sum = 15
Sum = 21
Sum = 28
Sum = 36
Sum = 45
```

Continue 语句用于在循环体内部结束本次循环，从而直接进入下一次循环迭代。

下面的例子输出 1 到 20 之间的偶数：

```txt
python@ubuntu:~/test$ awk 'BEGIN {for (i = 1; i <= 20; ++i) {if (i % 2 == 0) print i ; else continue} }'
2
4
6
8
10
12
14
16
18
20
```

Exit 用于结束脚本程序的执行。

该函数接受一个整数作为参数表示 AWK 进程结束状态。 如果没有提供该参数，其默认状态为 0。

下面例子中当和大于 50 时结束 AWK 程序。

```txt
$ awk 'BEGIN {
   sum = 0; for (i = 0; i < 20; ++i) {
      sum += i; if (sum > 50) exit(10); else print "Sum =", sum 
   } 
}'
```

输出结果为：

```txt
python@ubuntu:~/test$ awk 'BEGIN {
>    sum = 0; for (i = 0; i < 20; ++i) {
>       sum += i; if (sum > 50) exit(10); else print "Sum =", sum 
>    } 
> }'
Sum = 0
Sum = 1
Sum = 3
Sum = 6
Sum = 10
Sum = 15
Sum = 21
Sum = 28
Sum = 36
Sum = 45
python@ubuntu:~/test$ echo $?
10
```

## awk数组
AWK的数组底层数据结构是散列表，索引可以是数字或字符串。

数组使用的语法格式：

```txt
array_name[index]=value
```

创建数组并访问数组元素：

```txt
$ awk 'BEGIN {
sites["taobao"]="www.taobao.com";
sites["google"]="www.google.com"
print sites["taobao"] "\n" sites["google"]
}'
```

删除数组元素语法格式：

```txt
delete array_name[index]
```

下面的例子中，数组中的 google 元素被删除（删除命令没有输出）：

```txt
$ awk 'BEGIN {
sites["taobao"]="www.taobao.com";
sites["google"]="www.google.com"
delete sites["google"];
print sites["google"]
}'
```

AWK 本身不支持多维数组，不过我们可以很容易地使用一维数组模拟实现多维数组。

如下示例为一个 3x3 的三维数组：

```txt
100 200 300
400 500 600
700 800 900
```

以上实例中，array[0][0] 存储 100，array[0][1] 存储 200 ，依次类推。为了在 array[0][0] 处存储 100, 可以使用字符串0,0 作为索引： array[“0,0”] = 100。

下面是模拟二维数组的例子：

```txt
$ awk 'BEGIN {
array["0,0"] = 100;
array["0,1"] = 200;
array["0,2"] = 300;
array["1,0"] = 400;
array["1,1"] = 500;
array["1,2"] = 600;
# 输出数组元素
print "array[0,0] = " array["0,0"];
print "array[0,1] = " array["0,1"];
print "array[0,2] = " array["0,2"];
print "array[1,0] = " array["1,0"];
print "array[1,1] = " array["1,1"];
print "array[1,2] = " array["1,2"];
}'
```

执行上面的命令可以得到如下结果：

```txt
array[0,0] = 100
array[0,1] = 200
array[0,2] = 300
array[1,0] = 400
array[1,1] = 500
array[1,2] = 600
```

在数组上可以执行很多操作，比如，使用 asort 完成数组元素的排序，或者使用 asorti 实现数组索引的排序等等。

## AWK 用户自定义函数
自定义函数的语法格式为：

```txt
function function_name(argument1, argument2, ...)
{
    function body
}
```

以下实例实现了两个简单函数，它们分别返回两个数值中的最小值和最大值。

文件 functions.awk 代码如下：

```txt
# 返回最小值
function find_min(num1, num2)
{
  if (num1 < num2)
    return num1
  return num2
}

# 返回最大值
function find_max(num1, num2)
{
  if (num1 > num2)
    return num1
  return num2
}

# 主函数
function main(num1, num2)
{
  # 查找最小值
  result = find_min(10, 20)
  print "Minimum =", result

  # 查找最大值
  result = find_max(10, 20)
  print "Maximum =", result
}

# 脚本从这里开始执行
BEGIN {
  main(10, 20)
}
```

执行 functions.awk 文件，可以得到如下的结果：

```txt
$ awk -f functions.awk 
Minimum = 10
Maximum = 20
```

## AWK 内置函数
AWK 内置函数主要有以下几种：

- 算数函数
- 字符串函数
- 时间函数
- 位操作函数
- 其它函数

## 算数函数

![image](https://github.com/user-attachments/assets/5acb8fb1-8c6b-46fe-866d-d678a7841017)


## 字符串函数

![image](https://github.com/user-attachments/assets/347a5b0a-2885-43e2-90ad-d585ec438433)

**注：**Ere 部分可以是正则表达式。

#### 1、gsub、sub 使用

```txt
$ awk 'BEGIN{info="this is a test2012test!";gsub(/[0-9]+/,"||",info);print info}'
this is a test||test!
```

#### 2、查找字符串（index 使用）

使用了三元运算符: **表达式 ? 动作1 : 动作2**

```txt
$ awk 'BEGIN{info="this is a test2012test!";print index(info,"11111")?"ok":"no found";}'
no found
$ awk 'BEGIN{info="this is a test2012test!";print index(info,"is")?"ok":"no found";}'
ok
$ awk 'BEGIN{info="this is a test2012test!";print index(info,"test")?"ok":"no found";}'
ok
```

#### 3、正则表达式匹配查找(match 使用）

```txt
$ awk 'BEGIN{info="this is a test2012test!";print match(info,/[0-9]+/)?"ok":"no found";}'
ok
```

#### 4、截取字符串(substr使用）

从第 4 个 字符开始，截取 10 个长度字符串。

```txt
$ awk 'BEGIN{info="this is a test2012test!";print substr(info,4,10);}'
s is a tes
```

#### 5、字符串分割（split使用）

```txt
$ awk 'BEGIN{info="this is a test";split(info,tA," ");print length(tA);for(k in tA){print k,tA[k];}}'
4
2 is
3 a
4 test
1 this
```

分割 info，将 info 字符串使用空格切分为动态数组 tA。注意 awk for …in 循环，是一个无序的循环。 并不是从数组下标 1…n ，因此使用时候需要特别注意。

## 时间函数

![image](https://github.com/user-attachments/assets/c9f841a2-7bfc-4c7a-92ae-b6c08d0c5c14)


strftime 日期和时间格式说明符:

![image](https://github.com/user-attachments/assets/ff5bc4a6-6d91-49df-af14-35feff46d6be)


## 位操作函数

![image](https://github.com/user-attachments/assets/577be389-51e6-4d9e-b465-0ff22864b2a0)


## 其他函数

![image](https://github.com/user-attachments/assets/5ffd1207-8f70-45e9-80fb-12263ce5718b)


