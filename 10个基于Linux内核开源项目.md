原文链接：https://mp.weixin.qq.com/s/LfUDzoriYEYcyPrvw18h0g





# 10个基于Linux内核开源项目，你了解几个？



前言：开源（Open Source，开放源码）被非盈利软件组织(美国的Open Source Initiative协会)注册为认证标记，并对其进行了正式的定义，用于描述那些源码可以被公众使用的软件，并且此软件的使用、修改和发行也不受许可证的限制。

开源项目的所有者不属于任何组织或个人。在遵守开源协议的条件下，开源产品可通过修改代码定制成属于自己的个性化产品。





## 一、Linux kernel

Linux内核是一个操作系统（OS）内核，本质上定义为类Unix。它用于不同的操作系统，主要是以不同的Linux发行版的形式。Linux内核是第一个真正完整且突出的免费和开源软件示例。Linux 内核是第一个真正完整且突出的免费和开源软件示例，促使其广泛采用并得到了数千名开发人员的贡献。

Linux 内核由芬兰赫尔辛基大学的学生 Linus Torvalds 于 1991 年创建。随着程序员调整其他自由软件项目的源代码以扩展内核的功能，它迅速取得了进展。Torvalds 首先使用 80386 汇编语言编写的任务切换器以及终端驱动程序，然后将其发布到 Comp.os.minix Usenet 组。它很快被 Mini社区所改编，为该项目提供了见解和代码。

Linux 内核越来越受欢迎，因为 GNU 自己的内核 GNU Hurd 不可用且不完整，而 Berkeley Software DistribuTIon（BSD）操作系统仍然受到法律问题的困扰。在开发人员社区的帮助下，Linux 0.01 于 1991 年 9 月 17 日发布。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOVff8tnS0xWqZVODjcoTrYicX31ViaFSlaDVJZPA9DkxHaBeAtKcuIOow/640?wx_fmt=other&wxfrom=13&tp=wxpic)

Linux最早是由芬兰 Linus Torvalds为尝试在英特尔x86架构上提供自由的类Unix操作系统而开发的。该计划开始于1991年，在计划的早期有一些 Minix 黑客提供了协助，而如今全球无数程序员正在为该计划无偿提供帮助。

### 1.1内核结构

操作系统是一个用来和硬件打交道并为用户程序提供一个有限服务集的低级支撑软件。一个计算机系统是一个硬件和软件的共生体，它们互相依赖，不可分割。计算机的硬件，含有外围设备、处理器、内存、硬盘和其他的电子设备组成计算机的发动机。但是没有软件来操作和控制它，自身是不能工作的。完成这个控制工作的软件就称为操作系统，在Linux的术语中被称为“内核”，也可以称为“核心”。Linux内核的主要模块（或组件）分以下几个部分：存储管理、CPU和进程管理、文件系统、设备管理和驱动、网络通信，以及系统的初始化（引导）、系统调用等。

结构属性

在讨论大型而复杂的系统的体系结构时，可以从很多角度来审视系统。体系结构分析的一个目标是提供一种方法更好地理解源代码。

Linux 内核实现了很多重要的体系结构属性。在或高或低的层次上，内核被划分为多个子系统。Linux 也可以看作是一个整体，因为它会将所有这些基本服务都集成到内核中。这与微内核的体系结构不同，后者会提供一些基本的服务，例如通信、I/O、内存和进程管理，更具体的服务都是插入到微内核层中的。

随着时间的流逝，Linux 内核在内存和 CPU 使用方面具有较高的效率，并且非常稳定。但是对于 Linux 来说，最为有趣的是在这种大小和复杂性的前提下，依然具有良好的可移植性。Linux 编译后可在大量处理器和具有不同体系结构约束和需求的平台上运行。一个例子是 Linux 可以在一个具有内存管理单元（MMU）的处理器上运行，也可以在那些不提供MMU的处理器上运行。Linux 内核的uClinux移植提供了对非 MMU 的支持。

开发规范

核心的开发和规范一直是由Linux社区控制着，版本也是不重复的。实际上，操作系统的内核版本指的是在Linus本人领导下的开发小组开发出的系统内核的版本号。自1994年3月14日发布了第一个正式版本Linux 1.0以来，每隔一段时间就有新的版本或其修订版公布。

Linux将标准的GNU许可协议改称Copyleft，以便与Copyright相对照。通用的公共许可（GPL）允许用户销售、拷贝和改变具有Copyleft的应用程序。当然这些程序也可以是Copyright的，但是你必须允许进一步的销售、拷贝和对其代码进行改变，同时也必须使他人可以免费得到修改后的源代码。事实证明，GPL对于Linux的成功起到了极大的作用。它启动了一个十分繁荣的商用Linux阶段，还为编程人员提供了一种凝聚力，诱使大家加入这个充满了慈善精神的Linux运动。

### 1.2主要子系统

系统调用接口

SCI 层提供了某些机制执行从用户空间到内核的函数调用。正如前面讨论的一样，这个接口依赖于体系结构，甚至在相同的处理器家族内也是如此。SCI 实际上是一个非常有用的函数调用多路复用和多路分解服务。在 ./linux/kernel 中您可以找到 SCI 的实现，并在 ./linux/arch 中找到依赖于体系结构的部分。

进程管理

进程管理的重点是进程的执行。在内核中，这些进程称为线程，代表了单独的处理器虚拟化（线程代码、数据、堆栈和 CPU寄存器）。在用户空间，通常使用进程 这个术语，不过 Linux 实现并没有区分这两个概念（进程和线程）。内核通过 SCI 提供了一个应用程序编程接口（API）来创建一个新进程（fork、exec 或 Portable Operating System Interface [POSⅨ] 函数），停止进程（kill、exit），并在它们之间进行通信和同步（signal 或者 POSⅨ 机制）。

进程管理还包括处理活动进程之间共享 CPU 的需求。内核实现了一种新型的调度算法，不管有多少个线程在竞争 CPU，这种算法都可以在固定时间内进行操作。这种算法就称为 O⑴ 调度程序，这个名字就表示它调度多个线程所使用的时间和调度一个线程所使用的时间是相同的。O⑴ 调度程序也可以支持多处理器（称为对称多处理器或 SMP）。您可以在 ./linux/kernel 中找到进程管理的源代码，在 ./linux/arch 中可以找到依赖于体系结构的源代码。

内存管理

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfO58nyUOFGp1FlYRiaPFLfbLGwHrsepLV5Ezib5NRB5cjL1C38L2sjghxA/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

VFS 在用户和文件系统之间提供了一个交换层，内核所管理的另外一个重要资源是内存。为了提高效率，如果由硬管理虚拟内存，内存是按照所谓的内存页 方式进行管理的（对于大部分体系结构来说都是 4KB）。Linux 包括了管理可用内存的方式，以及物理和虚拟映射所使用的硬件机制。

不过内存管理要管理的可不止 4KB缓冲区。Linux 提供了对 4KB缓冲区的抽象，例如 slab分配器。这种内存管理模式使用 4KB缓冲区为基数，然后从中分配结构，并跟踪内存页使用情况，比如哪些内存页是满的，哪些页面没有完全使用，哪些页面为空。这样就允许该模式根据系统需要来动态调整内存使用。

为了支持多个用户使用内存，有时会出现可用内存被消耗光的情况。由于这个原因，页面可以移出内存并放入磁盘中。这个过程称为交换，因为页面会被从内存交换到硬盘上。内存管理的源代码可以在 ./linux/mm 中找到。

虚拟文件系统

虚拟文件系统（VFS）是 Linux 内核中非常有用的一个方面，因为它为文件系统提供了一个通用的接口抽象。VFS 在 SCI 和内核所支持的文件系统之间提供了一个交换层。

VFS 在用户和文件系统之间提供了一个交换层，在 VFS 上面，是对诸如 open、close、read 和 write 之类的函数的一个通用 API 抽象。在 VFS 下面是文件系统抽象，它定义了上层函数的实现方式。它们是给定文件系统（超过 50 个）的插件。文件系统的源代码可以在 ./linux/fs 中找到。

文件系统层之下是缓冲区缓存，它为文件系统层提供了一个通用函数集（与具体文件系统无关）。这个缓存层通过将数据保留一段时间（或者随即预先读取数据以便在需要是就可用）优化了对物理设备的访问。缓冲区缓存之下是设备驱动程序，它实现了特定物理设备的接口。

## 二、Bash命令行解释器

Bash是一种Unix/Linux操作系统的命令行解释器(shell)，也是Linux系统中默认的shell。Bash提供了一个命令行界面，用户可以在其中输入各种命令，并与计算机交互。通过Bash，用户可以使用各种工具来管理文件和目录、编辑文本文件、启动程序等等。

同时，Bash还支持脚本编程，可以编写各种自动化脚本来完成一些任务。这是一个开源 GNU 项目。它提供了比 Bourne Shell 更好的功能，适用于编程和交互使用。 我们可以这么理解，Bash 是一个命令处理器，通常运行于文本窗口中，可以将用户输入的命令解释并执行相应的操作，这样式的文件被称作脚本。 Bash 是绝大多数 Linux 、MAC 及 OS 默认的 shell 程序，并且 Shell Script 都大致相同。当您学会一种 Shell 后，其它的 Shell 都能够很快上手，而且一种 Shell Script 通常可以在很多 Shell 上使用，因此您不必在学习哪种 Shell 的选择上耗费太多的时间。

Bash是一个命令处理器，通常运行于文本窗口中，并能执行用户直接输入的命令。Bash还能从文件中读取命令，这样的文件称为脚本。和其他Unix shell 一样，它支持文件名替换（通配符匹配）、管道、here文档、命令替换、变量，以及条件判断和循环遍历的结构控制语句。包括关键字、语法在内的基本特性全部是从sh借鉴过来的。其他特性，例如历史命令，是从csh和ksh借鉴而来。总的来说，Bash虽然是一个满足POSIX规范的shell，但有很多扩展。

### 2.1语法与特性

bash的命令语法是Bourne shell命令语法的超集。数量庞大的Bourne shell脚本大多不经修改即可以在bash中执行，只有那些引用了Bourne特殊变量或使用了Bourne的内置命令的脚本才需要修改。bash的命令语法很多来自Korn shell（ksh）和C shell（csh），例如命令行编辑，命令历史，目录栈，$RANDOM和$PPID变量，以及POSIX的命令置换语法：$(...)。作为一个交互式的shell，按下TAB键即可自动补全已部分输入的程序名，文件名，变量名等等。

使用'function'关键字时，Bash的函数声明与Bourne/Korn/POSIX脚本不兼容（Korn shell 有同样的问题）。不过Bash也接受Bourne/Korn/POSIX的函数声明语法。因为许多不同，Bash脚本很少能在Bourne或Korn解释器中运行，除非编写脚本时刻意保持兼容性。然而，随着Linux的普及，这种方式正变得越来越少。不过在POSIX模式下，Bash更加符合POSIX。bash的语法针对Bourne shell的不足做了很多扩展。其中的一些列举在这里。

花括号扩展

花括号扩展是一个从C shell借鉴而来的特性，它产生一系列指定的字符串（按照原先从左到右的顺序）。这些字符串不需要是已经存在的文件。

```
$ echo a{p,c,d,b}eape ace ade abe$ echo {a,b,c}{d,e,f}ad ae af bd be bf cd ce cf
```

花括号扩展不应该被用在可移植的shell脚本中，因为Bourne shell产生的结果不同。

```
#! /bin/sh
# 传统的shell并不产生相同结果echo a{p,c,d,b}e 
# a{p,c,d,b}e
```

当花括号扩展和通配符一起使用时，花括号扩展首先被解析，然后正常解析通配符。因此，可以用这种方法获得当前目录的一系列JPEG和PEG文件。

```
ls *.{jpg,jpeg,png}    # 首先扩展为*.jpg *.jpeg *.png，然后解析通配符
echo *.{png,jp{e,}g}   # echo显示扩展结果；花括号扩展可以嵌套。
```

除了列举备选项，还可以用“..”在花括号扩展中指定字符或数字范围。较新的Bash版本接受一个整数作为第三个参数，指定增量。

```
$ echo {1..10}1 2 3 4 5 6 7 8 9 10
$ echo file{1..4}.txtfile1.txt file2.txt file3.txt file4.txt$ echo {a..e}a b c d e$ echo {1..10..3}1 4 7 10
$ echo {a..j..3}a d g j
```

当花括号扩展和变量扩展一起使用时，变量扩展解析于花括号扩展之后。有时有必要使用内置的eval函数。

```
$ start=1; end=10
$ echo {$start..$end}  # 由于解析顺序，无法得到想要的结果
{1..10}
$ eval echo {$start..$end} # 首先进行变量扩展的解析
1 2 3 4 5 6 7 8 9 10
```

使用整数

与Bourne shell不同的是bash不用另外生成进程即能进行整数运算。bash使用((...))命令和$[...]变量语法来达到这个目的：

```
VAR=55             
# 将整数55赋值给变量VAR ((VAR = VAR + 1))  
# 变量VAR加1。注意这里没有'$' ((++VAR))          
# 另一种方法给VAR加1。使用C语言风格的前缀自增 ((VAR++))          
# 另一种方法给VAR加1。使用C语言风格的后缀自增 echo $((VAR * 22)) 
# VAR乘以22并将结果送入命令 echo $[VAR * 22]   # 同上，但为过时用法
```

((...))命令可以用于条件语句，因为它的退出状态是0或者非0（大多数情况下是1），可以用于是与非的条件判断：

```
if((VAR == Y * 3 + X * 2)) then         echo Yes fi ((Z > 23)) && echo Yes 
```

((...))命令支持下列比较操作符：'==', '!=', '>', '<', '>='，和'<='。bash不能在自身进程内进行浮点数运算。当前有这个能力的unix shell只有Korn shell和Z shell。

输入输出重定向

bash拥有传统Bourne shell缺乏的I/O重定向语法。bash可以同时重定向标准输出和标准错误，这需要使用下面的语法：

```
command &> file
```

这比等价的Bourne shell语法"command > file 2>&1"来的简单。2.05b版本以后，bash可以用下列语法重定向标准输入至字符串（称为here string）：

```
command <<< "string to be read as standard input"
```

如果字符串包括空格就需要用引号包裹字符串。

例子: 重定向标准输出至文件，写数据，关闭文件，重置标准输出。

```
# 生成标准输出（文件描述符1）的拷贝文件描述符6 exec 6>&1 
# 打开文件"test.data"以供写入 exec 1>test.data 
# 产生一些内容 echo "data:data:data" 
# 关闭文件"test.data" exec 1>&- 
# 使标准输出指向FD 6（重置标准输出） exec 1>&6 
# 关闭FD6 exec 6>&-
```

打开及关闭文件

```
# 打开文件test.data以供读取 exec 6<test.data 
# 读文件直到文件尾 while read -u 6 dta do   echo "$dta" done 
# 关闭文件test.data exec 6<&-
```

抓取外部命令的输出

```
# 运行'find'并且将结果存于VAR  # 搜索以"h"结尾的文件名  VAR=$(find . -name "*h")
```

进程内的正则表达式

bash 3.0支持进程内的正则表达式，使用下面的语法：

```
[[ string =~ regex ]]
```

正则表达式语法同regex(7)man page所描述的一致。正则表达式匹配字符串时上述命令的退出状态为0，不匹配为1。正则表达式中用圆括号括起的子表达式可以访问shell变量BASH_REMATCH，如下：

```
if [[ abcfoobarbletch =~ 'foo(bar)bl(.*)' ]] then         echo The regex matches!
         echo $BASH_REMATCH      -- outputs: foobarbletch
         echo ${BASH_REMATCH[1]} -- outputs: bar        
         echo ${BASH_REMATCH[2]} -- outputs: etch 
 fi
```

使用这个语法的性能要比生成一个新的进程来运行grep命令优越，因为正则表达式匹配在bash进程内完成。如果正则表达式或者字符串包括空格或者shell关键字，（诸如'*'或者'?'），就需要用引号包裹。Bash 4 开始的版本已经不需要这么做了。

转义字符

$'string'形式的字符串会被特殊处理。字符串会被展开成string，并像C语言那样将反斜杠及紧跟的字符进行替换。反斜杠转义序列的转换方式如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOFG3cSGmhceZZcfL6m2rS0uGOXwdfpN2oAYpwDPXbSibo3rLHAyUia4kg/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

扩展后的结果将被单引号包裹，就好像美元符号一直就不存在一样。双引号包裹的字符串前若有一个美元符号（$"..."）将会使得字符串被翻译成符合当前locale的语言。如果当前locale是C或者POSIX，美元符号会被忽略。如果字符串被翻译并替换，替换后的字符串仍被双引号包裹。

### 2.2Shell的用途

Shell：UNIX Shell是一种程序或命令行解释程序，用于解释用户直接输入的用户命令或从文件中读取的用户命令(即，Shall Script)，然后将它们传递给操作系统以进行操作或处理。要注意，这个过程是解释而不编译脚本，因为计算机系统会解释它们，并且无需按执行顺序编译Shell脚本。

Linux操作系统中有不同类型的Shell，其中一些如下：

- Bourne Shell
- C shell
- Korn Shell
- GNU Bourne Shell

要想知道操作系统支持哪种Shell类型，可在终端中输入以下命令：

```
cat /etc/shells
```

要想知道bash在操作系统中的位置，可键入以下命令，将获得一个特定的位置：

```
which bash
```

下面是查看Ubutu支持的Shell类型以及其bash shell所在位置的示例：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfONJIdG2p4ExsRiawu1bWwhAm90gathgmbRyeCFqBiaic2Q62jWl03Cg0dw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

bash的优势

- 通过上下方向键来调取过往执行过得Linux命令
- 命令或参数仅需要输入前几位就可以用Tab键补全
- 具有强大的批处理脚本
- 具有实用的环境变量功能

### 2.3bash的使用

如图，bash可以从标准输入或者文件中读取命令。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOibX7EmvXDjJPu0XaAD33IdgYxLlJONAia8FBKvld7P2e4N1vwzGa32sA/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

\1. 标准输入读取命令

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOyF78snfzySWtgo8pibiaIK4evqAMIc6jLnBlLtDVjMAFMfhFWo3EfgrQ/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

如图bash是可以嵌套的。当我们打一个exit就会退出一个bash。多打一个exit的话便会退出SSH连接。

\2. 从文件中读取命令

创建sh01.sh文件，输入如下内容：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOOtRFbPHlDZgBQjtCE47UsCloZc7OzQ3hGKiczGIia39GHJBXIk5aaVuw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

我们使用source命令来执行我们的sh文件，source是内部命令，具体含义如下：“在当前shell执行文件中的命令”.什么是当前shell？我们说过bash是可以嵌套的。不同的bash执行相同的命令，可能结果不同（比如 echo $$ 来输出当前进程号），所有当前shell就是指的现在所在层的bash。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOKchxjkVbSHClTAia7Wjic9L4ibbGKZmabgEXMe7tCESbrEQsvhNJt5p0A/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

执行结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOlfc2YrPltPSHtMYXdOU8h0N3Nib8MXejTICriaIC6xiaibUIpb5cg9CImg/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

与source命令相同.也表示在当前shell执行文件内的命令：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOf2XPMc7mp8uicSYsJVia0g3RjCrtYjL6OI4WHvDdH3LaUEP91OOvOjcg/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

### 2.4bash的层级关系

bash具有层级关系，我们可以通过pstree命令来查看bash的层级关系，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOlficy9htGU9LQzmBfPh10ccKTQ230ibhib95K4UY0LOD3zdQbiaINgHYZA/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

系统进入默认是第一层bash【1235】，当我们再键入一个bash命令就会嵌套一层bash，依次类推，才有了我们进程号为1798、1805的bash。

思考：既然bash是一个命令，那么我么是否可以bash执行文件内容呢？

当然可以。但是又会嵌套一层bash，具体如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOxJ9dfibia9LWDRrTY6C3N5rlA9J1eQXBmfRGrBUX8z228MvCuB2g4ibxQ/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

但是我们执行pstree命令却发现为什么只有最外面一层默认的父bash，而没有执行sh01.sh文件的子bash呢？

显然这个过程是先开启bash然后执行完毕后再退出bash。

## 三、Vim文本编辑器

Vim是一款强大的文本编辑器，也是Linux系统下最常用的编辑器之一。它可以运行在多种操作系统平台上，并支持多种文件格式和编程语言。

Vim具有很多特性，如分屏、富文本格式、插件等等，使其非常适合程序员开发工作和日常使用。

它的优点包括：

- 可定制性高：用户可以自定义快捷键、配置文件等。
- 命令模式和插入模式切换方便：可以随时在命令模式和插入模式之间进行切换。
- 强大的搜索功能：支持正则表达式和全局搜索。
- 多种操作方式：支持单个字符、行或整个文档进行复制、剪切、粘贴等操作。

由于Vim使用起来需要一些时间去学习掌握，但一旦熟练掌握后将会显著提高编辑效率。

### 3.1使用技巧

```
vim - Vi IMproved, a programmers text editor
       vim [options] [file ..]
       vim [options] -
       vim [options] -t tag
       vim [options] -q [errorfile]
```

1）+#: 打开文件后，直接让光标处于第#行的行首

```
如：vim +20 file 
```

2）+/PATTERN：打开文件后，直接让光标处于第一个被pattren匹配的到的行的字符所在位置

3）vim –d file1 file2… 比较多个文件

```
example:vim -d test.sh test.txt 类似命令有:vimdiff test.sh test.txt 
```

vim的三大模式：

- 1）命令模式
- 2）插入模式
- 3）末行模式

Esc键可以切换模式，Esc键退出当前模式，Esc键 Esc键总是返回到命令模式

### 3.2VIM插件管理利器－vundle

安装配置vundle

第一步，创建ＶＩＭ的目录和配置文件：

在～目录下，添加.vimrc文件和.vim/bundle/vundle目录．

第二步，在.vimrc中添加Ｖｕｎｄｌｅ的配置内容：

```
"use vundle to manage plugin
filetype off
set nocompatible
set rtp+=~/.vim/bundle/vundle
call vundle#rc()
```

注：最好是将这部分内容放到此配置文件的最前面　

安装插件：

打开ＶＩＭ，在命令模式下执行　

```
:BundleInstall
```

等等一会儿就自动安装完成了．

添加插件操作

这个vundle可以自动去相应的官方去查找相应的制作，自动下载，例如，要使用tagbar，则在.vimrc添加

```
Bundle "majutsushi/tagbar" 
```

然后同样在命令模式下执行下面命令即可自动安装了：

```
:BundleInstall
```

常见插件参考：

```
" Syntax
Bundle 'asciidoc.vim'
Bundle 'confluencewiki.vim'
Bundle 'html5.vim'
Bundle 'JavaScript-syntax'
"Bundle 'mako.vim'
Bundle 'moin.vim'
Bundle 'python.vim--Vasiliev'
Bundle 'xml.vim'
 
" Color
 
Bundle 'desert256.vim'
Bundle 'Impact'

Bundle 'vibrantink'
Bundle 'vividchalk.vim'
 
" Ftplugin
Bundle 'python_fold'
 
" Indent
"Bundle 'indent/html.vim'
Bundle 'IndentAnything'
Bundle 'Javascript-Indentation'
Bundle 'mako.vim--Torborg'
Bundle 'gg/python.vim'
 
" Plugin
Bundle 'The-NERD-tree'
Bundle 'AutoClose--Alves'
Bundle 'auto_mkdir'
Bundle 'cecutil'
Bundle 'fcitx.vim'
Bundle 'FencView.vim'
"Bundle 'FuzzyFinder'
Bundle 'jsbeautify'
Bundle 'L9'
Bundle 'Mark'
Bundle 'matrix.vim'
Bundle 'mru.vim'
Bundle 'The-NERD-Commenter'
"Bundle 'project.vim'
Bundle 'restart.vim'
Bundle 'taglist.vim'
"Bundle 'templates.vim'
"Bundle 'vimim.vim'
Bundle 'ZenCoding.vim'
Bundle 'css_color.vim'
Bundle 'hallettj/jslint.vim'
```

### 3.2VIM使用

浏览内核源代码

为了实现类似SourceInsight功能，通过VIM+Ctags+Cscope+Taglist＋Source Explore +NERD Tree实现．

安装插件

１）安装Ctags 和Cscope

Ubuntu下可以直接通过命令安装：

```
sudo apt-get install ctags cscope
```

注：cscope与ctags功能类似，但能补充Ctags的不足，二者结合便能兼具ctags的便利，双能用cscope补充ctags的局限，算得上是Linux内核代码分析的强大工具。

２）安装taglist :

通过向.vimrc中添加：

```
Bundle 'taglist.vim'
Bundle "scrooloose/nerdtree" 
Bundle "wesleyche/SrcExpl" 
Bundle "majutsushi/tagbar"
```

3)再执行:BundleInstall命令即可自动安装

配置和使用插件

在Linux内核已经自带ctags和cscope的标签数据库的生成脚本，在内核源代码目录下通过命令可生成相应的数据库文件：

```
make ctags
make cscope
```

注：前者，生成一个92M的tags文件，后者会生成cscope.files(分析文件的目录）和其它文件数据库．

配置ctags和cscope的数据库与ＶＩＭ联动:

```
""" ctags database path """""""
set tags=/home/magc/workspace/linux-2.6.32.67/tags


""" cscope database path """""""
set csprg=/usr/bin/cscope    "whereis cscope
set csto=0            "cscope DB search first
set cst                "cscope db tag DB search
set nocsverb            "verbose off
"cs db path
cs add /home/magc/workspace/linux-2.6.32.67/cscope.out
set csverb            "verbos off
```

taglist插件配置：

```
""""""""tag list setting """"""""
filetype on
nmap <F7> :TlistToggle<CR>        "F7 Key = Tag list Toggling
let Tlist_Ctags_Cmd = "/usr/bin/ctags"    " whereis ctags
let Tlist_Inc_WinWidth = 0        "window width change off"
let Tlist_Exit_OnlyWindow = 0        
let Tlist_Auto_Open = 0            "VIM打开时
let Tlist_Use_Right_Window = 1
```

Source Explorer 插件配置：

```
""""""" Source Explorer Setting """"""


nmap <F4> :SrcExplToggle<CR>
 "control+h进入左边的窗口
nmap <C-H> <C-W>h
 "control+j进入下边的窗口
nmap <C-J> <C-W>j 
"control+k进入上边的窗口
nmap <C-K> <C-W>k 
"control+l进入右边的窗口
nmap <C-L> <C-W>l  

let g:Srcexpl_winHeight = 8

" // Set 100 ms for refreshing the Source Explorer 

let g:SrcExpl_refreshTime = 100

" // Set "Enter" key to jump into the exact definition context 

let g:SrcExpl_jumpKey = "<ENTER>"

" // Set "Space" key for back  the definition context 

let g:SrcExpl_gobackKey = "<SPACE>"
let g:SrcExpl_isUpdateTags = 0
```

NERD Tree插件配置：

```
""""" NERD Tree Setting """""""""
let NERDTreeWinPos="left"
nnoremap <F2> :NERDTreeToggle<CR>
```

注：上面设置中包含的快捷键有：

- F7打开Taglist
- F4打开Source Explorer
- F2打开Nerd Tree
- control+h进入左边的窗口
- control+k进入上边的窗口
- control+j进入下边的窗口
- control+l进入右边的窗口

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfO2o4vpeh5G9EZlA6XxCQoibLBfyZYbLjqQ2zTLPibUqB2zrQLY3iadQCoQ/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

代码浏览方法

类似SourceInsight的用法，只不过这里有些窗口需要手动打开，通过F2,F4,F7打开如上图的，先在左侧的ＮＥＲＤ文件树中找到你要查看的文件，中间大窗口是源码窗口，当光标在某变量或函数名上时，下面就会显示它的定义，右侧是当前文件的标签（变量，函数名等）注：这里标签的来源是cscope和ctags两个数据库。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfO93mE61rZcQ9oL6tojEicsKMSxINRejAIXF5vicaVfv8sAwYm8W58slyw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

## 四、GCC编译器集合

### 4.1简述

GCC（GNU Compiler Collection）是一套由自由软件基金会发布的编译器集合，可以编译多种编程语言的程序，如C、C++、Objective-C、Fortran、Ada等。GCC是自由软件的代表之一，许多自由操作系统都采用了GCC作为默认的编译器。

GCC具有以下特点：

1. 跨平台支持：GCC可在多个操作系统上使用，如Linux、Unix、Windows等。
2. 编译器集合：包含了多种编程语言的编译器，可以满足不同领域和需求的开发者。
3. 开源免费：完全开源，并且提供免费下载和使用。
4. 高度优化：能够对生成的代码进行高度优化，以达到更好的性能和效率。
5. 丰富的选项：提供大量参数选项来控制编译过程中的行为，可以调整生成代码质量和性能表现。

（1）基本用法

在使用Gcc 编译器的时候，我们必须给出一系列必要的调用参数和文件名称。GCC 编译器的调用参数大约有100多个，其中多数参数我们可能根本就用不到，这里只介绍其中最基本、最常用的参数。

GCC最基本的用法是∶gcc [options] [filenames]

其中options就是 编译器所需要的参数，filenames给出相关的文件名称。

- -c，只 编译，不链接成为 可执行文件， 编译器只是由输入的.c等 源代码文件生成.o为后缀的目标文件，通常用于编译不包含主程序的 子程序文件。
- -o output_filename，确定输出文件的名称为output_filename，同时这个名称不能和源文件同名。如果不给出这个选项，gcc就给出预设的 可执行文件a.out。
- -g，产生符号调试工具(GNU的gdb)所必要的符号资讯，要想对 源代码进行调试，我们就必须加入这个选项。
- -O，对程序进行优化 编译、链接，采用这个选项，整个 源代码会在编译、链接过程中进行优化处理，这样产生的 可执行文件的执行效率可以提高，但是，编译、链接的速度就相应地要慢一些。
- -O2，比-O更好的优化 编译、链接，当然整个编译、链接过程会更慢。
- -Idirname，将dirname所指出的目录加入到程序头文件目录列表中，是在 预编译过程中使用的参数。

C程序中的头文件包含两种情况∶

- A)#include <myinc.h>
- B)#include “myinc.h”

其中，A类使用尖括号(< >)，B类使用双引号(“ ”)。对于A类， 预处理程序cpp在系统预设包含 文件目录(如/usr/include)中搜寻相应的文件，而B类，预处理程序在 目标文件的文件夹内搜索相应文件。

（2）基本规则

gcc所遵循的部分约定规则：

- .c为后缀的文件，C语言 源代码文件；
- .a为后缀的文件，是由 目标文件构成的档案库文件；
- .C，.cc或.cxx 为后缀的文件，是C++ 源代码文件且必须要经过 预处理；
- .h为后缀的文件，是程序所包含的头文件；
- .i 为后缀的文件，是C 源代码文件且不应该对其执行 预处理；
- .ii为后缀的文件，是C++ 源代码文件且不应该对其执行 预处理；
- .m为后缀的文件，是Objective-C 源代码文件；
- .o为后缀的文件，是 编译后的 目标文件；
- .s为后缀的文件，是 汇编语言 源代码文件；
- .S为后缀的文件，是经过 预编译的 汇编语言 源代码文件。

（3）执行过程

虽然我们称Gcc是C语言的 编译器，但使用gcc由C语言 源代码文件生成 可执行文件的过程不仅仅是编译的过程，而是要经历四个相互关联的步骤∶ 预处理(也称 预编译，Preprocessing)、 编译(Compilation)、 汇编(Assembly)和 链接(Linking)。

命令gcc首先调用cpp进行 预处理，在预处理过程中，对 源代码文件中的文件包含(include)、 预编译语句(如 宏定义define等)进行分析。接着调用cc1进行 编译，这个阶段根据输入文件生成以.o为后缀的目标文件。 汇编过程是针对汇编语言的步骤，调用as进行工作，一般来讲，.S为后缀的汇编语言 源代码文件和汇编、.s为后缀的汇编语言文件经过 预编译和汇编之后都生成以.o为后缀的目标文件。当所有的 目标文件都生成之后，gcc就调用ld来完成最后的关键性工作，这个阶段就是连接。在连接阶段，所有的 目标文件被安排在可执行程序中的恰当的位置，同时，该程序所调用到的 库函数也从各自所在的档案库中连到合适的地方。

### 4.2GCC的组成部分

GCC 是由许多组件组成的。表 1 列出了 GCC 的各个部分，但它们也并不总是出现 的。有些部分是和语言相关的，所以如果没有安装某种特定语言，系统:中就不会出现相关的文件。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOcPX7oeUnzQ97dVKTOFsN9auGIt4FDKcBNe0ialkJkJj0rgzibQnv6Tzg/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

表1：GCC 安装的各个部分

表2列出的软件和 GCC 协同工作，目的是实现编译过程。有些是很基本的（例如 as 和 Id），而其他一些则是非常有用但不是严格需要的。尽管这些工具中的很多都是各种 UNIX 系统的本地工具，但还是能够通过 GNU 包 binutils 得到大多数工具。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfO3Hew09PibSy8W4wmtgfy4twJzSeBppS5m13mKqk0UAkKicUUt2ud0sfg/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

表2：GCC 使用的软件工具

### 4.3GCC 、gcc和g++的区别

GCC:GNU Compiler Collection(GUN 编译器集合)，它可以编译C、C++、JAV、Fortran、Pascal、Object-C、Ada等语言。

gcc是GCC中的GUN C Compiler（C 编译器）

g++是GCC中的GUN C++ Compiler（C++编译器）

就本质而言，gcc和g++并不是编译器，也不是编译器的集合，它们只是一种驱动器，根据参数中要编译的文件的类型，调用对应的GUN编译器而已，比如，用gcc编译一个c文件的话，会有以下几个步骤：

- Step1：Call a preprocessor, like cpp.
- Step2：Call an actual compiler, like cc or cc1.
- Step3：Call an assembler, like as.
- Step4：Call a linker, like ld

由于编译器是可以更换的，所以gcc不仅仅可以编译C文件

所以，更准确的说法是：gcc默认调用了C compiler，而g++默认调用了C++ compiler。

实际使用中我们更习惯使用 gcc 指令编译 C 语言程序，用 g++ 指令编译 C++ 代码。需要强调的一点是，这并不是 gcc 和 g++ 的区别，gcc 指令也可以用来编译 C++ 程序，同样 g++ 指令也可以用于编译 C 语言程序。

实际上，只要是 GCC 支持编译的程序代码，都可以使用 gcc 命令完成编译。可以这样理解，gcc 是 GCC 编译器的通用编译指令，因为根据程序文件的后缀名，gcc 指令可以自行判断出当前程序所用编程语言的类别，比如：

- xxx.c：默认以编译 C 语言程序的方式编译此文件；
- xxx.cpp：默认以编译 C++ 程序的方式编译此文件。
- xxx.m：默认以编译 Objective-C 程序的方式编译此文件；
- xxx.go：默认以编译 Go 语言程序的方式编译此文件；

当然，gcc 指令也为用户提供了“手动指定代表编译方式”的接口，即使用 -x 选项。例如，gcc -xc xxx 表示以编译 C 语言代码的方式编译 xxx 文件；而 gcc -xc++ xxx 则表示以编译 C++ 代码的方式编译 xxx 文件。

但如果使用 g++ 指令，则无论目标文件的后缀名是什么，该指令都一律按照编译 C++ 代码的方式编译该文件。也就是说，对于 .c 文件来说，gcc 指令以 C 语言代码对待，而 g++ 指令会以 C++ 代码对待。但对于 .cpp 文件来说，gcc 和 g++ 都会以 C++ 代码的方式编译。

有读者可能会认为，C++ 兼容 C 语言，因此对于 C 语言程序来说，使用 gcc 编译还是使用 g++ 编译，应该没有什么区别，事实并非如此。严格来说，C++ 标准和 C 语言标准的语法要求是有区别的。举个例子：

```
#include <stdio.h>
int main()
{
    const char * a = "abc";
    printStr(a);
    return;
}
int printStr(const char* str)
{
    printf(str);
}
```

如上所示，这是一段不规范的 C 语言代码。如果我们使用 gcc 指令编译，如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOj0mWI265hzRu6XibALF31esrdQYy1ic4mUoyJhpcwj3a8XMzZou2cppg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，该指令的执行过程并没有发生任何错误。而同样的程序，如果我们使用 g++ 指令编译，可以看到，GCC 编译器发现了 3 处错误。显然，C++ 标准对代码书写规范的要求更加严格。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOG5pKVFxe7UOEBvjUxPdIHBaa7zSQarJB7tyWnwiaZMvFlZkvsCyaZQw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

除此之外对于编译执行 C++ 程序，使用 gcc 和 g++ 也是有区别的。要知道，很多 C++ 程序都会调用某些标准库中现有的函数或者类对象，而单纯的 gcc 命令是无法自动链接这些标准库文件的。举个例子：

```
#include <iostream>
#include <string>
using namespace std;
int main(){
    string str ="C语言中文网";
    cout << str << endl;
    return 0;
}
```

这是一段很简单的 C++ 程序，其通过 <string> 头文件提供的 string 字符串类定义了一个字符串对象，随后使用 cout 输出流对象将其输出。对于这段 C++ 代码，如果我们使用 g++ 指令编译，如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOqJjS5icVAsA4RBKMoQicjfObjndsWuOrNI2nT2OdYUSAGxwSZ6sAtLfQ/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，使用g++可以正常编译，但使用gcc无法正常编译。其根本原因就在于，该程序中使用了标准库 <iostream> 和<string> 提供的类对象，而 gcc 默认是无法找到它们的。如果想使用 gcc 指令来编译执行 C++ 程序，需要在使用 gcc 指令时，手动为其添加 -lstdc++ -shared-libgcc 选项，表示 gcc 在编译 C++ 程序时可以链接必要的 C++ 标准库。也就是说，我们可以这样编译 demo.cpp 文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOeIe76eEjpblwfBVeCWtM7FX1icVkxUic5B5kIhT9ic1gU3wgxGYllTvXg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

显然通过gcc来编译书写起来更加麻烦，于 C 语言程序的编译，我们应该使用 gcc 指令，而编译 C++ 程序则推荐使用 g++ 指令，这就足够了。

### 4.4GCC自动识别扩展名

通过前面的学习我们知道，对于执行 C 或者 C++ 程序，需要借助 gcc（g++）指令来调用 GCC 编译器。并且对于以 .c 为扩展名的文件，GCC 会自动将其视为 C 源代码文件；而对于以 .cpp 为扩展名的文件，GCC 会自动将其视为 C++ 源代码文件。

除此之外，GCC 编译器还可以自动识别多种扩展名（如表 3 所示），即根据不同的扩展名确定该文件该怎样编译。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOjuOrzmZ7n4Gz7sPVibTrZN6FRXWDvjxKNZK2iaVnZiaLmZgAw02o8sicJw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

表3 GCC自动识别的常用扩展名

注意，表 1 仅罗列了 GCC 编译器可识别的与 C 和 C++ 语言相关的文件后缀名。除此之外，GCC 编译器还支持 Go、Objective-C，Objective-C ++，Fortran，Ada，D 和 BRIG（HSAIL）等编程语言的编译，关于这些编程语言可被识别的文件扩展名，感兴趣的读者可前往GCC官网查看。

有读者可能会问，如果当前文件的扩展名和表 1 不符，还能使用 GCC 编译器吗？答案是肯定的。只需要借助 -x 选项（小写）指明当前文件的类型即可。例如：一个C程序，存储在名为demo的文件中：

```
//存储在 demo 文件中
#include <stdio.h>
int main(){
   puts("GCC教程：http://c.biancheng.net/gcc/");
   return 0;
}
```

显然，这是一段完整的 C 语言程序，但由于其存储在无扩展名的 demo 文件中，如果直接使用 gcc 指令调用 GCC 编译器，则执行会报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOw4MmWnAIvK98AIWuKW1CicUOZD8utrY1G9c0BGlPB9dugYmE24WUlTA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，GCC 编译器无法识别 demo 这个文件。这种情况下，就必须使用 -x 选项手动为其指定文件的类型，例如：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOvzUtD5H0zunAaEpYFSprn45GBbkRq2M1YPqnL69bCnZbpVqXzzia0lQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

通过为 gcc 指令添加 -xc 选项，表明当前 demo 为 C 语言程序文件，由此 GCC 编译器即可成功将其编译为 a.out 可执行文件。除了用 c 表明 C 语言程序文件外，-x 指令还是后跟 c-header（C语言头文件）、c++（C++源文件）、c++-header（C++程序头文件）等选项。

GCC -std编译标准

任何一门语言都在不停的维护和更新，以 C 语言为例，发展至今该编程语言已经迭代了诸多个版本，例如 C89（偶尔又称为 C90）、C94（C89 的修订版）、C99、C11、C17，以及当下正在开发的 C2X 新标准。甚至于在这些标准的基础上，GCC 编译器本身还对 C 语言的语法进行了扩展，先后产生了 GNU90、GNU99、GNU11 以及 GNU17 这 4 个版本。

C++ 语言的发展也历经了很多个版本，包括 C++98、C++03（C++98 的修订版）、C++11（有时又称为 C++0x）、C++14、C++17，以及即将要发布的 C++20 新标准。和 C 语言类似，GCC 编译器本身也对不同的 C++ 标准做了相应的扩展，比如 GNU++98、GNU++11、GNU++14、GNU++17。

不同版本的 GCC 编译器，默认使用的标准版本也不尽相同。以当前最新的 GCC 10.1.0 版本为例，默认情况下 GCC 编译器会以 GNU11 标准（C11 标准的扩展版）编译 C 语言程序，以 GNU++14 标准（C++14 标准的扩展版）编译 C++ 程序。

们可以手动控制 GCC 编译器使用哪个编译标准吗？答案是肯定的，对于编译 C、C++ 程序来说，借助 -std 选项即可手动控制 GCC 编译程序时所使用的编译标准。也就是说，当使用 gcc 指令编译 C 语言程序时，我们可以借助 -std 选项指定要使用的编译标准；同样，当使用 g++ 指令编译 C++ 程序时，也可以借助 -std 选项指定要使用的编译标准。注意，不同版本的 GCC 编译器，所支持使用的 C/C++ 编译标准也是不同的。

举个例子，如下是一个 C 语言源程序：

```
#include <stdio.h>
int main(){
    for(int i=0;i<10;i++){
        printf("i=%d ",i);
    }
}
```

如果我们想以 c99 的标准编译它，在确认当前所有 GCC 编译器版本支持 C99 标准的前提下，通过执行如下指令，即可完成编译：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfO5ub4ic91R1oOuss9DJsDzGlnqR9aZYJsOyuiciceZbhBgQhvDLJUP9IFg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

但是，对于在 for 循环中声明变量 i 的做法，是违反 C89 标准的。也就是说，如果我们以 C89 的编译标准编译 main.c，GCC 编译器会报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOaXJT5qicM184HickiapCC9KfwtfJ8ic5t1sJiacNkCqck6sYj72k76ic566g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

在编写程序前必须明确要使用的编译标准，并清楚得知道该标准下什么可用，什么不可用。

## 五、GDB调试工具

GDB（GNU Debugger）是一种用于调试程序的工具，由自由软件基金会发布。它可以帮助程序员了解程序运行时的状态，包括变量值、堆栈信息等，并且能够让程序暂停在某个指定位置进行调试。GDB支持多种编程语言，如C、C++、Objective-C、Fortran等。

GDB主要特点：

1. 交互式命令行界面：可以通过命令行输入来控制GDB进行调试操作。
2. 多平台支持：可在多种操作系统上使用，如Linux、Unix和Windows等。
3. 支持多线程：可以对多线程程序进行调试。
4. 支持远程调试：可以通过网络连接到远程机器进行调试。
5. 功能强大：支持断点、单步执行、查看内存和寄存器等功能，还可以输出各种统计信息以供分析。

### 5.1什么是GDB

gdb是GNU debugger的缩写，是编程调试工具。

- GDB官网：  https://www.gnu.org/software/gdb/
- GDB适用的编程语言： Ada / C / C++ / objective-c / Pascal 等。
- GDB的工作方式： 本地调试和远程调试。

目前release的最新版本为8.0，GDB可以运行在Linux 和Windows 操作系统上。

精选文章推荐阅读：

- [1]牛客网论坛最具争议的Linux内核成神笔记，GitHub已下载量已过百万
- [2]牛客网论坛考研计算机组成原理笔记，GitHub已下载量已过百万
- [3]探索网络通信核心技术，手写TCP/IP用户态协议栈，让性能飙升起来！
- [4]万字总结简化跨平台编译利器CMake，从入门到项目实战演练！
- [5]程序员性能之道，从使用perf开始！

安装与启动GDB

1. gdb -v 检查是否安装成功，未安装成功则安装(必须确保编译器已经安装，如 gcc) 。

2. 启动 gdb

3. 1. gdb test_file.exe 来启动 gdb 调试, 即直接指定需要调试的可执行文件名

   2. 直接输入 gdb 启动，进入 gdb 之后采用命令　file test_file.exe　来指定文件名

   3. 如果目标执行文件要求出入参数(如 argv[] 接收参数)，则可以通过三种方式指定参数:

   4. 1. 在启动 gdb 时，gdb --args text_file.exe
      2. 在进入gdb 之后，运行 set args param_1
      3. 在 进入 gdb 调试以后，run param_1 或者 start para_1

gdb的功能

- 启动程序，可以按照用户自定义的要求随心所欲的运行程序。
- 可让被调试的程序在用户所指定的调试断点处停住（断点可以是条件表达式）。
- 当程序停住时，可以检查此时程序中所发生的事。比如，可以打印变量的值。
- 动态改变变量程序的执行环境。

gdb的使用

运行程序

```
run（r）运行程序，如果要加参数，则是run arg1 arg2 ...
```

查看源代码

```
list（l）：查看最近十行源码
list fun：查看fun函数源代码
list file:fun：查看flie文件中的fun函数源代码
```

设置断点与观察断点

```
break 行号/fun设置断点。
break file:行号/fun设置断点。
break if<condition>：条件成立时程序停住。
info break（缩写：i b）：查看断点。
watch expr：一旦expr值发生改变，程序停住。
delete n：删除断点。
```

单步调试

```
continue（c）：运行至下一个断点。
step（s）：单步跟踪，进入函数，类似于VC中的step in。
next（n）：单步跟踪，不进入函数，类似于VC中的step out。
finish：运行程序，知道当前函数完成返回，并打印函数返回时的堆栈地址和返回值及参数值等信息。
until：当厌倦了在一个循环体内单步跟踪时，这个命令可以运行程序知道退出循环体。
```

查看运行时数据

```
print（p）：查看运行时的变量以及表达式。
ptype：查看类型。
print array：打印数组所有元素。
print *array@len：查看动态内存。len是查看数组array的元素个数。
print x=5：改变运行时数据。
```

程序错误

- 编译错：编写程序的时候没有符合语言规范导致编译错误。比如：语法错误。
- 运行时错误：编译器检查不出这种错误，但在运行时候可能会导致程序崩溃。比如：内存地址非法访问。
- 逻辑错误：编译和运行都很顺利，但是程序没有干我们期望干的事情。

gdb调试段错误

什么是段错误？段错误是由于访问非法地址而产生的错误。

- 访问系统数据区，尤其是往系统保护的内存地址写数据。比如：访问地址为0的地址。
- 内存越界（数组越界，变量类型不一致等）访问到不属于当前程序的内存区域。

gdb调试段错误，可以直接运行程序，当程序运行崩溃后，gdb会打印运行的信息，比如：收到了SIGSEGV信号，然后可以使用`bt`命令，打印栈回溯信息，然后根据程序发生错误的代码，修改程序。

core文件调试

core文件

在程序崩溃时，一般会生成一个文件叫`core`文件。core文件记录的是程序崩溃时的内存映像，并加入调试信息，core文件生成过程叫做`core dump（核心已转储）`。系统默认不会生成该文件。

设置生成core文件

- `ulimit -c`：查看core-dump状态。
- `ulimit -c xxxx`：设置core文件的大小。
- `ulimit -c unlimited`：core文件无限制大小。

gdb调试core文件

当设置完`ulimit -c xxxx`后，再次运行程序发生段错误，此时就会生成一个`core`文件，使用`gdb core`调试core文件，使用`bt`命令打印栈回溯信息。

> 【文章福利】小编推荐自己的Linux内核技术交流群:【865977150】整理了一些个人觉得比较好的学习书籍、视频资料共享在群文件里面，有需要的可以自行添加哦！！！

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR1OBl2HkEwV305Nhibu5tS7MsKrZQwl8Gw37GlQ4q5A1IlRsdlkv5CZ6FE8XqnqJXqTXgLh0ggcBNg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

### 5.2GDB常用命令

- 以下以 test_file.c　作为源程序例子的名字，test_file.exe 作为可执行文件例子的名字, 以param_1 作为参数的例子的名字。
- (gdb) 表示是在 gdb 调试模式下运行
- 一般常用的方法有两种，即打断点调试 和单步调试。
- list(l): 列出源代码
- quit(q):　退出 gdb 调试模式
- 进入 gdb 之后，输入 help 可以查看所有命令的使用说明

查看源码

list [函数名][行数]

打断点调试

（1）设置断点：

- a、break + [源代码行号][源代码函数名][内存地址]
- b、break ... if condition ...可以是上述任一参数，condition是条件。例如在循环体中可以设置break ... if i = 100 来设置循环次数

删除断点

(gdb) clear location：参数 location 通常为某一行代码的行号或者某个具体的函数名。当 location 参数为某个函数的函数名时，表示删除位于该函数入口处的所有断点。

(gdb) delete [breakpoints] [num]：breakpoints 参数可有可无，num 参数为指定断点的编号，其可以是 delete 删除某一个断点，而非全部。

禁用断点

disable [breakpoints] [num...]：breakpoints 参数可有可无；num... 表示可以有多个参数，每个参数都为要禁用断点的编号。如果指定 num...，disable 命令会禁用指定编号的断点；反之若不设定 num...，则 disable 会禁用当前程序中所有的断点。

激活断点

1. enable [breakpoints] [num...]激活用 num... 参数指定的多个断点，如果不设定 num...，表示激活所有禁用的断点
2. enable [breakpoints] once num… 临时激活以 num... 为编号的多个断点，但断点只能使用 1 次，之后会自动回到禁用状态
3. enable [breakpoints] count num... 临时激活以 num... 为编号的多个断点，断点可以使用 count 次，之后进入禁用状态
4. enable [breakpoints] delete num… 激活 num.. 为编号的多个断点，但断点只能使用 1 次，之后会被永久删除。

break(b): 打的是普通断点，打断点有两种形式

(gdb) break location // b location，location 代表打断点的位置

![图片](https://mmbiz.qpic.cn/mmbiz_png/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOCr7CIWfuCUJ5NA9dpqdQcia7On5BXTREDaGPAMY2uglXVPLO4FQDXwQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

(gdb) break ... if cond // b .. if cond，代表如果 cond 条件为true，则在 “...” 处打断点

通过借助 condition 命令为不同类型断点设置条件表达式，只有当条件表达式成立（值为 True）时，相应的断点才会触发从而使程序暂停运行。

tbreak: tbreak 命令可以看到是 break 命令的另一个版本，tbreak 和 break 命令的用法和功能都非常相似，唯一的不同在于，使用 tbreak 命令打的断点仅会作用 1 次，即使程序暂停之后，该断点就会自动消失。

rbreak: 和 break 和 tbreak 命令不同，rbreak 命令的作用对象是 C、C++ 程序中的函数，它会在指定函数的开头位置打断点。

- (gdb) tbreak regex

- - regex　代表一个正则表达式，会在匹配到的函数的内部的开头位置打断点

- tbreak 命令打的断点和 break 命令打断点的效果是一样的，会一直存在，不会自动消失。

watch: 此命令打的是观察断点，可以监控某个变量或者表达式的值。只有当被监控变量（表达式）的值发生改变，程序才会停止运行。

- (gdb) watch cond

- - cond 代表的就是要监控的变量或者表达式

rwatch 命令：只要程序中出现读取目标变量（表达式）的值的操作，程序就会停止运行；

awatch 命令：只要程序中出现读取目标变量（表达式）的值或者改变值的操作，程序就会停止运行。

catch: 捕捉断点的作用是，监控程序中某一事件的发生，例如程序发生某种异常时、某一动态库被加载时等等，一旦目标时间发生，则程序停止执行。

（2）观察断点：

- a、watch + [变量][表达式] 当变量或表达式值改变时即停住程序。
- b、rwatch + [变量][表达式] 当变量或表达式被读时，停住程序。
- c、awatch + [变量][表达式] 当变量或表达式被读或被写时，停住程序。

（3）设置捕捉点：

catch + event 当event发生时，停住程序。

event可以是下面的内容：

- a、throw 一个C++抛出的异常。（throw为关键字）
- b、catch 一个C++捕捉到的异常。（catch为关键字）
- c、exec 调用系统调用exec时。（exec为关键字，目前此功能只在HP-UX下有用）
- d、fork 调用系统调用fork时。（fork为关键字，目前此功能只在HP-UX下有用）
- e、vfork 调用系统调用vfork时。（vfork为关键字，目前此功能只在HP-UX下有用）
- f、load 或 load 载入共享库（动态链接库）时。（load为关键字，目前此功能只在HP-UX下有用）
- g、unload 或 unload 卸载共享库（动态链接库）时。（unload为关键字，目前此功能只在HP-UX下有用）

（4）捕获信号：

handle + [argu] + signals

signals：是Linux/Unix定义的信号，SIGINT表示中断字符信号，也就是Ctrl+C的信号，SIGBUS表示硬件故障的信号；SIGCHLD表示子进程状态改变信号； SIGKILL表示终止程序运行的信号，等等。

argu：

- nostop 当被调试的程序收到信号时，GDB不会停住程序的运行，但会打出消息告诉你收到这种信号。
- stop 当被调试的程序收到信号时，GDB会停住你的程序。
- print 当被调试的程序收到信号时，GDB会显示出一条信息。
- noprint 当被调试的程序收到信号时，GDB不会告诉你收到信号的信息。
- pass or noignore 当被调试的程序收到信号时，GDB不处理信号。这表示，GDB会把这个信号交给被调试程序会处理。
- nopass or ignore 当被调试的程序收到信号时，GDB不会让被调试程序来处理这个信号。

（5）线程中断：

break [linespec] thread [threadno] [if ...]

linespec 断点设置所在的源代码的行号。如: test.c:12表示文件为test.c中的第12行设置一个断点。

threadno 线程的ID。是GDB分配的，通过输入info threads来查看正在运行中程序的线程信息。

if ... 设置中断条件。

查看信息：

（1）查看数据：

print variable 查看变量

print *array@len 查看数组（array是数组指针，len是需要数据长度）

可以通过添加参数来设置输出格式：

```
/ 按十六进制格式显示变量。
/d 按十进制格式显示变量。
/u 按十六进制格式显示无符号整型。
/o 按八进制格式显示变量。
/t 按二进制格式显示变量。 
/a 按十六进制格式显示变量。
/c 按字符格式显示变量。
/f 按浮点数格式显示变量。
```

（2）查看内存

examine /n f u + 内存地址（指针变量）

- n 表示显示内存长度
- f 表示输出格式（见上）
- u 表示字节数制定（b 单字节；h 双字节；w 四字节；g 八字节；默认为四字节）

```
如：x /10cw pFilePath  （pFilePath为一个字符串指针，指针占4字节）
     x 为examine命令的简写。
```

（3）查看栈信息

backtrace [-n][n]

- n 表示只打印栈顶上n层的栈信息。
- -n 表示只打印栈底上n层的栈信息。
- 不加参数，表示打印所有栈信息。

单步调试

run(r)

continue(c)

next(n)

- 命令格式: (gdb) next count：count 表示单步执行多少行代码，默认为 1 行
- 其最大的特点是当遇到包含调用函数的语句时，无论函数内部包含多少行代码，next 指令都会一步执行完。也就是说，对于调用的函数来说，next 命令只会将其视作一行代码

step(s)

- (gdb) step count：参数 count 表示一次执行的行数，默认为 1 行。
- 通常情况下，step 命令和 next 命令的功能相同，都是单步执行程序。不同之处在于，当 step 命令所执行的代码行中包含函数时，会进入该函数内部，并在函数第一行代码处停止执行。

until(u)

- (gdb) until：不带参数的 until 命令，可以使 GDB 调试器快速运行完当前的循环体，并运行至循环体外停止。注意，until 命令并非任何情况下都会发挥这个作用，只有当执行至循环体尾部（最后一行代码）时，until 命令才会发生此作用；反之，until 命令和 next 命令的功能一样，只是单步执行程序

(gdb) until location：参数 location 为某一行代码的行号

查看变量的值

print(p)

- p num_1：参数 num_1 用来代指要查看或者修改的目标变量或者表达式
- 它的功能就是在 GDB 调试程序的过程中，输出或者修改指定变量或者表达式的值

isplay

- (gdb) display expr
- (gdb) display/fmt expr
- expr 表示要查看的目标变量或表达式；参数 fmt 用于指定输出变量或表达式的格式

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOkNRvia3N8nHXU0IDbe4uj1fS8SR6S2r2xvCPNLuJEaic6Yv3E9IemFng/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

- (gdb) undisplay num...
- (gdb) delete display num...
- 参数 num... 表示目标变量或表达式的编号，编号的个数可以是多个
- (gdb) disable display num...
- 禁用自动显示列表中处于激活状态下的变量或表达式
- (gdb) enable display num...
- 也可以激活当前处于禁用状态的变量或表达式
- 和 print 命令一样，display 命令也用于调试阶段查看某个变量或表达式的值
- 它们的区别是，使用 display 命令查看变量或表达式的值，每当程序暂停执行（例如单步执行）时，GDB 调试器都会自动帮我们打印出来，而 print 命令则不会

GDB handle 命令: 信号处理

→(gdb) handle signal mode其中，signal 参数表示要设定的目标信号，它通常为某个信号的全名（SIGINT）或者简称（去除‘SIG’后的部分，如 INT）；如果要指定所有信号，可以用 all 表示。

mode 参数用于明确 GDB 处理该目标信息的方式，其值可以是如下几个：

- ostop：当信号发生时，GDB 不会暂停程序，其可以继续执行，但会打印出一条提示信息，告诉我们信号已经发生；
- stop：当信号发生时，GDB 会暂停程序执行。
- noprint：当信号发生时，GDB 不会打印出任何提示信息；
- print：当信号发生时，GDB 会打印出必要的提示信息；
- nopass（或者 ignore）：GDB 捕获目标信号的同时，不允许程序自行处理该信号；
- pass（或者 noignore）：GDB 调试在捕获目标信号的同时，也允许程序自动处理该信号。

可以在 gdb 模式下，通过 info signals 或者 info signals <signal_name> (例如 info signals SIGINT) 查看不同 signal 的信息。

GDB frame和backtrace命令：查看栈信息

(gdb) frame spec 该命令可以将 spec 参数指定的栈帧选定为当前栈帧。spec 参数的值，常用的指定方法有 3 种：

1. 通过栈帧的编号指定。0 为当前被调用函数对应的栈帧号，最大编号的栈帧对应的函数通常就是 main() 主函数；
2. 借助栈帧的地址指定。栈帧地址可以通过 info frame 命令（后续会讲）打印出的信息中看到；
3. 通过函数的函数名指定。注意，如果是类似递归函数，其对应多个栈帧的话，通过此方法指定的是编号最小的那个栈帧。

(gdb) info frame 我们可以查看当前栈帧中存储的信息

该命令会依次打印出当前栈帧的如下信息：

- 当前栈帧的编号，以及栈帧的地址；
- 当前栈帧对应函数的存储地址，以及该函数被调用时的代码存储的地址
- 当前函数的调用者，对应的栈帧的地址；
- 编写此栈帧所用的编程语言；
- 函数参数的存储地址以及值；
- 函数中局部变量的存储地址；
- 栈帧中存储的寄存器变量，例如指令寄存器（64位环境中用 rip 表示，32为环境中用 eip 表示）、堆栈基指针寄存器（64位环境用 rbp 表示，32位环境用 ebp 表示）等。

除此之外，还可以使用 `info args` 命令查看当前函数各个参数的值；使用 `info locals` 命令查看当前函数中各局部变量的值。

(gdb) backtrace [-full] [n] 用于打印当前调试环境中所有栈帧的信息

其中，用 [ ] 括起来的参数为可选项，它们的含义分别为：

- n：一个整数值，当为正整数时，表示打印最里层的 n 个栈帧的信息；n 为负整数时，那么表示打印最外层 n 个栈帧的信息；
- -full：打印栈帧信息的同时，打印出局部变量的值。

GDB编辑和搜索源码

GDB edit命令：编辑文件

- (gdb) edit [location]

- (gdb) edit [filename] : [location]

- - location 表示程序中的位置。这个命令表示激活文件的指定位置，然后进行编辑。
  - 如果遇到报错 "bash: /bin/ex: 没有那个文件或目录", 因为 GDB 的默认编辑器是 ex , 则需要指定编辑器，如 export EDITOR=/usr/bin/vim or export EDITOR=/usr/bin/vi

GDB search命令：搜索文件

- search <regexp>

- reverse-search <regexp>

- - 第一项命令格式表示从当前行的开始向前搜索，后一项表示从当前行开始向后搜索。其中 regexp 就是正则表达式，正则表达式描述了一种字符串匹配的模式，可以用来检查一个串中是否含有某种子串、将匹配的子串替换或者从某个串中取出符合某个条件的子串。很多的编程语言都支持使用正则表达式。

### 5.3GDB调试程序用法

一般来说，GDB主要帮忙你完成下面四个方面的功能：

1、启动你的程序，可以按照你的自定义的要求随心所欲的运行程序。
2、可让被调试的程序在你所指定的调置的断点处停住。（断点可以是条件表达式）
3、当程序被停住时，可以检查此时你的程序中所发生的事。
4、动态的改变你程序的执行环境。

从上面看来，GDB和一般的调试工具没有什么两样，基本上也是完成这些功能，不过在细节上，你会发现GDB这个调试工具的强大，大家可能比较习惯了图形化的调试工具，但有时候，命令行的调试工具却有着图形化工具所不能完成的功能。让我们一一看来。

一个调试示例：

```
源程序：tst.c

1 #include <stdio.h>
2
3 int func(int n)
4 {
5 int sum=0,i;
6 for(i=0; i<n; i++)
7 {
8 sum+=i;
9 }
10 return sum;
11 }
12
13
14 main()
15 {
16 int i;
17 long result = 0;
18 for(i=1; i<=100; i++)
19 {
20 result += i;
21 }
22
23 printf("result[1-100] = %d /n", result );
24 printf("result[1-250] = %d /n", func(250) );
25 }
```

编译生成执行文件：（Linux下）

```
hchen/test> cc -g tst.c -o tst
```

使用GDB调试：

```
hchen/test> gdb tst <---------- 启动GDB
GNU gdb 5.1.1
Copyright 2002 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "i386-SUSE-linux"...
(gdb) l <-------------------- l命令相当于list，从第一行开始例出原码。
1 #include <stdio.h>
2
3 int func(int n)
4 {
5 int sum=0,i;
6 for(i=0; i<n; i++)
7 {
8 sum+=i;
9 }
10 return sum;
(gdb) <-------------------- 直接回车表示，重复上一次命令
11 }
12
13
14 main()
15 {
16 int i;
17 long result = 0;
18 for(i=1; i<=100; i++)
19 {
20 result += i;
(gdb) break 16 <-------------------- 设置断点，在源程序第16行处。
Breakpoint 1 at 0x8048496: file tst.c, line 16.
(gdb) break func <-------------------- 设置断点，在函数func()入口处。
Breakpoint 2 at 0x8048456: file tst.c, line 5.
(gdb) info break <-------------------- 查看断点信息。
Num Type Disp Enb Address What
1 breakpoint keep y 0x08048496 in main at tst.c:16
2 breakpoint keep y 0x08048456 in func at tst.c:5
(gdb) r <--------------------- 运行程序，run命令简写
Starting program: /home/hchen/test/tst

Breakpoint 1, main () at tst.c:17 <---------- 在断点处停住。
17 long result = 0;
(gdb) n <--------------------- 单条语句执行，next命令简写。
18 for(i=1; i<=100; i++)
(gdb) n
20 result += i;
(gdb) n
18 for(i=1; i<=100; i++)
(gdb) n
20 result += i;
(gdb) c <--------------------- 继续运行程序，continue命令简写。
Continuing.
result[1-100] = 5050 <----------程序输出。

Breakpoint 2, func (n=250) at tst.c:5
5 int sum=0,i;
(gdb) n
6 for(i=1; i<=n; i++)
(gdb) p i <--------------------- 打印变量i的值，print命令简写。
$1 = 134513808
(gdb) n
8 sum+=i;
(gdb) n
6 for(i=1; i<=n; i++)
(gdb) p sum
$2 = 1
(gdb) n
8 sum+=i;
(gdb) p i
$3 = 2
(gdb) n
6 for(i=1; i<=n; i++)
(gdb) p sum
$4 = 3
(gdb) bt <--------------------- 查看函数堆栈。
#0 func (n=250) at tst.c:5
#1 0x080484e4 in main () at tst.c:24
#2 0x400409ed in __libc_start_main () from /lib/libc.so.6
(gdb) finish <--------------------- 退出函数。
Run till exit from #0 func (n=250) at tst.c:5
0x080484e4 in main () at tst.c:24
24 printf("result[1-250] = %d /n", func(250) );
Value returned is $6 = 31375
(gdb) c <--------------------- 继续运行。
Continuing.
result[1-250] = 31375 <----------程序输出。

Program exited with code 027. <--------程序退出，调试结束。
(gdb) q <--------------------- 退出gdb。
hchen/test>
```

好了，有了以上的感性认识，还是让我们来系统地认识一下gdb吧。

基本gdb命令：

```
GDB常用命令	格式	含义	简写
list	List [开始，结束]	列出文件的代码清单	l
prit	Print 变量名	打印变量内容	p
break	Break [行号或函数名]	设置断点	b
continue	Continue [开始，结束]	继续运行	c
info	Info 变量名	列出信息	i
next	Next	下一行	n
step	Step	进入函数（步入）	S
display	Display 变量名	显示参数	 
file	File 文件名（可以是绝对路径和相对路径）	加载文件	 
run	Run args	运行程序	r
```

### 5.4GDB实战

下面是一个使用了上述命令的实战例子：

```
[root@www.linuxidc.com bufbomb]# gdb bufbomb 
GNU gdb (GDB) Red Hat Enterprise Linux (7.2-75.el6)
Copyright (C) 2010 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-RedHat-linux-gnu".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from /root/Temp/bufbomb/bufbomb...done.
(gdb) b getbuf
Breakpoint 1 at 0x8048ad6
(gdb) run -t cdai
Starting program: /root/Temp/bufbomb/bufbomb -t cdai
Team: cdai
Cookie: 0x5e5ee04e

Breakpoint 1, 0x08048ad6 in getbuf ()
Missing separate debuginfos, use: debuginfo-install glibc-2.12-1.149.el6_6.4.i686

(gdb) bt
#0  0x08048ad6 in getbuf ()
#1  0x08048db2 in test ()
#2  0x08049085 in launch ()
#3  0x08049257 in main ()
(gdb) info frame 0
Stack frame at 0xffffb540:
 eip = 0x8048ad6 in getbuf; saved eip 0x8048db2
 called by frame at 0xffffb560
 Arglist at 0xffffb538, args: 
 Locals at 0xffffb538, Previous frame's sp is 0xffffb540
 Saved registers:
  ebp at 0xffffb538, eip at 0xffffb53c
(gdb) info registers
eax            0xc      12
ecx            0xffffb548       -19128
edx            0xc8c340 13157184
ebx            0x0      0
esp            0xffffb510       0xffffb510
ebp            0xffffb538       0xffffb538
esi            0x804b018        134524952
edi            0xffffffff       -1
eip            0x8048ad6        0x8048ad6 <getbuf+6>
eflags         0x282    [ SF IF ]
cs             0x23     35
ss             0x2b     43
ds             0x2b     43
es             0x2b     43
fs             0x0      0
gs             0x63     99
(gdb) x/10x $sp
0xffffb510:     0xf7ffc6b0      0x00000001      0x00000001      0xffffb564
0xffffb520:     0x08048448      0x0804a12c      0xffffb548      0x00c8aff4
0xffffb530:     0x0804b018      0xffffffff

(gdb) si
0x08048ad9 in getbuf ()
(gdb) si
0x08048adc in getbuf ()
(gdb) si
0x080489c0 in Gets ()
(gdb) n
Single stepping until exit from function Gets,
which has no line number information.
Type string:123
0x08048ae1 in getbuf ()
(gdb) si
0x08048ae2 in getbuf ()
(gdb) c
Continuing.
Dud: getbuf returned 0x1
Better luck next time

Program exited normally.
(gdb) quit
```

逆向调试

GDB 7.0后加入了Reversal Debugging功能。具体来说，比如我在getbuf()和main()上设置了断点，当启动程序时会停在main()函数的断点上。此时敲入record后continue到下一断点getbuf()，GDB就会记录从main()到getbuf()的运行时信息。现在用rn就可以逆向地从getbuf()调试到main()。就像《X战警：逆转未来》里一样，挺神奇吧！

这种方式适合从bug处反向去找引起bug的代码，实用性因情况而异。当然，它也是有局限性的。像程序假如有I/O输出等外部条件改变时，GDB是没法“逆转”的。

```
[root@www.linuxidc.com bufbomb]# gdb bufbomb 
GNU gdb (GDB) Red Hat Enterprise Linux (7.2-75.el6)
Copyright (C) 2010 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-redhat-linux-gnu".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from /root/Temp/bufbomb/bufbomb...done.

(gdb) b getbuf
Breakpoint 1 at 0x8048ad6
(gdb) b main
Breakpoint 2 at 0x80490c6

(gdb) run -t cdai
The program being debugged has been started already.
Start it from the beginning? (y or n) y

Starting program: /root/Temp/bufbomb/bufbomb -t cdai

Breakpoint 2, 0x080490c6 in main ()
(gdb) record
(gdb) c
Continuing.
Team: cdai
Cookie: 0x5e5ee04e

Breakpoint 1, 0x08048ad6 in getbuf ()

(gdb) rn
Single stepping until exit from function getbuf,
which has no line number information.
0x08048dad in test ()
(gdb) rn
Single stepping until exit from function test,
which has no line number information.
0x08049080 in launch ()
(gdb) rn
Single stepping until exit from function launch,
which has no line number information.
0x08049252 in main ()
```

VSCode+GDB+Qemu调试ARM64 linux内核

linux kernel是一个非常复杂的系统，初学者会很难入门。如果有一个方便的调试环境，学习效率至少能有5-10倍的提升。

为了学习linux内核，通常有这两个需要：

1. 可以摆脱硬件，方便的编译和运行linux
2. 可以使用图形化的工具来调试linux

笔者使用VSCode+GDB+Qemu完成了这两个需求：

- qemu作为虚拟机，用来启动linux。
- VSCode+GDB作为调试工具，用来图形化地DEBUG。

最终效果大致如下：

qemu运行界面：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfO7BuSmia4icwmTlPrPG5xPjypKuCHHuU098fNHuMpTCspcLPVAW1KjDvQ/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

vscode调试界面：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOskmd0YqgUAKP1vm4SqibkAf7fzXKT0HKP6SsVk0ic78nW2LZSYdoA9FQ/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

下面将一步一步介绍如何搭建上述环境。本文所有操作都在Vmware Ubuntu16虚拟机上进行。

安装编译工具链

由于Ubuntu是X86架构，为了编译arm64的文件，需要安装交叉编译工具链

```
sudo apt-get install gcc-aarch64-linux-gnu
sudo apt-get install libncurses5-dev  build-essential git bison flex libssl-dev
```

制作根文件系统

linux的启动需要配合根文件系统，这里我们利用busybox来制作一个简单的根文件系统

编译busybox

```
wget  https://busybox.net/downloads/busybox-1.33.1.tar.bz2
tar -xjf busybox-1.33.1.tar.bz2
cd busybox-1.33.1
```

打开静态库编译选项

```
make menuconfig
Settings --->
 [*] Build static binary (no shared libs)
```

指定编译工具

```
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-gnu-
```

编译

```
make
make install
```

编译完成，在busybox目录下生成_install目录

定制文件系统

为了init进程能正常启动， 需要再额外进行一些配置

根目录添加etc、dev和lib目录

```
# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install [1:02:17]
$ mkdir etc dev lib
# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install [1:02:17]
$ ls
bin  dev  etc  lib  linuxrc  sbin  usr
```

在etc分别创建文件：

```
# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/etc [1:06:13]
$ cat profile
#!/bin/sh
export HOSTNAME=bryant
export USER=root
export HOME=/home
export PS1="[$USER@$HOSTNAME \W]\# "
PATH=/bin:/sbin:/usr/bin:/usr/sbin
LD_LIBRARY_PATH=/lib:/usr/lib:$LD_LIBRARY_PATH
export PATH LD_LIBRARY_PATH

# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/etc [1:06:16]
$ cat inittab
::sysinit:/etc/init.d/rcS
::respawn:-/bin/sh
::askfirst:-/bin/sh
::ctrlaltdel:/bin/umount -a -r

# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/etc [1:06:19]
$ cat fstab
#device  mount-point    type     options   dump   fsck order
proc /proc proc defaults 0 0
tmpfs /tmp tmpfs defaults 0 0
sysfs /sys sysfs defaults 0 0
tmpfs /dev tmpfs defaults 0 0
debugfs /sys/kernel/debug debugfs defaults 0 0
kmod_mount /mnt 9p trans=virtio 0 0

# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/etc [1:06:26]
$ ls init.d
rcS

# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/etc [1:06:30]
$ cat init.d/rcS
mkdir -p /sys
mkdir -p /tmp
mkdir -p /proc
mkdir -p /mnt
/bin/mount -a
mkdir -p /dev/pts
mount -t devpts devpts /dev/pts
echo /sbin/mdev > /proc/sys/kernel/hotplug
mdev -s
```

这里对这几个文件做一点说明：

1. busybox 作为linuxrc启动后， 会读取/etc/profile, 这里面设置了一些环境变量和shell的属性
2. 根据/etc/fstab提供的挂载信息， 进行文件系统的挂载
3. busybox 会从 /etc/inittab中读取sysinit并执行， 这里sysinit指向了/etc/init.d/rcS
4. /etc/init.d/rcS 中 ，mdev -s 这条命令很重要， 它会扫描/sys目录，查找字符设备和块设备，并在/dev下mknod

dev目录：

```
# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/dev [1:17:36]
$ sudo mknod console c 5 1
```

这一步很重要， 没有console这个文件， 用户态的输出没法打印到串口上

lib目录：拷贝lib库，支持动态编译的应用程序运行：

```
# bryant @ ubuntu in ~/Downloads/busybox-1.33.1/_install/lib [1:18:43]
$ cp /usr/aarch64-linux-gnu/lib/*.so*  -a .
```

编译内核

配置内核

linux内核源码可以在github上直接下载。

根据arch/arm64/configs/defconfig 文件生成.config

```
make defconfig ARCH=arm64
```

将下面的配置加入.config文件中

```
CONFIG_DEBUG_INFO=y 
CONFIG_INITRAMFS_SOURCE="./root"
CONFIG_INITRAMFS_ROOT_UID=0
CONFIG_INITRAMFS_ROOT_GID=0
```

CONFIG_DEBUG_INFO是为了方便调试

CONFIG_INITRAMFS_SOURCE是指定kernel ramdisk的位置，这样指定之后ramdisk会直接被编译到kernel 镜像中。

我们将之前制作好的根文件系统cp到root目录下：

```
# bryant @ ubuntu in ~/Downloads/linux-arm64 on git:main x [1:26:56]
$ cp -r ../busybox-1.33.1/_install root
```

执行编译

```
make ARCH=arm64 Image -j8  CROSS_COMPILE=aarch64-linux-gnu-
```

这里指定target为Image 会只编译kernel, 不会编译modules， 这样会增加编译速度

启动qemu

下载qemu

需要注意的，qemu最好源码编译， 用apt-get直接安装的qemu可能版本过低，导致无法启动arm64内核。笔者是使用4.2.1版本的qemu

```
apt-get install build-essential zlib1g-dev pkg-config libglib2.0-dev binutils-dev libboost-all-dev autoconf libtool libssl-dev libpixman-1-dev libpython-dev python-pip python-capstone virtualenv
wget https://download.qemu.org/qemu-4.2.1.tar.xz
tar xvJf qemu-4.2.1.tar.xz
cd qemu-4.2.1
./configure --target-list=x86_64-softmmu,x86_64-linux-user,arm-softmmu,arm-linux-user,aarch64-softmmu,aarch64-linux-user --enable-kvm
make 
sudo make install
```

编译完成之后，qemu在 /usr/local/bin目录下

```
$ /usr/local/bin/qemu-system-aarch64 --version
QEMU emulator version 4.2.1
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers
```

启动linux内核

```
/usr/local/bin/qemu-system-aarch64 -m 512M -smp 4 -cpu cortex-a57 -machine virt -kernel
```

这里对于参数做一些解释：

- `-m 512M` 内存为512M
- `-smp 4` 4核
- `-cpu cortex-a57`cpu 为cortex-a57
- `-kernel` kernel镜像文件
- `-append`传给kernel 的cmdline参数。其中rdinit指定了init进程；nokaslr 禁止内核起始地址随机化，这个很重要， 否则GDB调试可能有问题；console=ttyAMA0指定了串口，没有这一步就看不到linux的输出；
- `-nographic`禁止图形输出
- `-s`监听gdb端口， gdb程序可以通过1234这个端口连上来。

这里说明一下console=ttyAMA0是怎么生效的。

查看linux源码可知ttyAMA0对应的是`AMBA_PL011`这个驱动：

```
config SERIAL_AMBA_PL011_CONSOLE
    bool "Support for console on AMBA serial port"
    depends on SERIAL_AMBA_PL011=y
    select SERIAL_CORE_CONSOLE
    select SERIAL_EARLYCON
    help
      Say Y here if you wish to use an AMBA PrimeCell UART as the system
      console (the system console is the device which receives all kernel
      messages and warnings and which allows logins in single user mode).

      Even if you say Y here, the currently visible framebuffer console
      (/dev/tty0) will still be used as the system console by default, but
      you can alter that using a kernel command line option such as
      "console=ttyAMA0". (Try "man bootparam" or see the documentation of
      your boot loader (lilo or loadlin) about how to pass options to the
      kernel at boot time.)
```

AMBA_PL011是arm的一个标准串口设备， qemu 的输出就是模拟的这个串口。

在qemu的源码文件中，也可以看到PL011的相关文件：

```
# bryant @ ubuntu in ~/Downloads/qemu-4.2.1 [1:46:54]
$ find . -name "*pl011*"
./hw/char/pl011.c
```

成功启动Linux后， 串口打印如下：

```
[    3.401567] usbcore: registered new interface driver usbhid
[    3.404445] usbhid: USB HID core driver
[    3.425030] NET: Registered protocol family 17
[    3.429743] 9pnet: Installing 9P2000 support
[    3.435439] Key type dns_resolver registered
[    3.440299] registered taskstats version 1
[    3.443685] Loading compiled-in X.509 certificates
[    3.461041] input: gpio-keys as /devices/platform/gpio-keys/input/input0
[    3.473163] ALSA device list:
[    3.474432]   No soundcards found.
[    3.485283] uart-pl011 9000000.pl011: no DMA platform data
[    3.541376] Freeing unused kernel memory: 10752K
[    3.545897] Run /linuxrc as init process
[    3.548390]   with arguments:
[    3.550279]     /linuxrc
[    3.551073]     nokaslr
[    3.552216]   with environment:
[    3.554396]     HOME=/
[    3.555898]     TERM=linux
[    3.985835] 9pnet_virtio: no channels available for device kmod_mount
mount: mounting kmod_mount on /mnt failed: No such file or directory
/etc/init.d/rcS: line 8: can't create /proc/sys/kernel/hotplug: nonexistent directory

Please press Enter to activate this console.
[root@bryant ]#
[root@bryant ]#
```

VSCode+GDB

vscode中集成了GDB功能，我们可以用它来图形化的调试linux kernel

首先我们添加vscode的gdb配置文件(.vscode/launch.json)：

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "kernel debug",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/vmlinux",
            "cwd": "${workspaceFolder}",
            "MIMode": "gdb",
            "miDebuggerPath":"/usr/bin/gdb-multiarch",
            "miDebuggerServerAddress": "localhost:1234"
        }
    ]
}
```

这里对几个重点参数做一些说明：

- `program`: 调试的符号文件
- `miDebuggerPath`：gdb的路径， 这里需要注意的是，由于我们是arm64内核，因此需要用gdb-multiarch来进行调试
- `miDebuggerServerAddress`：对端地址，qemu会默认使用1234这个端口

配置完成之后，可以直接启动GDB, 连接上linux kernel

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOtPdGQOmKF3wBlCJanianXfYVqBLg8vpbODAVZd2PtLjbM90VpMw1XVw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

在vscode中，可以设置断点，进行单步调试

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOC9sctnJzEDhGtEbiboaH78y455PXrhaaf9EG2uicn4eyLvXx65kIibXjg/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOyAZbgictKv0En6Xouvkb91ic9voRFkGnVW5eretiaKZhNmoibZn0jkWic9A/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

## 六、Apache HTTP Server

Apache HTTP Server，通常称为 Apache Web Server，是世界上最流行的 Web 服务器软件之一，由 Apache 软件基金会开发和维护。它是一个跨平台的、开源的 HTTP 服务器，可以在多种操作系统上运行（如 Linux、Unix、Windows 等），并支持多种编程语言（如 PHP、Python 等）。

Apache HTTP Server 的主要特点包括：

1. 多模块化：提供了很多扩展模块，可以通过加载不同的模块来实现不同的功能。
2. 高度可配置：具有灵活性和可扩展性，允许用户根据自己的需求进行定制。
3. 安全性高：提供了各种安全机制来保护服务器和客户端数据的安全性。
4. 可靠稳定：已经成熟，并且被广泛应用于互联网中，在负载量较大时仍能保持稳定性。
5. 性能优越：采用事件驱动和异步 I/O 模型等技术，以及缓存机制等方法来提高处理效率和响应速度。

### 6.1安装Apache软件

\1. 下载软件包

```
[root@centos6 ~]# wget http://mirror.bit.edu.cn/apache/httpd/httpd-2.4.4.tar.gz 
[root@centos6 ~]# wget http://mirror.bjtu.edu.cn/apache/apr/apr-1.4.6.tar.gz 
[root@centos6 ~]# wget http://mirror.bjtu.edu.cn/apache/apr/apr-util-1.5.2.tar.gz 
```

\2. 安装软件

```
[root@centos6 ~]# yum –y install gcc autoconf automake make \ 
> pcre pcre-devel openssl openssl-devel 
[root@centos6 ~]# tar –xzf httpd-2.4.4.tar.gz –C /usr/src/ 
[root@centos6 ~]# tar –xzf apr-1.4.6.tar.gz –C /usr/src/ 
[root@centos6 ~]# tar –xzf apr-util-1.5.2.tar.gz –C /usr/src/ 
[root@centos6 ~]# cd /usr/src/apr-1.4.6/ 
[root@centos6 apr-1.4.6]# ./configure  --with-apr=/usr/local/apr/ 
[root@centos6 apr-1.4.6]# make && make install 
[root@centos6 apr-1.4.6]# cd /usr/src/apr-util-1.5.2/ 
[root@centos6 apr-util-1.5.2]# ./configure  --with-apr=/usr/local/apr/ 
[root@centos6 apr-util-1.5.2]# make && make install 
[root@centos6 apr-util-1.5.2]# cd /usr/src/httpd-2.4.4/ 
[root@centos6 httpd-2.4.4]# ./configure –prefix=/usr/local/apache2 –enable-so \ 
> --enable-ssl  --enable-rewrite –with-mpm=worker –with-suexec-bin \ 
> --with-apr=/usr/local/apr/ 
[root@centos6 httpd-2.4.4]# make && make install 
```

configure脚本用来检查系统环境、查找依赖文件、设置安装路径等操作，configure拥有很多参数，读者可以通过./configure --help查看该脚本支持的所有参数。

下面是configure常用参数说明：

```
参数            描述
--prefix            指定Apache httpd程序的安装主目录
--enable-so         开启模块化功能，支持DSO（动态共享对象）
--enable-ssl        支持SSL加密
--enable-rewrite    支持地址重写
--with-mpm          设置Apache httpd工作模式
--with-suexec-bin   支持SUID、SGID
--with-apr          指定apr程序绝对路径
```

\3. 启动服务

```
[root@centos6 ~]# /usr/local/apache2/bin/apachectl start 
[root@centos6 ~]# netstat -ntulp |grep http 
[root@centos6 ~]# iptables -I INPUT -p tcp -dport 80 -j ACCEPT 
```

安装完成后Apache会提供名为apachectl启动脚本，该脚本提供了Apache httpd的启动、关闭以及测试功能，没有修改配置文件的情况下使用start启动httpd程序，可能会返回错误提示：”Could not reliably determine the server’s fully qualified domain name”，提示说明httpd无法确定服务器域名称，可以修改主配置文件的ServerName项来解决。该提示也可以忽略，通过netstat命令查看httpd已经启动成功。

在客户端使用浏览器访问该Web服务器，看到”IT works!”说明服务器可以被正常访问了。

apachectl具体参数如下：

```
参数            描述
start           启动httpd程序，如果已经启动过该程序则报错
stop            关闭httpd程序
restart         重启httpd程序
graceful        启动httpd，不中断现有的连接
graceful-stop   关闭httpd，不中断现有的连接
status          查看httpd程序当前状态
configtest      检查httpd主配置文件语法
```

### 6.2Apache与Tomcat的关系

Apache:侧重于HTTP Server；

Tomcat:侧重于servlet引擎，如果以standalone方式运行，功能上与Apache等效，支持JSP，但对静态网页不太理想； Apache:侧重于HTTP Server；

相同点：

- 1、两者都是Apache组织开发的
- 2、两者都有HTTP服务的功能
- 3、两者都是免费的

不同点：

- 1、Apache是专门用了提供HTTP服务的，以及相关配置的（例如虚拟主机、URL转发等等）
- 2、Tomcat是Apache组织在符合J2EE的JSP、Servlet标准下开发的一个JSP服务器

一般使用Apache+Tomcat的话，Apache只是作为一个转发，对JSP的处理是由Tomcat来处理的。

Apache可以支持php/cgi/perl,但是要使用java的话，你需要Tomcat在Apache后台支撑，将java请求由Apache转发给Tomcat处理。

Apache是web服务器，Tomcat是应用（java）服务器，它只是一个servlet(jsp也翻译成servlet)容器，可以认为是Apache的扩展，但是可以独立于Apache运行。

Apache与Tomcat整合的好处是：

- 1、如果客户端请求的是静态页面，则只需要Apache服务器响应请求
- 2、如果客户端请求动态页面，则是Tomcat服务器响应请求
- 3、因为JSP是服务器端解释代码的，这样整合就可以减少Tomcat的服务开销

Apache是一辆卡车，上面可以装一些东西如html等。但是不能装水，要装水必须要有Tomcat这个桶，而这个桶也可以不放在卡车上。

## 七、MySQL/MariaDB/PostgreSQL、

MySQL、MariaDB 和 PostgreSQL 都是常用的关系型数据库管理系统（RDBMS）。

MySQL 是一种开源关系型数据库管理系统，最初由瑞典 MySQL AB 公司开发。MySQL 以其高性能、可靠性和易用性而闻名，并被广泛应用于 Web 应用程序和企业级软件系统中。

MariaDB 是一个 MySQL 分支，最初由 MySQL 的创始人之一创建，旨在提供一个具有更好性能和安全性的替代品。MariaDB 基本上与 MySQL 兼容，并且可以直接使用现有的 MySQL 数据库和代码。

PostgreSQL 是另一种流行的开源关系型数据库管理系统，它支持 SQL 标准并提供了许多先进的功能，如事务处理、并发控制、触发器等。它被广泛应用于企业级应用程序、数据仓库等领域。

### 安装

服务器环境

CentOS7 x86_64

```
[root@slave2 yum.repos.d]# uname -a
Linux slave2 3.10.0-1062.el7.x86_64 #1 SMP Wed Aug 7 18:08:02 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
[root@slave2 yum.repos.d]# cat /etc/redhat-release
CentOS Linux release 7.7.1908 (Core)
[root@slave2 yum.repos.d]#
```

安装mariadb

mariadb的下载地址是：404 | MariaDB

建议采用yum的方式去安装，通过yum安装前最好把/etc/my.cnf文件删除掉，默认数据文件放在/var/lib/mysql目录里，安装前最好也把/var/lib/mysql删除掉避免安装后启动失败(我就是因为好几次没删除干净导致安装失败)。在/etc/yum.repos.d目录下创建MariaDB.repo文件，内容如下

用中科大的镜像网站去下载比官网的快多了！！！

```
# MariaDB 10.4 CentOS repository list - created 2020-02-25 13:00 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://mirrors.ustc.edu.cn/mariadb/yum/10.4/centos/7/x86_64/
gpgkey=https://mirrors.ustc.edu.cn/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

然后执行命令 yum -y install MariaDB-server MariaDB-client

如果中间报错 Delta RPMs disabled because /usr/bin/applydeltarpm not installed，则可以通过执行yum -y install deltarpm去解决。

查看/启动/停止/开机启动/开机禁止命令如下

```
systemctl status/start/stop/enable/disable mariadb
```

Connector（驱动包）

驱动包可以参考官网去下载MariaDB-Connector

```
driverClassName = "org.mariadb.jdbc.Driver"
```

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOK4KdIbRHTiae1VwMzgeWsukPrZMNgPXTLpicjDELzxkHITV311AHnqGw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

安装mysql

和上面安装MariaDB一样，安装前先删除掉文件/etc/my.cnf和目录/var/lib/mysql避免安装后启动失败。
一样从中科大镜像网站下载，新建mysql.repo文件，内容如下

```
#
[mysql]
name = mysql
baseurl = https://mirrors.ustc.edu.cn/mysql-repo/yum/mysql-5.7-community/el/7/x86_64
gpgkey = https://mirrors.ustc.edu.cn/mysql-repo/RPM-GPG-KEY-mysql
gpgcheck = 1
```

然后执行命令`yum -y install mysql-server`

查看/启动/停止/开机启动/开机禁止命令如下，注意后面是`mysqld`

```
systemctl status/start/stop/enable/disable mysqld 
```

安装后会有一个临时密码会存放到`/var/log/mysqld.log`文件里

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

如果要修改成简单的密码，如 set password for root@localhost = password('root');

那么会报错 ERROR 1819 (HY000): Your password does not satisfy the current policy requirements

对于8.0版本的mysql，最好是通过alter user来修改用户的密码

如alter user 'root'@'%' identified by 'root123';，最好是添加with mysql_native_password

如alter user 'root'@'%' identified with mysql_native_password by 'root123';

这是由于mysql8.0默认用的Authentication Plugin是caching_sha2_password，而以前的mysql版本默认用的是with mysql_native_password，所以添加密码或者修改密码时最好使用with mysql_native_password这样就能和以前保持一样，且能正常使用Navicat Premium 或者SQLyog

对于5.7版本的mysql，解决方法如下：

```
set global validate_password_policy=0;
set global validate_password_length=1;
```

对于8.0版本的mysql，解决方法如下。

下面的设置`validate_password.length=1`的语句可能是不成功的，貌似最低将成长度为4。但是我们不是运维，不要考虑这些细节，要把握重点，分清主次关系。密码设置为`root`不行的话就设置成为`root123`吧。

```
SHOW VARIABLES LIKE 'validate_password%';
set global validate_password.policy=0;
set global validate_password.length=1;
```

执行上面的命令后再修改密码即可成功。通过mavenMysql-Connector去下载

Connector（驱动包）

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.38</version>
</dependency>
```



```
driverClassName = "com.mysql.jdbc.Driver"
jdbcUrl = "jdbc:mysql://slave2:3306/hive?createDatabaseIfNotExist=true"
```

安装postgresql

最好先删除目录 /var/lib/pgsql，新建 postgresql.repo 文件，内容如下：

```
[postgresql]
name = postgresql
baseurl = https://mirrors.tuna.tsinghua.edu.cn/postgresql/repos/yum/12/redhat/rhel-7.7-x86_64
gpgkey= https://mirrors.tuna.tsinghua.edu.cn/postgresql/repos/yum/RPM-GPG-KEY-PGDG-12
gpgcheck = 1
```

然后执行命令 yum install postgresql-server，查看/启动/停止/开机启动/开机禁止命令如下，注意后面是postgresql 。

```
systemctl status/start/stop/enable/disable postgresql
```

默认会创建用户`postgres`，启动服务后切换用户`postgres`然后再执行`psql`即可登录到客户端

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOrL1Qwk0baGoWnM9E9VXd5qMI38icYIVI15I0wxVjibNqYbkRy6txmWTw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

下面是常用的基本命令，注意每个sql命令必须以分号结尾，字符用单引号：

```
# 创建用户test并设置密码为test
create user root with password 'root';
# 创建数据库test
create database test;
# 赋予权限
GRANT ALL PRIVILEGES ON DATABASE test TO root;
# 查看版本信息
select version();
# 查看所有数据库
\l
# 切换到hive数据库
\c hive
# 查看当前库所有的表
select * from pg_tables where schemaname='public';
```

如果想要从其他机器连接到postgresql服务，需要修改两个配置文件

`/var/lib/pgsql/data/postgresql.conf`文件添加如下内容，该配置在原文件里是注释掉了

```
# 在所有IP地址上监听，从而允许远程连接到数据库服务器
listen_addresses = '*'
```

`/var/lib/pgsql/data/pg_hba.conf`文件

```
# 允许任意用户从任意机器上以密码方式访问数据库
host    all             all             0.0.0.0/0                md5
```

Connector（驱动包）

查看Postgresql-Connector

```
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.2.5</version>
</dependency>
```



```
driverClassName = "org.postgresql.Driver"
jdbcUrl = "jdbc:postgresql://slave2:3306/hive?createDatabaseIfNotExist=true"
```

## 八、PHP

PHP（全称为“Hypertext Preprocessor”）是一种流行的开源服务器端脚本语言，主要用于 Web 开发。它最初由 Rasmus Lerdorf 在1994年创建，并在其后逐步发展成一个成熟的编程语言。PHP 可以嵌入 HTML 页面中，在服务器端执行脚本代码，生成动态网页内容并将其发送到客户端浏览器。

PHP 语言具有简单易学、开发效率高、功能强大和跨平台等特点。它支持众多数据库类型，如 MySQL、Oracle 和 PostgreSQL 等，并且可以与许多不同的 Web 服务器软件进行集成，如 Apache、Nginx 等。此外，PHP 还提供了大量的扩展库和框架，方便开发人员快速构建复杂的 Web 应用程序。

PHP是能让你生成动态网页的工具之一。PHP网页文件被当作一般HTML网页文件来处理并且在编辑时你可以用编辑HTML的常规方法编写PHP。

PHP代表：超文本预处理器（PHP: Hypertext Preprocessor）。PHP是完全免费的，不用花钱，你可以从PHP官方站点(http://www.php.net)自由下载。PHP遵守GNU公共许可（GPL)，在这一许可下诞生了许多流行的软件诸如Linux和Emacs。你可以不受限制的获得源码，甚至可以从中加进你自己需要的特色。PHP在大多数Unix平台，GUN/linux和微软Windows平台上均可以运行。

### 8.1环境搭建

首先我们需要先安装好apache,我这里用的是appserver来安装的。如果想要上传要公网的服务器上的话可以使用cygwin、ftp，我这里使用的集成IDE是phpstorm,感觉还是非常方便的，这种IDE的风格和androidStudio的都差不多，所以上手非常快，而且可以自动找到浏览器，总之是一款非常不错的IDE。安装配置这里不再重复啰嗦！

常见的名词：

- cygwin:在windows中模拟linux的环境。
- apache httped：服务器。
- Nginx：服务器。
- xampp：应用服务器，快速搭建开发环境。
- phpStorm：php集成开发环境。
- ftp:协议，上传文件。
- ssh：一个命令，连接服务器。
- scp:一个命令，上传和下载文件。

### 8.2php基本语法

在phpstorm中新建一个工程HelloPHP,然后建一个文件夹base,在里面新建一个cc.php，格式就是：

```
 <?php
        echo 'hello php'
```

在php中，所有用户定义的函数都对大小写不敏感，但是在所有变量对大小写敏感。

常量和变量、数组、函数

我们使用符号来定义变量，在php中很多地方都用到了符号来定义变量，在php中很多地方都用到了,感觉有点像jQuery了，呵呵!

声明变量：

```
$a=10;
    $a=20;
    $b=5;
    echo $a+$b;
```

如果要定义常量的话可以使用：

```
const  THE_VALUE=100;
    echo  THE_VALUE;
```

也可以用函数来传值：

```
function traceNum($a,$b)
    {
    echo "a=$a,b=$b";
    }
    traceNum(3,4);
```

常量只能被赋值一次，而变量可以赋值多次。

流程控制、循环

php的流程控制可以使用if else来处理以及switch，和java类似，可以使用break和continue来控制循环.

下面是一个if循环的例子，这里注意的是elseif是连在一起写的，不要分开，和Oracle中的存储函数类型，存储函数就是elsif来控制的，真的很像，呵呵！

```
function getLevel($score){
    if($score>90){
    return '优秀';
    }elseif($score>80){
    return '良好';
    }elseif($score>60){
    return '合格';
    }else{
    return '不合格';
    }
    }
    echo getLevel(93);
```

如果使用switch的话可以这样：

```
function getLevel($score){

    $result='不合格';
    switch(intval($score/10)){
    case 10;
    case 9:
    $result='优秀';
    break;
    case 8:
    $result='良好';
    break;
    case 7:
    $result='好';
    break;
    case 6:
    $result='合格';
    break;
    default:
    $result='不合格';
    break;
    }
    return $result;


    }
    echo getLevel(93);
```

类、方法

新建一个类：

```
<?php      class Hello{     public function sayHello(){     echo 'hello';     }     }
```

这个地方和java非常相似啦，我就不说了！

就是引入文件使用：require,或者require_once

```
 include  'demo1.php';  //包含，如果没有不会报错。
    require  'demo1.php';  //依赖 ，如果没有就报错

    //同一个php在不同的地方重复引用，
    require_once  'demo1.php';
```

新建一个man类，构造方法。

```
  class Man
    {
    /**
     * @param $age年龄
     * @param $name   名字
     *
     */
    public  function __construct($age,$name){
       // echo 'Construce  a man';
    $this->_age=$age;
    $this->_name=$name;
    }

    public function getAge(){
    return $this->_age;
    }
    public function getName(){
    return $this->_name();
    }
    private $_age,$_name;

    public static function sayHello(){
    echo 'hello man';
    }

    }
```

库函数

获取时间：

```
 //获取时间
    //echo  time();

    date_default_timezone_set('Asia/Shanghai');
    //日期
    echo  date('Y-m-d H:i:s');
```

操作json

```
//生成json格式的数据
    $arr=array(1,2,3,5,7,'hello');
    echo json_encode($arr);

    $obj=array('h'=>'hello','w'=>'world',array(3,4,5,7));

    echo json_encode($obj);

    //解码
    $jsonStr="{\"h\":\"hello\",\"w\":\"world\",\"0\":[3,4,5,7]}";
    $obj=json_decode($jsonStr);

    echo $obj->h;
```

创建图片

```
$img=imagecreate(400,300);
    imagecolorallocate($img,255,255,255);
    header('Content-type:image/png');
    imageellipse($img,200,200,50,50,imagecolorallocate($img,255,0,0));
    imagepng($img);
```

为图片添加水印

```
$img=imagecreatefrompng('img.png');

    imagestring($img,5,5,5,'www.tianfang1314.cn',imagecolorallocate($img,255,0,0));

    header('Content-type:image/png');
    imagepng($img);
```

操作文本

把数据写到data的文本中：

```
$f=@fopen('data','w');
    fwrite($f,'hello php');
    fclose($f);
```

把数据从data的文本中读取出来：

```
$f=@fopen('data','r');

    while(!feof($f)){
    $content=fgets($f);
    echo $content;
    }

    fclose($f);
```

输出内容：

```
echo file_get_contents('data');
```

上传文件：

html页面端：

```
<form  action="upload.php"  method="post"  enctype="multipart/form-data">
          <input type="file"  name="file"  >
            <input type="submit" value="提交" />
        </form>
```

php端：

```
 $file=$_FILES['file'];
    $fileName=$file['name'];
    move_uploaded_file($file['tmp_name'],$fileName);
```

## 九、Python

Python是一种高级编程语言，由Guido van Rossum在1989年底发明，并在1991年公开发布。它以简单、易读、易学的特点受到了广泛的欢迎和应用。Python具有动态类型、解释性和面向对象等多种特性，被广泛应用于Web开发、数据分析、人工智能等领域。同时，Python还拥有丰富的第三方库和生态系统，使得Python成为了最流行的编程语言之一。

Python在各个编程语言中比较适合新手学习，Python解释器易于扩展，可以使用C语言或C++（或者其他可以通过C调用的语言）扩展新的功能和数据类型。Python也可用于可定制化软件中的扩展程序语言。Python丰富的标准库，提供了适用于各个主要系统平台的源码或机器码。

### 9.1安装Python3.8

目前，Python有两个版本，一个是2.x版，一个是3.x版，这两个版本是不兼容的。由于3.x版越来越普及，我们的教程将以最新的Python 3.8版本为基础。请确保你的电脑上安装的Python版本是最新的3.8.x，这样，你才能无痛学习这个教程。

在Mac上安装Python

如果你正在使用Mac，系统是OS X>=10.9，那么系统自带的Python版本是2.7。要安装最新的Python 3.8，有两个方法：

方法一：从Python官网下载Python 3.8的安装程序，下载后双击运行并安装；

方法二：如果安装了Homebrew，直接通过命令`brew install python3`安装即可。

在Linux上安装Python

如果你正在使用Linux，那我可以假定你有Linux系统管理经验，自行安装Python 3应该没有问题，否则，请换回Windows系统。对于大量的目前仍在使用Windows的同学，如果短期内没有打算换Mac，就可以继续阅读以下内容。

在Windows上安装Python

首先，根据你的Windows版本（64位还是32位）从Python的官方网站下载Python 3.8对应的64位安装程序或32位安装程序，然后，运行下载的exe安装包：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOpGYicxt17O9cY0iaQaacVYM507fsJWrxDlic5xZBqldicGB4LnZqy9kZkw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

特别要注意勾上`Add Python 3.8 to PATH`，然后点“Install Now”即可完成安装。

运行Python

安装成功后，打开命令提示符窗口，敲入python后，会出现两种情况：

情况一：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOQ3cJq7vnuPuT1GMRib4N7BERL1SWyjLvpxibOUEF6enLScm2LpCnKNsw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

看到上面的画面，就说明Python安装成功！

你看到提示符`>>>`就表示我们已经在Python交互式环境中了，可以输入任何Python代码，回车后会立刻得到执行结果。现在，输入`exit()`并回车，就可以退出Python交互式环境（直接关掉命令行窗口也可以）。

情况二：得到一个错误：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/dkX7hzLPUR0QAIT5ZrNVkASSTNxD6icfOicvesMXjv6WIhibgmOtNmn5nENYibxURKSfzJxdzYSlX7YpO7Drt3OwRw/640?wx_fmt=other&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这是因为Windows会根据一个Path的环境变量设定的路径去查找python.exe，如果没找到，就会报错。如果在安装时漏掉了勾选Add Python 3.8 to PATH，那就要手动把python.exe所在的路径添加到Path中。

如果你不知道怎么修改环境变量，建议把Python安装程序重新运行一遍，务必记得勾上Add Python 3.8 to PATH。

## 十、Perl

Perl是一种高级的通用编程语言，由Larry Wall在1987年创建。它具有强大的文本处理能力和灵活的特性，在Unix/Linux系统上得到了广泛应用。Perl被设计为一种实用主义语言，可以轻松地完成各种任务，包括文本处理、系统管理、网络编程、Web开发等方面。尽管Perl的流行度已经逐渐下降，但它仍然是许多领域中值得学习的编程语言之一。

Perl易于使用、高效、完整，而不是美观（小巧，优雅，简约）。同时支持过程和面向对象编程，对文本处理具有强大的内置支持，并且拥有第三方模块集合之一。Perl借取了C、sed、awk、shell脚本语言以及很多其他程序语言的特性，其中最重要的特性是它内部集成了正则表达式的功能，以及巨大的第三方代码库CPAN。

### 10.1主要功能

Perl最初的设计者为拉里·沃尔(Larry Wall)，他于1987年12月18日发表。Perl借取了C、sed、awk、shell 脚本语言以及很多其他程序语言的特性。其中最重要的特性是它内部集成了正则表达式的功能，以及巨大的第三方代码库CPAN。

Perl它是术语，而不仅仅是简写，Perl的创造者，Larry Wall提出第一个，但很快又扩展到第二个。那就是为什么‘’Perl‘’没有所有字母都大写。没必要争论哪一个正确，Larry两个都认可。

特点

Perl是由Larry Wall设计的，并由他不断更新和维护的编程语言。

Perl具有高级语言(如C)的强大能力和灵活性。事实上，你将看到，它的许多特性是从C语言中借用来的。

Perl与脚本语言一样，Perl不需要编译器和链接器来运行代码，你要做的只是写出程序并告诉Perl来运行而已。这意味着Perl对于小的编程问题的快速解决方案和为大型事件创建原型来测试潜在的解决方案是十分理想的。

Perl提供脚本语言(如sed和awk)的所有功能，还具有它们所不具备的很多功能。Perl还支持sed到Perl及awk到Perl的翻译器。

简而言之，Perl像C一样强大，像awk、sed等脚本描述语言一样方便。

开源

Perl的解释程序是开放源码的免费软件，使用Perl不必担心费用。Perl能在绝大多数操作系统运行，可以方便地向不同操作系统迁移。

Perl是一种能完成任务的语言。从一开始，Perl就设计成可以把简单工作简单化，同时又不失去处理困难问题能力的语言。它可以很容易操作数字，文本，文件和目录，计算机和网络，特别是程序的语言。这种语言应该很容易运行外部的程序并且扫描这些程序的输出获取感兴趣的东西。而且它还应该很容易能把这些你感兴趣的东西交给其它程序做特殊的处理。当然，这种语言还应该很容易在任何现代的操作系统上可以移植地编译和运行。

语法

- 变量定义，以$号开头，如：$num =1；
- 数组定义，以@开头，如：@array = (1，2，3)；
- 数组元素调用 $array[index]，其中index表示数组下标，如上例，$array[0]的值是1
- 哈希定义，以%开头，如：%hash=("a"，1，"b"，2)；
- 哈希调用 %hash，其中key表示键，多用字符串表示，注意hash的key必须具有独一性，但value可以不独一，为此hash的key经常被用来做独一化处理，如上例中的"a"， "b"， values是key对应的值，如1，2。$hash{"b"}的值是2。

优点

Perl追求的是简单， 解决一个一般的问题用它几行代码就完成了. 一个稍复杂一点的问题代码也不会超过一屏! 在软件测试中，Perl通常是非常重要的角色。一般一个测试通用函数库就要分十几个文件，甚至更多，包含多达上千个定制功能。而这些函数将在主函数运行时，不定数量的被调用。几乎可以说，一切自动过程都是由Perl自己完成的，可见其功能的强大和在当今计算机技术高速发展的时期仍然发挥着重要的作用。

Perl最初是当做一种Unix的脚本语言设计的，但是它早就移植到大多数其它操作系统里了。因为Perl几乎可以在任何地方运行，所以Perl可以说是当今最具有移植性的编程环境；要想写可移植的C/C++程序，你得在程序里加上一大堆 #ifdef标签来区分不同的系统；要想写可移植的Java程序，你必须理解每种新的Java实现的特质；要想写可移植的shell，你可能要记住每条命令在每种操作系统上的语法，走运的时候你可能可以找到一些公共的东西；要想写可移植的Visual Basic程序，需要对‘’移植‘’有个更灵活的定义。

让我们很高兴的是Perl避免了所有这些问题，同时还保留了这些语言中的许多优点，同时还有一些自己的特色。Perl的特色来自许多方面：它的特性集的工具，Perl社区的创造性，以及开源运动的大环境。不过，许多这些特性都是混合的东西；Perl的身世复杂，它总是把事物看成是优点的不同方面，而不是弱点。Perl是‘’背黑锅我来‘’的语言。如果你觉得自己陷入一团乱麻之中，非常渴望自由，那么请使用Perl。

Perl是跨文化的。Perl的爆炸性增长很大程度上是因为那些前Unix系统程序员的渴望，他们希望从他们的‘’老家‘’带着尽可能多的东西。对于他们而言，Perl是可移植的Unix化蒸馏器，是"此路不通"的沙漠中的绿洲。从另外一个角度来看，Perl还可以从另外一个方向运转：在Windows上工作的web设计者通常会非常开心地发现他们的 Perl程序可以不加修改地在Unix服务器上跑。

尽管Perl在系统程序员和web设计师中间非常流行，但这只是因为是他们最早发现Perl的，Perl可以用于更广泛的用途。从Perl最早的文本处理语言开始，它已经发展成为一种非常复杂的，通用的编程语言，以及完整的开发环境，包括调试器，调节器，交叉引用，编译器，库，语法提示编辑器，以及所有其它‘’真正‘’的编程语言所具有的所有挂勾，只要你需要。当然这些东西都是让我们可能处理难的问题的东西，而且很多其它语言也可以做到这一点。Perl之所以成为Perl是因为它从来不会因为保持简单事情简单化而丢失其他方面的特性。

因为Perl既强大又好用，所以它被广泛地用于日常生活的方方面面，从宇航工程到分子生物学，从数学到语言学，从图形处理到文档处理，从数据库操作到网络管理。很多人用Perl进行快速处理那些很难分析或转换的大批量数据，不管你是处理DNA序列，网页，还是猪肚皮的未来都无所谓。实际上，在Perl社区有一个笑话就是，下次股市大崩盘就很有可能是哪个家伙写的脚本里头有bug造成的。(不过，乐观点来看就是，任何还在失业的股票分析师仍然有可以利用的技巧。)

Perl的成功有许多原因。Perl早在开源软件的名字出现之前就已经是一个成功的开源项目了。Perl是自由的，并将永远自由下去。你可以在任何合适的场合使用 Perl，只需要遵守一个非常自由的版权就可以了。如果你在从事商业活动并且还想使用Perl，那么用就是了。你可以把Perl嵌入到你写的商业软件中而不需要支付任何费用也没有任何限制。如果你碰上一个Perl社区解决不了的问题，那你也还有最后的一招：源程序本身。 Perl社区不会在‘’升级‘’的伪装下租给你它们的商业秘密。而且Perl社区也不会‘’停业 ‘’，更不会让你孤立无援。

Perl是自由软件这一点无疑对它是有帮助的。但这一条并不足以解释Perl现象，因为许多自由软件包没有能繁荣起来。Perl不仅自由；而且好玩。人们觉得自己在Perl里可以有创造力，因为它们有表达的自由：他们可以选择是为计算机速度优化还是为程序员的速度优化，是冗长还是简洁，是选择可读性还是可维护性，或者选择复用性，移植性，接受性和传授性等等。假如你进入一次模糊的Perl比赛，甚至你还可以为模糊性做优化。

Perl可以给予你所有这些自由，因为它是一门有着分裂人格的语言。Perl同时是很简单并且很富有的语言。Perl从其它地方拿来好主意，然后把它们安装到易用的框架里面。对于只是喜欢她的人来说，Perl是实用抽取和报表语言(Practical Extractoin and Report Language)。对那些热爱她的人而言，她是变态电子垃圾制造者(Pathologically Electric Rubbish Lister)。在少数人眼里，Perl是毫无意义的重复练习。不过世界需要一点点冗余。精简主义者总是想把事物分隔开。而我们则总是企图把它们合并到一起。

Perl之所以是简单的语言是有很多原因的。比如你用不着知道什么特殊的指令就可以编译Perl程序--只要把它当做批处理或者 shell脚本执行就可以了。Perl的类型和结构很容易使用和理解。Perl对你的数据没有任何限制--你的字串和数组可以要多长就多长(只要你有足够的内存)，而且它们都会自动增长。Perl不会强迫你学习新的语法和语意，Perl改从许多其它你已经熟悉的语言里(比如C， awk， BASIC 和 Python， 英文，希腊语等)借来语法。实际上，任何程序员都可以从书写良好的Perl代码段中读懂它的含义。

最重要的是，你不用先学习所有Perl的东西就可以开始写有用的程序。你可以写很小的Perl程序。你也可以象小孩那样写Perl程序，保证不会笑话你。或者更准确地说是，绝不会笑话小孩做事情的创造性。Perl里的许多观点都是从自然语言中借来的，其中一条最好的观点就是只要你能把自己的意思表述清楚，那么你就可以使用这些语言的一个子集。Perl文化可以接受任何熟练程度的成员。不会在你背后放个语言警察。如果你的老板不炒你，而且你的Perl脚本也能完成工作，那么它就是‘’正确‘’的。

尽管Perl很简单，但它仍然是一种特性很丰富的语言，如果你想用那些特性的话，那你就要学习一些东西。这也是把难题变简单的学费。虽然你要想把所有Perl能做的事情吸收还需要一些时间，但到你需要这些功能的时候你就会非常开心地发现Perl已经可以做这些事情了。

由于Perl的继承性，就算它只是用做数据归纳语言的时候也有丰富的特性，Perl一开始就设计成可以浏览文件，扫描大量文本并且生成动态数据以及打印出这些数据的良好格式化的报表。不过，随后 Perl 就开始风行，于是它就成了可以操作文件系统，进程管理，数据库管理，进行C/S编程和安全编程，web信息管理，甚至可以进行面向对象和面向功能的编程的语言。而且这些功能并非只是在Perl这边，每种新功能都和其它东西交流得很好，别忘了Perl从一开始就是设计成胶水语言的。

而且Perl并不仅仅只能黏合它自己的特性。Perl是设计成可以用模块扩展的语言。你可以用Perl快速设计，编写，调试和部署Perl应用，并且你还可以在需要的时候很方便地扩展这些应用。你可以在其它语言里嵌入Perl，而且你也可以在Perl里嵌入其它语言。通过模块输入机制，你可以把这些外部的扩展当做内置于Perl的特性。那些面向对象的外部库在Perl内部仍然保持面向对象的特征。

Perl还在许多其它方面协助你。和严格的每次执行一条命令的命令文件和shell脚本不同的是，Perl先把你的程序快速编译成一种内部格式。和其它任何编译器一样，这个时候还进行各种优化，同时把碰到的任何问题反馈给你。一旦Perl的编译器前端对你的程序表示满意了，它就把这些中间代码交给解释器执行(或者是给其它的能生成C或者字节码的模块后端)。听起来挺复杂，不过Perl的编译器和解释器干这些活效率相当高，编译-运行-修改的过程几乎都是以秒计。再加上Perl的许多其他开发特性，这种快速的角色转换很适合做快速原型设计。然后随着你的程序的成熟，你可以逐步拧紧身上的螺母，减少散漫增强纪律。如果你做得好，Perl也能帮你这个忙。

Perl还可以帮你写更安全的程序。除了其它语言提供的典型的安全接口之外，Perl还通过一种跟踪数据的机制给你提供预防意外安全错误的保护，这样就可以在灾害发生之前预防其发生。最后，Perl还可以让你设置一个特殊的防护隔段运行那些来源不明的Perl代码，以此来杜绝危险操作。

不过，偏执一点儿说，Perl 帮你的大部分内容和Perl本身没有什么关系，而是和使用Perl的人有关。坦率地说，Perl社区的人们可以说是地球上最热心的人了。如果Perl运动里面有那么一点点宗教色彩的话，那么这就是它的核心了。Larry希望Perl社区像一小片天堂那样运转，看来他的愿望基本上是实现了。也请你为此做出自己的努力。

Perl之所以强大， 是因为有CPAN， CPAN上面有无数的开源模块， 从科学计算到桌面应用到网络等等各个方面都有大量的模块! 并且世界上也还有无数的人在向上面添加模块! 如果你想要用PERL实现某功能， 不用自己做， 在CPAN上面搜一搜， 多半都会得到已有的结果! CPAN("the Comprehensive Perl Archive Network"全面的Perl存档网络)是查找任何Perl有关的东西的中心仓库。它包含从整个Perl社区收集来的智慧：成百上千的Perl模块和脚本，相当于好几本书的文档，以及整个Perl发布。如果有东西是用Perl写的，而且这个东西很有用而且是自由的，那么它很有可能就在CPAN上。

缺点

也正是因为Perl的灵活性和‘’过度‘’的冗余语法，也因此获得了write-only的‘’美誉‘’，因为许多Perl程序的代码令人难以阅读，实现相同功能的程序代码长度可以相差十倍百倍。但Perl同样可以将代码书写得像Python或Ruby等语言一样优雅。

很多时候，perl.exe进程会占用很多的内存空间，虽然只是一时，但是感觉不好。

讲述了Perl的构成和特点，并且穿插着Perl本身实现的方方面面的设计思想，举个例子来说就是引入了语言环境的做法，这种语言层次的语言环境让程序员在写程序的时候更多地像是在‘’说‘’，而不是在‘’解释‘’，我甚至可以说理解语言环境是了解和掌握Perl的一个关键等内容。





