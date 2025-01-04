原文地址：https://blog.csdn.net/weixin_38889300/article/details/129828412



# 40 个简单又有效的 Linux Shell 脚本示例



历史上，shell 一直是类 Unix 系统的本地命令行解释器。它已被证明是 Unix 的主要功能之一，并发展成为一个全新的主题。Linux 提供了各种功能强大的 shell，包括 Bash、Zsh、Tcsh 和 Ksh。这些外壳最令人惊讶的特性之一是其可编程性。创建简单而有效的 Linux shell 脚本来处理日常工作非常容易。

## 1.Hello World

程序员经常通过学习 hello world 程序来学习新语言。这是一个简单的程序，将字符串 “HelloWorld” 打印到标准输出中。然后，使用 vim 或 nano 等编辑器创建 hello-world.sh 文件，并将以下行复制到其中。

```
#!/bin/bash
echo "Hello World"
```

保存并退出文件。接下来，您需要使用以下命令使该文件可执行。

```
$ chmod a+x hello-world.sh
```

可以使用以下两个命令中的任何一个来运行此命令。

```
$ bash hello-world.sh
$ ./hello-world.sh
```

它将打印出传递给脚本内部回显的字符串。

## 2.使用 echo 打印

echo 命令用于在 bash 中打印信息。它类似于 C 函数 “printf”，并提供了许多常见选项，包括转义序列和重定向。将以下行复制到名为 echo.sh 的文件中，并使其可执行，如上所述。

```
#!/bin/bash
echo "Printing text"
echo -n "Printing text without newline"
echo -e "\nRemoving \t special \t characters\n"
```

运行脚本以查看其功能。-e 选项用于告诉 echo 传递给它的字符串包含特殊字符，需要扩展功能。

## 3.使用注释

注释对文档很有用，是高质量代码库的要求。将注释放在处理关键逻辑的代码中是一种常见的做法。要注释掉一行，只需在其前面使用 #（hash）字符。例如，请查看下面的 bash 脚本示例。

```
#!/bin/bash

# Adding two values
((sum=25+35))

#Print the result
echo $sum
```

此脚本将输出数字 60。首先，在某些行之前使用 #检查注释的使用方式。不过，第一行是一个例外。它被称为 shebang，让系统知道在运行这个脚本时要使用哪个解释器。

## 4.多行注释

许多人使用多行注释来记录他们的 shell 脚本。在下一个名为 comment.sh 的脚本中检查这是如何完成的。

```
#!/bin/bash
: '
This script calculates
the square of 5.
'
((area=5*5))
echo $area
```

注意多行注释是如何放置在内部的：“和” 字符。

## 5.While 循环

while 循环构造用于多次运行某些指令。查看以下名为 while.sh 的脚本，以更好地理解此概念。

```
#!/bin/bash
i=0

while [ $i -le 2 ]
do
echo Number: $i
((i++))
done

因此，while 循环采用以下形式。

while [ condition ]
do
commands 1
commands n
done
```

方括号周围的空格是必填的。

## 6.For 循环

for 循环是另一种广泛使用的 bashshell 构造，它允许用户高效地迭代代码。下面演示了一个简单的示例。

```
#!/bin/bash

for (( counter=1; counter<=10; counter++ ))
do
echo -n "$counter "
done

printf "\n"
```

## 7.接收用户输入

```
#!/bin/bash

echo -n "Enter Something:"
read something

echo "You Entered: $something"
```

## 8.If 语句

```
if CONDITION 
then
STATEMENTS
fi
```

只有当条件为真时，才会执行这些语句。fi 关键字用于标记 if 语句的结尾。下面显示了一个快速示例。

```
> #!/bin/bash
> echo -n "Enter a number:"
> read num
> if [[$num -gt 10]]
> then
> echo "Number is greater than 10."
> fi
```

如果通过输入提供的数字大于 10，上述程序将仅显示输出。-gt 表示大于；类似地 - lt 表示小于 - le 表示小于等于；且 - ge 表示大于等于。此外，还需要 [[]]。

## 9.使用 If Else 进行更多控制

将 else 构造与 if 结合起来，可以更好地控制脚本的逻辑。下面显示了一个简单的示例。

```
#!/bin/bash

read n
if [ $n -lt 10 ];
then
echo "It is a one digit number"
else
echo "It is a two digit number"
fi
```

其他部分需要放在 if 的动作部分之后和 fi 之前。

## 10.使用 AND 运算符

AND 运算符允许我们的程序检查是否同时满足多个条件。由 AND 运算符分隔的所有部分必须为 true。否则，包含 AND 的语句将返回 false。查看下面的 bash 脚本示例，以更好地了解 AND 的工作原理。

```
#!/bin/bash

echo -n "Enter Number:"
read num

if [[ ( $num -lt 10 ) && ( $num%2 -eq 0 ) ]]; then
echo "Even Number"
else
echo "Odd Number"
fi
```

AND 运算符由 && 符号表示。

## 11.使用 OR 运算符

OR 运算符是另一个关键的构造，它允许我们在脚本中实现复杂、健壮的编程逻辑。与 AND 相反，当 OR 运算符的任一操作数为真时，由 OR 运算符组成的语句返回真。仅当由 OR 分隔的每个操作数为假时，它才返回假。

```
#!/bin/bash

echo -n "Enter any number:"
read n

if [[ ( $n -eq 15 || $n -eq 45 ) ]]
then
echo "You won"
else
echo "You lost!"
fi
```

这个简单的示例演示了 OR 运算符如何在 Linuxshell 脚本中工作。只有当用户输入数字 15 或 45 时，它才会宣布用户为获胜者。|| 符号表示 OR 运算符。

## 12.使用 El if

elif 语句代表 else if，并为实现链逻辑提供了一种方便的方法。通过评估以下示例，了解 elif 的工作原理。

```
#!/bin/bash

echo -n "Enter a number: "
read num

if [[ $num -gt 10 ]]
then
echo "Number is greater than 10."
elif [[ $num -eq 10 ]]
then
echo "Number is equal to 10."
else
echo "Number is less than 10."
fi
```

上面的程序是不言自明的，所以我们不会逐行剖析它。相反，更改脚本中的变量名称和值等部分，以检查它们如何一起工作。

## 13.case 条件

. switch 构造是 Linux bash 脚本提供的另一个强大功能。它可以用于需要嵌套条件的地方，但不希望使用复杂的 if-else elif 链。看看下一个例子。

```
#!/bin/bash

echo -n "Enter a number: "
read num

case $num in
100)
echo "Hundred!!" ;;
200)
echo "Double Hundred!!" ;;
*)
echo "Neither 100 nor 200" ;;
esac
```

条件写在 case 和 esac 关键字之间。*）用于匹配除 100 和 200 以外的所有输入。

## 14.命令行参数

在许多情况下，直接从命令 shell 获取参数是有益的。下面的示例演示了如何在 bash 中执行此操作。

```
#!/bin/bash
echo "Total arguments : $#"
echo "First Argument = $1"
echo "Second Argument = $2"
```

运行此脚本时，在其名称后添加两个附加参数。我将其命名为 test.sh，调用过程概述如下。

```
$ ./test.sh Hey Howdy
```

因此，1、用于访问第一个参数；2、用于访问第二个参数，依此类推。最后，3、用于获取参数总数。

## 15.使用名称获取参数

下面的示例显示了如何获取带有名称的命令行参数。

```
#!/bin/bash

for arg in "$@"
do
index=$(echo $arg | cut -f1 -d=)
val=$(echo $arg | cut -f2 -d=)
case $index in
X) x=$val;;
Y) y=$val;;
*)
esac
done
((result=x+y))
echo "X+Y=$result"
```

将此脚本命名为 test.sh，并按如下所示调用它。

```
$ ./test.sh X=44 Y=100
```

它应该返回 X+Y=144。这里的参数存储在 “$@” 中，脚本使用 Linuxcut 命令获取它们。

## 16.连接字符串

字符串处理对于广泛的现代 bash 脚本来说非常重要。值得庆幸的是，它在 bash 中更加舒适，并允许以更精确、简洁的方式实现这一点。请参见下面的示例，了解 bash 字符串连接。

```
#!/bin/bash

string1="Ubuntu"
string2="Pit"
string=$string1$string2
echo "$string is a great resource for Linux beginners."
```

## 17.字符串截取

与许多编程语言不同，bash 不提供任何用于剪切字符串部分的内置函数。然而，下面的示例演示了如何使用参数展开来实现这一点。

```
#!/bin/bash
Str="Learn Bash Commands from UbuntuPit"
subStr=${Str:0:20}
echo $subStr
```

该脚本应打印出 “学习 Bash 命令” 作为其输出。参数展开形式为 ${VAR_NAME:S:L}。这里，S 表示起始位置，L 表示长度。

## 18.使用 cut 做截取

可以在脚本中使用 Linux cut 命令来截取字符串的一部分，也就是子字符串。下一个示例显示了如何做到这一点。

```
#!/bin/bash
Str="Learn Bash Commands from UbuntuPit"
#subStr=${Str:0:20}

subStr=$(echo $Str| cut -d ' ' -f 1-3)
echo $subStr
```

## 19.添加两个值

在 Linux shell 脚本中执行算术运算非常容易。下面的示例演示了如何从用户接收两个数字作为输入并将它们相加。

```
#!/bin/bash
echo -n "Enter first number:"
read x
echo -n "Enter second number:"
read y
(( sum=x+y ))
echo "The result of addition=$sum"
```

如您所见，在 bash 中添加数字相当简单。

## 20.添加多个值

您可以使用循环获取多个用户输入并将其添加到脚本中。以下示例显示了这一点。

```
#!/bin/bash
sum=0
for (( counter=1; counter<5; counter++ ))
do
echo -n "Enter Your Number:"
read n
(( sum+=n ))
#echo -n "$counter "
done
printf "\n"
echo "Result is: $sum"
```

但是，省略 (()) 将导致字符串串联而不是相加。所以，在你的程序中检查类似的情况。

## 21.Bash 中的函数

与任何编程方言一样，函数在 Linux shell 脚本中扮演着重要角色。它们允许管理员创建自定义代码块以供频繁使用。下面的演示将概述函数如何在 Linux bash 脚本中工作。

```
#!/bin/bash
function Add()
{
echo -n "Enter a Number: "
read x
echo -n "Enter another Number: "
read y
echo "Adiition is: $(( x+y ))"
}

Add
```

这里我们像以前一样添加了两个数字。但在这里，我们使用了一个名为 Add 的函数来完成这项工作。因此，每当您需要再次添加时，只需调用此函数，而不必再次编写该部分。

## 22.具有返回值的函数

最神奇的功能之一是允许数据从一个函数传递到另一个函数。它在各种场景中都很有用。查看下一个示例。

```
#!/bin/bash

function Greet() {

str="Hello $name, what brings you to UbuntuPit.com?"
echo $str
}

echo "-> what's your name?"
read name

val=$(Greet)
echo -e "-> $val"
```

这里，输出包含从 Greet（）函数接收的数据。

## 23.从 Bash 脚本创建目录

使用 shell 脚本运行系统命令的能力使开发人员的工作效率大大提高。下面的简单示例将向您展示如何在 shell 脚本中创建目录。

```
#!/bin/bash
echo -n "Enter directory name ->"
read newdir
cmd="mkdir $newdir"
eval $cmd
```

该脚本只需调用标准 shell 命令 mkdir，并在仔细查看时将目录名传递给它。这个程序应该在文件系统中创建一个目录。您还可以传递命令以在 backticks（“）内部执行，如下所示。

```
`mkdir $newdir`
```

## 24.确认存在后创建目录

如果当前工作目录中已包含同名文件夹，则上述程序将无法运行。例如，下面的程序将检查是否存在名为 $dir 的文件夹，如果找不到，则只创建一个。

```
#!/bin/bash
echo -n "Enter directory name ->"
read dir
if [ -d "$dir" ]
then
echo "Directory exists"
else
`mkdir $dir`
echo "Directory created"
fi
```

使用 eval 编写此程序以提高 bash 脚本编写技能。

## 25.读取文件

Bash 脚本允许用户非常有效地读取文件。下面的示例将展示如何使用 shell 脚本读取文件。首先，创建一个名为 editors.txt 的文件，其中包含以下内容。

```
1. Vim 
2. Emacs 
3. ed 
4. nano 
5. Code
```

此脚本将输出上述 5 行中的每一行。

```
#!/bin/bash
file='editors.txt'
while read line; do
echo $line
done < $file
```

## 26.删除文件

以下程序将演示如何在 Linux shell 脚本中删除文件。程序将首先要求用户提供文件名作为输入，如果文件名存在，则将其删除。Linux rm 命令在此处执行删除操作。

```
#!/bin/bash
echo -n "Enter filename ->"
read name
rm -i $name
```

让我们输入 editors.txt 作为文件名，并在要求确认时按 y。它应该删除该文件。

## 27.附加到文件

下面的 shell 脚本示例将向您展示如何使用 bash 脚本将数据附加到文件系统上的文件。它向早期的 editors.txt 文件添加了一行。

```
#!/bin/bash
echo "Before appending the file"
cat editors.txt
echo "6. NotePad++" >> editors.txt
echo "After appending the file"
cat editors.txt
```

现在您应该注意到，我们直接从 Linux bash 脚本使用日常终端命令。

## 28.测试文件存在

下一个 shell 脚本示例显示如何检查 bash 程序中文件的存在。

```
#!/bin/bash
filename=$1
if [ -f "$filename" ]; then
echo "File exists"
else
echo "File does not exist"
fi
```

我们直接从命令行传递文件名作为参数。

## 29.从 Shell 脚本发送邮件

从 bash 脚本发送电子邮件非常简单。下面的简单示例将演示一种从 bash 应用程序执行此操作的方法。

```
#!/bin/bash
recipient=”admin@example.com”
subject=”Greetings”
message=”Welcome to UbuntuPit”
`mail -s $subject $recipient <<< $message`
```

它将向收件人发送包含给定主题和消息的电子邮件。

## 30.解析日期和时间

下一个 bash 脚本示例将向您展示如何使用脚本处理日期和时间。同样，Linuxdate 命令用于获取必要的信息，我们的程序执行解析。

```
#!/bin/bash
year=`date +%Y`
month=`date +%m`
day=`date +%d`
hour=`date +%H`
minute=`date +%M`
second=`date +%S`
echo `date`
echo "Current Date is: $day-$month-$year"
echo "Current Time is: $hour:$minute:$second"
```

运行此程序以了解其工作原理。此外，尝试从终端运行 date 命令。

## 31.sleep 命令

sleep 命令允许 shell 脚本在指令之间暂停。它在许多场景中都很有用，例如执行系统级作业。下一个示例显示了 shell 脚本中的 sleep 命令。

```
#!/bin/bash
echo "How long to wait?"
read time
sleep $time
echo "Waited for $time seconds!"
```

该程序暂停最后一条指令的执行，直到 $time 秒，在本例中，用户提供了这一点。

## 32.wait 命令

wait 命令用于暂停 Linux bash 脚本中的系统进程。查看下面的示例，详细了解这在 bash 中的工作方式。

```
#!/bin/bash
echo "Testing wait command"
sleep 5 &
pid=$!
kill $pid
wait $pid
echo $pid was terminated.
```

## 33.显示上次更新的文件

有时，您可能需要为某些操作查找最后更新的文件。下面的简单程序向我们展示了如何在 bash 中使用 awk 命令执行此操作。它将列出当前工作目录中最近更新或创建的文件。 #!/bin/bash

```
ls -lrt | grep ^- | awk 'END{print $NF}'
```

为了简单起见，我们将避免在本示例中描述 awk 的功能。相反，您可以简单地复制此代码来完成任务。

## 34.添加批处理扩展

下面的示例将对目录中的所有文件应用自定义扩展名。创建一个新目录，并将一些文件放在其中以供演示。我的文件夹共有五个文件，每个文件名为 test，后跟（0-4）。我已将此脚本编程为在文件末尾添加（.UP）。您可以添加所需的任何扩展名。

```
#!/bin/bash
dir=$1
for file in `ls $1/*`
do
mv $file $file.UP
done
```

首先，不要从任何常规目录尝试此脚本；相反，请从测试目录运行此命令。此外，您需要提供文件的目录名作为命令行参数。对当前工作目录使用句点（.）。

## 35.打印文件或目录的数量

下面的 Linuxbash 脚本查找给定目录中存在的文件或文件夹的数量。它使用 Linux find 命令来执行此操作。首先，需要传递目录名以从命令行搜索文件。

```
#!/bin/bash

if [ -d "$@" ]; then
echo "Files found: $(find "$@" -type f | wc -l)"
echo "Folders found: $(find "$@" -type d | wc -l)"
else
echo "[ERROR] Please retry with another folder."
exit 1
fi
```

如果指定的目录不可用或存在权限问题，程序将要求用户重试。

## 36.清理日志文件

下一个简单的示例演示了在现实生活中使用 shell 脚本的简便方法。该程序只需删除 / var/log 目录中的所有日志文件。您可以更改保存此目录的变量以清理其他日志。

```
#!/bin/bash
LOG_DIR=/var/log
cd $LOG_DIR

cat /dev/null > messages
cat /dev/null > wtmp
echo "Logs cleaned up."
```

请记住以 root 身份运行此 Linuxshell 脚本。

## 37.使用 Bash 备份脚本

Shell 脚本提供了一种强大的方法来备份文件和目录。以下示例将备份过去 24 小时内修改的每个文件或目录。该程序使用 find 命令执行此操作。

```
#!/bin/bash

BACKUPFILE=backup-$(date +%m-%d-%Y)
archive=${1:-$BACKUPFILE}

find . -mtime -1 -type f -print0 | xargs -0 tar rvf "$archive.tar"
echo "Directory $PWD backed up in archive file \"$archive.tar.gz\"."
exit 0
```

备份过程成功后，它将打印文件和目录的名称。

## 38.检查你是否是 root 用户

下面的示例演示了通过 Linux bash 脚本快速确定用户是否为 root 用户的方法。

```
#!/bin/bash
ROOT_UID=0

if [ "$UID" -eq "$ROOT_UID" ]
then
echo "You are root."
else
echo "You are not root"
fi
exit 0
```

此脚本的输出取决于运行它的用户。它将根据 $UID 匹配根用户。

## 39.从文件中删除重复行

文件处理需要相当长的时间，并在许多方面阻碍了管理员的工作效率。例如，在文件中搜索重复项可能会成为一项艰巨的任务。幸运的是，您可以使用一个简短的 shell 脚本来完成此操作。

```
#! /bin/sh

echo -n "Enter Filename-> "
read filename
if [ -f "$filename" ]; then
sort $filename | uniq | tee sorted.txt
else
echo "No $filename in $pwd...try again"
fi
exit 0
```

上面的脚本逐行遍历文件并删除所有重复的行。然后，它将新内容放入新文件，并保持原始文件的完整性。

## 40.系统维护

我经常使用一个小的 Linuxshell 脚本来升级我的系统，而不是手动升级。下面的简单 shell 脚本将向您展示如何做到这一点。

```
#!/bin/bash

echo -e "\n$(date "+%d-%m-%Y --- %T") --- Starting work\n"

apt-get update
apt-get -y upgrade

apt-get -y autoremove
apt-get autoclean

echo -e "\n$(date "+%T") \t Script Terminated"
```

该脚本还处理不再需要的旧包。您需要使用 sudo 运行此脚本，否则它将无法正常工作。
