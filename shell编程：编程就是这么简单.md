原文地址：https://mp.weixin.qq.com/s/cOPDTSPXAgRvoH1wU_nZCg





# shell编程：编程就是这么简单



#### Q:

什么是shell编程？



#### A:

shell编程就是通过语法将bash命令或外部命令整合起来，搭配正则表达式、管道命令与数据流定向等功能，来实现我们要完成的任务。最简单的shell script就是将多条命令写在一起，让用户可以一次性执行多条命令，同时每个命令及其输入参数得以在纯文本的shell脚本中保存。shell脚本运行较慢，使用CPU资源较多，是一个很好的项目管理工具，但一般不用于大数据处理（注：本文部分例子来自《鸟哥的Linux私房菜》）。







![图片](https://mmbiz.qpic.cn/mmbiz_jpg/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7M8yCzhcWhcT2t18VDicia7UekdeqHvv83NtdH07UNbefoIliagH8ByHzA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

## 01shell脚本基本编写规则

shell脚本基本规则如下：

①命令的执行是由上而下，自左而右，空白行会被忽略；

②空格不可省略，多个空格会被忽略；

③每读到一个[Enter]命令就开始执行，拓展下一行可以使用\[Enter]；

④命令的执行需要加绝对路径，否则默认在当前路径寻找脚本命令；

⑤通过环境变量PATH可设置脚本命令的查询范围，来简化脚本。

一个简单的shell脚本helloword如下所示：

```
#!/bin/bash#Show "Hello World!" in the screen#20170320 tengwkPATH=/opt/node/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbinexport PATHecho -e "Hello World! \n"exit 1
```

脚本一般分为四部分。其中第一行#!/bin/bash声明脚本类型（更为普遍来说是语言解释器的路径），为bash脚本，除此之外其余#后面均为注释内容；之后为脚本环境变量例如PATH和LANG设置，对于命令的执行非常重要；第三部分为主要程序执行部分，上面程序的含义是在屏幕上显示“Hello World!”，-e表示使反斜杠转义，“\n”表示换行并插入新一行；第四部分为告知执行结果，利用exit可以自定义错误信息，可以使用环境变量？查看。脚本运行如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7DIU7rnPzDpeDejXVp8YtNQQEjLF47ICkbCvQRWEibVngxAtujViaIPEQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

## 02shell脚本基本结构

shell脚本的两个基本结构就是判断结构和循环结构，判断结构使用方法如下所示：

```
if [ 判断条件 ]; then执行命令1elif [ 判断条件 ]; then执行命令2fi
```

不同判断条件之间可以通过逻辑连接符连接，接下来我们通过一个askfor help小脚本来练习：

```
#!/bin/bash#ask if you can help me# 20170330 tengwkPATH=/opt/node/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbinexport PATHread -p "Can you help me (Y/N): " answerif [ "$answer" == "Y" ] || [ "$answer" == "y" ]; then#其中 [ "$answer" == "Y" ] || [ "$answer" == "y" ]也可以改写为[ "$answer" == "Y" -o "$answer" == "y" ]echo "I'm so glad to hear that, thank you!"elif [ "$answer" == "N" ] || [ "$answer" == "n" ]; thenecho "Thank you all the same!"elseecho "Sorry, i can't understand you!"exit 1fi
```

运行示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP72maUYLxcxRcF0dAwmN894qULDuQkVIc7LoVpY0ziatqQGdYELjfArPA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

if可以使用的判断符号有：

①字符串判断

str1== str2 当两个串有相同内容、长度时为真

str1!= str2  当串str1和str2不等时为真

-nstr1     当串的长度大于0时为真(串非空)

-zstr1     当串的长度为0时为真(空串)

str1       当串str1为非空时为真

②数字的判断

int1-eq int2    两数相等为真

int1-ne int2    两数不等为真

int1-gt int2    int1大于int2为真

int1-ge int2    int1大于等于int2为真

int1-lt int2     int1小于int2为真

int1-le int2     int1小于等于int2为真

③文件的判断

-rfile  用户可读为真

-wfile  用户可写为真

-xfile  用户可执行为真

-ffile  文件为正规文件为真

-dfile  文件为目录为真

-cfile  文件为字符特殊文件为真

-bfile  文件为块特殊文件为真

-sfile  文件大小非0时为真

-tfile  当文件描述符(默认为1)指定的设备为终端时为真

④复杂逻辑判断

-a  与

-o  或

!   非

while循环结构使用方法如下：

```
while [ 条件 ] do执行命令done
```

或者更为简单的可以在命令行执行的：

```
while 条件; do 执行命令; done
```

下面是一个选择食物的selectfood脚本：

```
#!/bin/bash#to input foods you like# 20170330 tengwkPATH=/opt/node/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbinexport PATHwhile [ "$word" != "END" -a "$word" != "end" ]#或者 until [ "$word" == "END" -o "$word" == "end" ]doread -p "Please input the foods you like, and press END to stop: " worddoneecho "OK! Now i know what you want eat."
```

运行示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7g9HaswV3LOLEcRaRVmpa96uTAvIy621Sezl81byJUibnHj3UONzLcXg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

另一个更为常用的循环结构是for循环，常用来批量执行任务，如下所示：

```
for 变量名 in 单词组do  执行命令done
```

其中单词组不同单词之间空格或者换行符分隔，例如我们进入不同项目文件夹批量解压序列文件：

```
for id in `ls`do  cd $id  gzip -d raw_reads.fq.gz  cd ..done
```

## 03shell脚本命令行参数

命令行参数是程序与用户交互的重要过程，能大大提高程序脚本的适用性。前面的read命令就是一个用户与程序交互的过程。在shell脚本中，命令行参数可以直接加在脚本后面，在脚本里使用默认变量“$n”来调用（n为非负整数），下面通过一个小例子来了解shell脚本命令行参数使用方法：

```
echo $0echo $1echo $2
```

将上面脚本保存为sh04.sh并运行：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7rQ7jOnedNCYqmeTcexYzuRNPxCwTicV1yjFnia44k3JU3Wtqp1uBcFnw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出第一个变量$0为脚本名字，从$1开始为用户输入数据。当n大于10时需要添加大括号，例如${10}。

在if结构里添加参数-n可以检查命令行参数是否存在，$#可以表示参数个数，$@用来提取所有参数并构成数组，$*用来提取所有参数并构成字符串，如下所示：

```
if [ -n “$1” ]; then   echo "Arguments exist!"else   echo "No arguments"fiif [ $# -ne 2 ]; then   echo "There are $#arguments"fiecho $@
```

将上面脚本保存为sh05.sh，运行如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7zU832nkZwnrmq1OrWUvlWWfuH8CTiaCtfArSLYgENt2sK3aGO6uGiatg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

假如想设置命令行选项，可以使用getopts函数，该函数可以将命令行内容转换为变量。getopts包含两个内置变量，OPTARG和OPTIND。OPTARG就是将选项后面的参数保存在这个变量当中；OPTIND：这个表示命令行的下一个选项或参数的位置。

语法格式：getopts[option[:]] VARIABLE

getopts有两个参数，第一个参数是一个字符串，包括字符和“：”，每一个字符都是一个有效的选项，如果字符后面带有“：”，表示这个字符有自己的参数。getopts从命令中获取这些参数，并且删去了“-”，并将其赋值在第二个参数中，如果带有自己参数，这个参数赋值在“OPTARG”中。

具体实例如下所示：

```
echo $*while getopts ":a:bc" optdo     case $opt in        a ) echo $OPTARG           echo $OPTIND;;        b ) echo "b $OPTIND";;        c ) echo "c $OPTIND";;        ? ) echo "error"           exit 1;;     esacdoneecho $OPTINDshift $(($OPTIND - 1))#通过shift $(($OPTIND - 1))的处理，$*中就只保留了除去选项内容的参数，可以继续使用后面的位置参数。echo $0echo $*
```

其中":a:bc"，这就是一个选项字符串。对应到命令行就是-a ,-b ,-c。冒号又是什么呢？第一个冒号表示忽略错误，选项后面的冒号表示参数，一个冒号就表示这个选项后面必须带有参数，但是这个参数可以和选项连在一起写，也可以用空格隔开，比如-a123 和-a 123（中间有空格）都表示123是-a的参数；两个冒号的就表示这个选项的参数是可选的，即可以有参数，也可以没有参数，但要注意有参数时，参数与选项之间不能有空格。将上面脚本保存为getopts.sh。并运行如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7n6vH9l6omicTia4YiaBqb7UUzwth6richUjiadTONEFXV3Vv9eKdQwCXP0w/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/ibj9nANUc6z5gia8CDicoHTAv7EFRvicoLP7lMRaqGdIWHqAqXAw7Cud0xaNmxeQr4DTNmEEpPwUacsdHRymLYYM9Q/640?wx_fmt=gif&tp=wxpic&wxfrom=5&wx_lazy=1)

