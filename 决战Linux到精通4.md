# vim全套笔记
## VIM快速复习
### 什么是 vim？
Vim是从 vi 发展出来的一个文本编辑器。代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。vim 的官方网站 (http://www.vim.org)

vim 键盘图：

![image](https://github.com/user-attachments/assets/7096f023-9ca0-4feb-b429-797b87e0133f)


基本上vi可以分为三种状态：

- 命令模式（command mode)
- 插入模式（Insert mode)
- 底行模式（last line mode)

## 按:冒号即可进入last line mode

```txt
:set nu 列出行号
:set nonu	取消行号
:#7 跳到文件中的第7行
/keyword 查找字符  按n向下
?keyword 查找字符  按N向下
:n1,n2/word1/word2/gc  替换指定范围单词，c表示提示
:w 保存文件
:w filename 以指定的文件名另存
:n1,n2 w [filename]	将 n1 到 n2行另存
:r [filename]	读入另一个文件加到光标所在行后面
:! ls /home  在vi当中察看ls输出信息！
:q离开vi
:wq 和 :ZZ 和 :x 保存并退出vi
!强制执行
:% s/^/#/g 来在全部内容的行首添加 # 号注释
:1,10 s/^/#/g 在1~10 行首添加 # 号注释  
```

## 从command mode进入Insert mode
按i在当前位置编辑

按a在当前位置的下一个字符编辑

按o插入新行，从行首开始编辑

按R(Replace mode)：R会一直取代光标所在的文字，直到按下 ESC为止；(常用)

## 按ESC键退回command mode
h←j↓k↑l→前面加数字移动指定的行数或字符数

1、翻页bu上下整页，ud上下半页

```txt
ctrl+b：上移一页。
ctrl+f：下移一页。
ctrl+u：上移半页。
ctrl+d：下移半页。
```

2、行定位

```txt
7gg或7G：定位第7行首字符。(可能只在Vim中有效)
G：移动到文章的最后。
7H:当前屏幕的第7行行首
M：当前屏幕中间行的行首
7L:当前屏幕的倒数第7行行首
```

3、当前行定位

```txt
$：移动到光标所在行的“行尾”。
0或^：移动到光标所在行的“行首”
w：光标跳到下个单词的开头
e：光标跳到下个单词的字尾
b：光标回到上个单词的开头
```

4、编辑

```txt
x：剪切当前字符
7x：剪切从当前位置起7个字符
大写的X，表示从前面一个字符开始往前计算
dd：剪切光标所在行。
7dd：从光标所在行开始剪切7行
d7G	删除光标所在到第7行的所有数据
yw：复制当前单词
7yw：复制从当前位置起7个单词
yy：复制当前行
6yy：从当前行起向下复制6行
y7G	复制游标所在列到第7列的所有数据
p：粘贴
u：撤销
ctrl+r：取消撤销
cw：删除当前单词(从光标位置开始计算)，并进入插入模式
c7w：删除7个单词并进入插入模式
```

## 多行编辑，vim支持，vi不支持
按ctrl+V进入块模式，上下键选中快，按大写G选择到末尾，上下左右键移动选择位置

按大写I进去编辑模式，输入要插入的字符，编辑完成按ESC退出

选中要替换的字符后，按c键全部会删除，然后输入要插入的字符，编辑完成按ESC退出

选中要替删除的字符后，按delete键，则会全部删除

按shift+V可进入行模式，对指定行操作


## vim练习
1、创建目录/tmp/test，将/etc/man.config复制到该目录下

```txt
# mkdir -p /tmp/test

# cp /etc/man.config /tmp/test/

# cd /tmp/test/
```

2、用vim编辑man.config文件：

```txt
vim man.config
```

3、设置显示行号； 移动到第58行，向右移动40个字符，查看双引号内的是什么目录；

```txt
：set nu
58G 或58gg 
40-> 或40空格 目录为：/dir/bin/foo 
```

4、移动到第一行，并向下查找“bzip2”这个字符串，它在第几行；

```txt
移动到最后一行，并向上查找该字符串；
gg 或1G
/bzip 137行 ?bzip2
```

5、将50行到100行之间的man更改为MAN，并且 逐个挑选 是否需要修改；

```txt
若在挑选过程中一直按y，结果会在最后一行出现改变了几个man?
:50,100s/man/MAN/gc 25次替换
```

6、修改完后，突然反悔了，要全部复原，有哪些方法？

```txt
一直按u键	
或者
:q!强制不保存退出后，再重新打开该文件
```

7、复制65到73这9行的内容（含有MANPATH_MAP），并且粘贴到最后一行之后；

```txt
65gg或65G到该行后，9yy,G 移动到最后一行，p粘贴
```

8、21行到42行之间开头为#符号的批注数据不要了，如何删除；

```txt
21G到该行 22dd
```

9、将这个文件另存为man.test.config的文件

```txt
:w man.test.config
```

10、到第27行，并且删除15个字符，结果出现的第一个字符是什么？

```txt
27gg 后15x
```

11、在第一行新增一行，在该行内输入“I am a student ”

```txt
gg到第一行 O输入即可 说明：o是在当前行之后插入一行，O是在当前行之前插入一行
```

12、保存并退出

```txt
:wq
```


## vi/vim的三种模式
vi/vim主要分为三种模式，分别是**命令模式（Command mode），输入模式（Insert mode）和底线命令模式（Last line mode）。**

![image](https://github.com/user-attachments/assets/d4fa63df-06cf-4d86-ac93-ae4fb16c9f04)

这三种模式的作用分别是：

### 命令模式
用户刚刚启动 vi/vim，便进入了命令模式。 任何时候，不管用户处于何种模式，只要按一下ESC键，即可使Vi进入命令模式；

此状态下敲击键盘动作会被Vim识别为命令，输入: 可切换到**底线命令模式**，以在最底一行输入命令。

若想要编辑文本：启动Vim，进入了命令模式，按下i，切换到输入模式。

### 输入模式
在命令模式下输入插入命令i、附加命令a 、打开命令o、修改命令c、取代命令r或替换命令s都可以进入文本输入模式。在该模式下，用户输入的任何字符都被Vi当做文件内容保存起来，并将其显示在屏幕上。在文本输入过程中，若想回到命令模式下，按键ESC即可。

### 底行模式
在命令模式下按下:（英文冒号）就进入了底行命令模式。

底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。

在底线命令模式中，基本的命令有（已经省略了冒号）：

- q 退出程序
- w 保存文件

按ESC键可随时退出底线命令模式。

# vim基础操作
## 进入输入模式(Insert mode)

![image](https://github.com/user-attachments/assets/1a4d9678-91e1-47a2-bef4-660dd491c184)

i: 插入光标前一个字符

I: 插入行首

a: 插入光标后一个字符

A: 插入行未

o: 向下新开一行,插入行首

O: 向上新开一行,插入行首


在进入输入模式后， vi 画面的左下角处会出现『–INSERT–』的字样

## 进入替换模式(Replace mode)
- r : 只会取代光标所在的那一个字符一次
- R: 会一直取代光标所在的文字，直到按下ESC为止

在进入输入模式后， vi 画面的左下角处会出现『–REPLACE–』的字样

## 命令模式下常用命令
### 移动光标

![image](https://github.com/user-attachments/assets/6d28da77-a7ea-4fe9-b933-420a581274ff)


### 删除操作

![image](https://github.com/user-attachments/assets/fd08d271-7520-44f0-a843-715e5ffaa008)

### 撤销&复原&重复

![image](https://github.com/user-attachments/assets/2ff7ddf7-1e3d-486f-9e17-103da90f40f7)

### 复制&粘贴

![image](https://github.com/user-attachments/assets/e1b03421-5d91-4722-8a36-220b4a9f4280)


### 合成行
- J: 将光标所在行与下一行的数据结合成同一行

### 搜索

![image](https://github.com/user-attachments/assets/c38ded3a-e9e3-4cf2-88ad-ff0829893e62)

### 替换

![image](https://github.com/user-attachments/assets/89a55a5f-7245-4700-b755-283646494603)


## 底行命令模式的常用操作

![image](https://github.com/user-attachments/assets/82d997c5-a0c5-47d3-bca8-a7bb4a876ebe)


示例：

```txt
将当前路径插入到光标的下一行
:r!pwd
```

## 可视模式
v 进入字符可视化模式： 文本选择是以字符为单位的。

V 进入行可视化模式： 文本选择是以行为单位的。

Ctrl+v 进入块可视化模式 ： 选择一个矩形内的文本。

可视模式下可进行如下操作：

![image](https://github.com/user-attachments/assets/af76707b-5612-472f-a97c-655881db8e77)


可视模式下，选中的区域是由两个端点来界定的（一个在左上角，一个在右下角），在默认情况下只可以控制右下角的端点，而使用o按键则可以在左上角和右下角之间切换控制端点。

## Linux系统启动过程
Linux系统的启动过程可以分为5个阶段：

- 内核的引导。
- 运行 init。
- 系统初始化。
- 建立终端 。
- 用户登录系统。

## 加载内核
当计算机打开电源后，首先是BIOS开机自检，按照BIOS中设置的启动设备（通常是硬盘）来启动。

操作系统接管硬件以后，首先读入 /boot 目录下的内核文件。

![image](https://github.com/user-attachments/assets/445df4ef-5e1d-460e-b048-d50853266b60)



## 启动初始化进程init
内核文件加载以后，就开始运行第一个程序 /sbin/init，它的作用是初始化系统环境。

init程序首先是需要读取配置文件/etc/inittab。

![image](https://github.com/user-attachments/assets/ab80687a-f3e6-4424-8046-dbba0d2107a2)


![image](https://github.com/user-attachments/assets/72c08c05-db94-4155-a59f-366ef5868efa)


由于init是第一个运行的程序，它的进程编号（pid）就是1。其他所有进程都从它衍生，都是它的子进程。

## 确定运行级别
许多程序需要开机启动。它们在Windows叫做"服务"（service），在Linux就叫做"守护进程"（daemon）。

init进程的一大任务，就是去运行这些开机启动的程序。

但是，不同的场合需要启动不同的程序，比如用作服务器时，需要启动Apache，用作桌面就不需要。

Linux允许为不同的场合，分配不同的开机启动程序，这就叫做"运行级别"（runlevel）。也就是说，启动时根据"运行级别"，确定要运行哪些程序。

![image](https://github.com/user-attachments/assets/1a5565ff-1d69-4c82-a0d4-ff6d2032186c)

Linux系统有7个运行级别(runlevel)：

- 运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动
- 运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登陆
- 运行级别2：多用户状态(没有NFS)
- 运行级别3：完全的多用户状态(有NFS)，登陆后进入控制台命令行模式
- 运行级别4：系统未使用，保留
- 运行级别5：X11控制台，登陆后进入图形GUI模式
- 运行级别6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动

可以使用运行级别执行关机或重启：

```txt
init 0	关机
init 6	重启
```

## 加载开机启动程序
在init的配置文件中有这么一行： si::sysinit:/etc/rc.d/rc.sysinit它调用执行了/etc/rc.d/rc.sysinit，而rc.sysinit是一个bash shell的脚本，它主要是完成一些系统初始化的工作，rc.sysinit是每一个运行级别都要首先运行的重要脚本。

它主要完成的工作有：激活交换分区，检查磁盘，加载硬件模块以及其它一些需要优先执行任务。

```txt
l5:5:wait:/etc/rc.d/rc 5
```

这一行表示以5为参数运行/etc/rc.d/rc，/etc/rc.d/rc是一个Shell脚本，它接受5作为参数，去执行/etc/rc.d/rc5.d/目录下的所有的rc启动脚本，/etc/rc.d/rc5.d/目录中的这些启动脚本实际上都是一些连接文件，而不是真正的rc启动脚本，真正的rc启动脚本实际上都是放在/etc/rc.d/init.d/目录下。

而这些rc启动脚本有着类似的用法，它们一般能接受start、stop、restart、status等参数。

/etc/rc.d/rc5.d/中的rc启动脚本通常是K或S开头的连接文件，对于以 S 开头的启动脚本，将以start参数来运行。

而如果发现存在相应的脚本也存在K打头的连接，而且已经处于运行态了(以/var/lock/subsys/下的文件作为标志)，则将首先以stop为参数停止这些已经启动了的守护进程，然后再重新运行。

这样做是为了保证是当init改变运行级别时，所有相关的守护进程都将重启。

至于在每个运行级中将运行哪些守护进程，用户可以通过chkconfig或setup中的"System Services"来自行设定。

![image](https://github.com/user-attachments/assets/8a19098c-6c40-41b6-b8c8-5a1e82c89c67)


## 用户登录
一般来说，用户的登录方式有三种：

- （1）命令行登录
- （2）ssh登录
- （3）图形界面登录

![image](https://github.com/user-attachments/assets/370b2b77-3cdd-405b-acbd-942808e46e31)


对于运行级别为5的图形方式用户来说，他们的登录是通过一个图形化的登录界面。登录成功后可以直接进入 KDE、Gnome 等窗口管理器。

而本文主要讲的还是文本方式登录的情况：当我们看到mingetty的登录界面时，我们就可以输入用户名和密码来登录系统了。

Linux 的账号验证程序是login，login会接收mingetty传来的用户名作为用户名参数。

然后login会对用户名进行分析：如果用户名不是root，且存在 /etc/nologin 文件，login 将输出 nologin 文件的内容，然后退出。

这通常用来系统维护时防止非root用户登录。只有/etc/securetty中登记了的终端才允许 root 用户登录，如果不存在这个文件，则root用户可以在任何终端上登录。

/etc/usertty文件用于对用户作出附加访问限制，如果不存在这个文件，则没有其他限制。

## 图形模式与文字模式的切换方式
Linux预设提供了六个命令窗口终端机让我们来登录。

默认我们登录的就是第一个窗口，也就是tty1，这个六个窗口分别为tty1,tty2 … tty6，你可以按下Ctrl + Alt + F1 ~ F6 来切换它们。

如果你安装了图形界面，默认情况下是进入图形界面的，此时你就可以按Ctrl + Alt + F1 ~ F6来进入其中一个命令窗口界面。

当你进入命令窗口界面后再返回图形界面只要按下Ctrl + Alt + F7 就回来了。

如果你用的vmware 虚拟机，命令窗口切换的快捷键为 Alt + Space + F1~F6. 如果你在图形界面下请按Alt + Shift + Ctrl + F1~F6 切换至命令窗口。

## login shell

![image](https://github.com/user-attachments/assets/936d1ecd-7657-4903-b32a-70f7323a6a09)


shell，简单说就是命令行界面，让用户可以直接与操作系统对话。用户登录时打开的shell，就叫做login shell。

（1）命令行登录：首先读入 /etc/profile，这是对所有用户都有效的配置；然后依次寻找下面三个文件，这是针对当前用户的配置。

```txt
~/.bash_profile
~/.bash_login
~/.profile
```

需要注意的是，这三个文件只要有一个存在，就不再读入后面的文件了。比如，要是 ~/.bash_profile 存在，就不会再读入后面两个文件了。

（2）ssh登录：与第一种情况完全相同。

（3）图形界面登录：只加载 /etc/profile 和 /.profile。也就是说，/.bash_profile 不管有没有，都不会运行。

## Linux关机

```txt
sync 将数据由内存同步到硬盘中。

shutdown 关机指令，你可以man shutdown 来看一下帮助文档。例如你可以运行如下命令关机：
shutdown –h 10 'This server will shutdown after 10 mins' 计算机将在10分钟后关机，并且显示信息在登陆用户的当前屏幕中。
shutdown –h now 立马关机
shutdown –h 20:25 系统会在今天20:25关机
shutdown –h +10 十分钟后关机
shutdown –r now 系统立马重启
shutdown –r +10 系统十分钟后重启
reboot 就是重启，等同于 shutdown –r now
halt 关闭系统，等同于shutdown –h now 和 poweroff
```

最后总结一下，不管是重启系统还是关闭系统，首先要运行**sync**命令，把内存中的数据写到磁盘中。

关机的命令有 **shutdown –h now halt poweroff 和 init 0** , 重启系统的命令有 **shutdown –r now reboot init 6。**

# 计算机启动的流程

![image](https://github.com/user-attachments/assets/95f2569d-71fe-49e2-819d-22ae1dd9bd67)


boot是bootstrap（鞋带）的缩写，它来自一句谚语：

![image](https://github.com/user-attachments/assets/11b0afb5-cc82-456e-9aa9-61d6e0dd7518)


字面意思是"拽着鞋带把自己拉起来"，这当然是不可能的事情。最早的时候，工程师们用它来比喻，计算机启动是一个很矛盾的过程：必须先运行程序，然后计算机才能启动，但是计算机不启动就无法运行程序！

早期真的是这样，必须想尽各种办法，把一小段程序装进内存，然后计算机才能正常运行。所以，工程师们把这个过程叫做"拉鞋带"，久而久之就简称为boot了。

计算机的整个启动过程分成四个阶段。

## 第一阶段：BIOS
上个世纪70年代初，“只读内存”（read-only memory，缩写为ROM）发明，开机程序被刷入ROM芯片，计算机通电后，第一件事就是读取它。

BIOS全称是Basic Input/Output System，即基本输入输出系统，即下图芯片里的程序。

![image](https://github.com/user-attachments/assets/5b8b5c69-d280-4184-9463-a8ce5d726b23)

### 硬件自检

BIOS程序首先检查，计算机硬件能否满足运行的基本条件，这叫做"硬件自检"（Power-On Self-Test），缩写为POST。

如果硬件出现问题，主板会发出不同含义的蜂鸣，启动中止。如果没有问题，屏幕就会显示出CPU、内存、硬盘等信息。

![image](https://github.com/user-attachments/assets/1e4bf01f-abcc-4a3b-b14c-b827bf013dff)

### 启动顺序

硬件自检完成后，BIOS把控制权转交给下一阶段的启动程序。

下一阶段的启动程序根据BIOS设置项Boot Sequence（启动顺序）决定，排在前面的设备就是优先转交控制权的设备。

![image](https://github.com/user-attachments/assets/b3aa5108-aeb9-454d-aee4-3cee6f331ff3)

## 第二阶段： 主引加粗样式导记录
BIOS按照"启动顺序"，把控制权转交给排在第一位的储存设备。

这时，计算机读取该设备的第一个扇区，也就是读取最前面的512个字节。如果这512个字节的最后两个字节是0x55和0xAA，表明这个设备可以用于启动；如果不是，表明设备不能用于启动，控制权于是被转交给"启动顺序"中的下一个设备。

这最前面的512个字节，就叫做"主引导记录"（Master boot record，缩写为MBR）。

### 主引导记录组成

主引导记录由三个部分组成：

![image](https://github.com/user-attachments/assets/3656c687-557d-4104-9f26-e93cd081780d)

其中，第二部分"分区表"的作用，是将硬盘分成若干个区。

### 分区表

硬盘分区有很多好处。每个分区可以安装不同的操作系统，"主引导记录"因此必须知道将控制权转交给哪个区。

分区表的长度只有64个字节，里面又分成四项，每项16个字节。所以，一个硬盘最多只能分四个一级分区，又叫做"主分区"。

每个主分区的16个字节，由6个部分组成：

![image](https://github.com/user-attachments/assets/3e8cf840-4516-4a2b-99ab-30ce1df45f9d)

最后的四个字节（“主分区的扇区总数”），决定了这个主分区的长度。也就是说，一个主分区的扇区总数最多不超过2的32次方。

如果每个扇区为512个字节，就意味着单个分区最大不超过2TB。再考虑到扇区的逻辑地址也是32位，所以单个硬盘可利用的空间最大也不超过2TB。如果想使用更大的硬盘，只有2个方法：一是提高每个扇区的字节数，二是增加扇区总数。

## 第三阶段：硬盘启动
这时，计算机的控制权就要转交给硬盘的某个分区了，这里又分成三种情况。

### 情况A：卷引导记录

上一节提到，四个主分区里面，只有一个是激活的。计算机会读取激活分区的第一个扇区，叫做"卷引导记录"（Volume boot record，缩写为VBR）。

"卷引导记录"的主要作用是，告诉计算机，操作系统在这个分区里的位置。然后，计算机就会加载操作系统了。

### 情况B：扩展分区和逻辑分区

随着硬盘越来越大，四个主分区已经不够了，需要更多的分区。但是，分区表只有四项，因此规定有且仅有一个区可以被定义成"扩展分区"（Extended partition）。

所谓"扩展分区"，就是指这个区里面又分成多个区。这种分区里面的分区，就叫做"逻辑分区"（logical partition）。

计算机先读取扩展分区的第一个扇区，叫做"扩展引导记录"（Extended boot record，缩写为EBR）。它里面也包含一张64字节的分区表，但是最多只有两项（也就是两个逻辑分区）。

计算机接着读取第二个逻辑分区的第一个扇区，再从里面的分区表中找到第三个逻辑分区的位置，以此类推，直到某个逻辑分区的分区表只包含它自身为止（即只有一个分区项）。因此，扩展分区可以包含无数个逻辑分区。

但是，似乎很少通过这种方式启动操作系统。如果操作系统确实安装在扩展分区，一般采用下一种方式启动。

### 情况C：启动管理器

在这种情况下，计算机读取"主引导记录"前面446字节的机器码之后，不再把控制权转交给某一个分区，而是运行事先安装的"启动管理器"（boot loader），由用户选择启动哪一个操作系统。

Linux环境中的启动管理器例如Grub。

![image](https://github.com/user-attachments/assets/07576b17-23e2-463a-b4ab-0ee19f031575)

## 第四阶段：操作系统
控制权转交给操作系统后，操作系统的内核首先被载入内存。

以Linux系统为例，先载入/boot目录下面的kernel。内核加载成功后，第一个运行的程序是/sbin/init。它根据配置文件（Debian系统是/etc/initab）产生init进程。这是Linux启动后的第一个进程，pid进程编号为1，其他进程都是它的后代。

然后，init线程加载系统的各个模块，比如窗口程序和网络程序，直至执行/bin/login程序，跳出登录界面，等待用户输入用户名和密码。

至此，全部启动过程完成。

## 单用户模式修改Centos系统root密码
步骤如下：

重启linux系统

![image](https://github.com/user-attachments/assets/a44a6e84-c5a6-4938-8e96-1ff240cdf5e9)

3 秒之内要按一下回车，出现如下界面

![image](https://github.com/user-attachments/assets/265d196e-535a-487f-8038-9c8ef1ab7551)

按向下方向键移动到第二行，按"e"进入编辑模式

![image](https://github.com/user-attachments/assets/9d9b61b7-1788-471d-a48d-a2a6561df1bf)

在 第二行最后边输入 single，用空格与前面内容隔开

![image](https://github.com/user-attachments/assets/0d06d968-1a7a-4258-bd62-4458bee352f4)

回车

![image](https://github.com/user-attachments/assets/610db764-fd9f-42bc-b10d-54edccad9c79)

最后按"b"启动，启动后就进入了单用户模式了

![image](https://github.com/user-attachments/assets/9bcb201a-232d-47c2-97b5-800f604a372f)

进入到单用户模式后，就可以使用passwd命令任意更改root密码了：

![image](https://github.com/user-attachments/assets/eae84990-4ed8-4f1e-905e-111565a67a44)

## 救援模式修改Ubuntu系统root密码
重启，按住shift键，出现如下界面，选中如下选项

![image](https://github.com/user-attachments/assets/a7b62c8d-4a0f-4d22-a69b-107d715c723c)

按回车键进入如下界面，然后选中最新的recovery mode选项

![image](https://github.com/user-attachments/assets/d7bd7927-d0b2-46c5-b4c5-2a45956e4efa)

按e进入如下界面，找到图中红色框的recovery nomodeset并将其删掉，再在这一行的后面输入

```txt
quiet splash rw init=/bin/bash
```

![image](https://github.com/user-attachments/assets/367d7323-f250-4c3b-a5ec-393414fd48cd)

![image](https://github.com/user-attachments/assets/8b8918f7-7cdb-47fa-82f4-ca535b447cc8)

接着按F10或者Ctrl+x 后出现如下界面，在命令行内输入passwd后进行修改密码即可

![image](https://github.com/user-attachments/assets/35d4dfc0-a4ad-4436-a4a2-e4ee5cf396a3)

修改完之后重启系统。

# 虚拟机
## 三种网络模式
### 桥接

在网络网卡上安装了一个桥接协议，让这块网卡处于混杂模式，可以同时连接多个网络的做法。

桥接下，类似于把物理主机虚拟为一个交换机，所有桥接设置的虚拟机连接到这个交换机的一个接口上，物理主机也同样查在这个交换机当中，所以所有桥接下网卡与网卡都是交换模式的，相互可以访问而不干扰。

![image](https://github.com/user-attachments/assets/a14d40c6-f219-42e5-8c70-de7e5a746217)

### Host-only（仅与主机通信）

虚拟机使用VMnet1网卡与主机单独组网,主机对于虚拟机相当于路由器

![image](https://github.com/user-attachments/assets/0eda774f-5ee7-4bea-8f72-3463a15ef775)

### NAT

虚拟机使用VMnet8网卡与主机单独组网,主机对于虚拟机相当于路由器，VMnet8网卡通过NAT地址转换协议与物理机网卡通信

![image](https://github.com/user-attachments/assets/8c0be0c3-83a4-48b9-9297-746c746a1a16)

![image](https://github.com/user-attachments/assets/a1a2d409-3cf2-4dc4-b936-a3cb1e839112)

## 常见问题
### 修改静态地址后发现无法ping外网

```txt
需要设置网关
route add default gw 192.168.33.1
添加nameserver
vi /etc/resolv.conf
nameserver 192.168.33.1
```

### 虚拟机克隆后eth0消失

```txt
直接修改  /etc/sysconfig/network-script/ifcfg-eth0
删掉UUID  HWADDR
配置静态地址
然后：
rm -rf 　/etc/udev/rules.d/70-persistent-net.rules
然后 reboot
```
