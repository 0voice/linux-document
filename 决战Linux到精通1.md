原文链接：https://blog.csdn.net/as604049322/article/details/120446586
# 操作系统的发展史
## Unix
- 1965年之前，电脑只有军事或者学院的研究机构碰的起，当时大型主机至多能提供30台终端（30个键盘、显示器)的连接。
- 1965年左后由贝尔实验室、麻省理工学院 以及 通用电气共同发起了Multics项目，想让大型主机支持300台终端
- 1969年前后这个项目进度缓慢，资金短缺，贝尔实验室退出了研究
- 1969年从这个项目中退出的Ken Thompson当时在实验室无聊时，为了让一台空闲的电脑上能够运行“星际旅行”游行，在8月份左右趁着其妻子探亲的时间，用了1个月的时间编写出了 Unix操作系统的原型
- 1970年，美国贝尔实验室的 Ken Thompson，以 BCPL语言 为基础，设计出很简单且很接近硬件的 B语言（取BCPL的首字母），并且他用B语言写了第一个UNIX操作系统。
- 因为B语言的跨平台性较差，为了能够在其他的电脑上也能够运行这个非常棒的Unix操作系统，Dennis Ritchie和Ken Thompson 从B语言的基础上准备研究一个更好的语言
- 1972年，美国贝尔实验室的 Dennis Ritchie在B语言的基础上最终设计出了一种新的语言，他取了BCPL的第二个字母作为这种语言的名字，这就是C语言
- 1973年初，C语言的主体完成。Thompson和Ritchie迫不及待地开始用它完全重写了现在大名鼎鼎的Unix操作系统

## Minix
因为AT&T(通用电气)的政策改变，在Version 7 Unix推出之后，发布新的使用条款，将UNIX源代码私有化，在大学中不再能使用UNIX源代码。Andrew S. Tanenbaum(塔能鲍姆)教授为了能在课堂上教授学生操作系统运作的实务细节，决定在不使用任何AT&T的源代码前提下，自行开发与UNIX兼容的操作系统，以避免版权上的争议。他以小型UNIX（mini-UNIX）之意，将它称为MINIX。

## Linux
因为Minix只是教学使用，因此功能并不强，因此Torvalds利用GNU的bash当做开发环境，gcc当做编译工具，编写了Linux内核-v0.02，但是一开始Linux并不能兼容Unix，即Unix上跑的应用程序不能在Linux上跑，即应用程序与内核之间的接口不一致，因为Unix是遵循POSIX规范的，因此Torvalds修改了Linux，并遵循POSIX（Portable Operating System Interface，他规范了应用程序与内核的接口规范）； 一开始Linux只适用于386，后来经过全世界的网友的帮助，最终能够兼容多种硬件

## 操作系统的发展
![image](https://github.com/user-attachments/assets/8c84710c-a74c-446c-b7d4-6202d2782cab)

![image](https://github.com/user-attachments/assets/d0e9c13f-61a8-46f7-914c-a201c0394cb6)

![image](https://github.com/user-attachments/assets/ad6c6e2a-fc6d-45de-b675-de701fd0e587)

## Minix没有火起来的原因
Minix的创始人说，MINIX 3没有统治世界是源于他在1992年犯下的一个错误，当时他认为BSD必然会一统天下，因为它是一个更稳定和更成熟的系统，其它操作系统难以与之竞争。因此他的MINIX的重心集中在教育上。四名BSD开发者已经成立了一家公司销售BSD系统，他们甚至还有一个有趣的电话号码1-800-ITS-UNIX。然而他们正因为这个电话号码而惹火上身。美国电话电报公司因电话号码而提起诉讼。官司打了三年才解决。在此期间，BSD陷于停滞，而Linux则借此一飞冲天。他的错误在于没有意识官司竟然持续了如此长的时间，以及BSD会因此受到削弱。如果美国电话电报公司没有起诉，Linux永远不会流行起来，BSD将统治世界。

# Linux介绍
## Linux内核&发行版
### Linux内核版本
内核(kernel)是系统的心脏，是运行程序和管理像磁盘和打印机等硬件设备的核心程序，它提供了一个在裸设备与应用程序间的抽象层。

Linux内核版本又分为稳定版和开发版，两种版本是相互关联，相互循环：

- 稳定版：具有工业级强度，可以广泛地应用和部署。新的稳定版相对于较旧的只是修正一些bug或加入一些新的驱动程序。
- 开发版：由于要试验各种解决方案，所以变化很快。

内核源码网址：http://www.kernel.org 所有来自全世界的对Linux源码的修改最终都会汇总到这个网站，由Linus领导的开源社区对其进行甄别和修改最终决定是否进入到Linux主线内核源码中。

### Linux发行版本
Linux发行版 (也被叫做 GNU/Linux 发行版) 通常包含了包括桌面环境、办公套件、媒体播放器、数据库等应用软件。

目前市面上较知名的发行版有：Ubuntu、RedHat、CentOS、Debian、Fedora、SuSE、OpenSUSE、Arch Linux、SolusOS 等。
![image](https://github.com/user-attachments/assets/19b4f19e-99be-41a3-b1b3-089ef2b55be1)

## 类Unix系统目录结构
Unix没有盘符这个概念，只有一个根目录/，所有文件都在它下面
![image](https://github.com/user-attachments/assets/b628eddd-0a8a-4a07-bbf7-2dbe45c9d884)


## Linux目录
![image](https://github.com/user-attachments/assets/8b5f63b7-f275-4f08-9298-d247ab860b67)


- /：根目录，一般根目录下只存放目录，在Linux下有且只有一个根目录。所有的东西都是从这里开始。当你在终端里输入“/home”，你其实是在告诉电脑，先从/（根目录）开始，再进入到home目录。
- /bin: /usr/bin: 可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等。
- /boot：放置linux系统启动时用到的一些文件，如Linux的内核文件：/boot/vmlinuz，系统引导管理器：/boot/grub。
- /dev：存放linux系统下的设备文件，访问该目录下某个文件，相当于访问某个设备，常用的是挂载光驱 mount /dev/cdrom /mnt。
- /etc：系统配置文件存放的目录，不建议在此目录下存放可执行文件，重要的配置文件有 /etc/inittab、/etc/fstab、/etc/init.d、/etc/X11、/etc/sysconfig、/etc/xinetd.d。
- /home：系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下，表示当前用户的家目录，edu 表示用户 edu 的家目录。
- /lib: /usr/lib: /usr/local/lib：系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助。
- /lost+fount：系统异常产生错误时，会将一些遗失的片段放置于此目录下。
- /mnt: /media：光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，也不一定，可以选择任意位置进行挂载。
- /opt：给主机额外安装软件所摆放的目录。
- /proc：此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的目录有 /proc/cpuinfo、/proc/interrupts、/proc/dma、/proc/ioports、/proc/net/* 等。
- /root：系统管理员root的家目录。
- /sbin: /usr/sbin: /usr/local/sbin：放置系统管理员使用的可执行命令，如fdisk、shutdown、mount 等。与 /bin 不同的是，这几个目录是给系统管理员 root使用的命令，一般用户只能"查看"而不能设置和使用。
- /tmp：一般用户或正在执行的程序临时存放文件的目录，任何人都可以访问，重要数据不可放置在此目录下。
- /srv：服务启动之后需要访问的数据目录，如 www 服务需要访问的网页数据存放在 /srv/www 内。
- /usr：应用程序存放目录，/usr/bin 存放应用程序，/usr/share 存放共享数据，/usr/lib 存放不能直接运行的，却是许多程序运行所必需的一些函数库文件。/usr/local: 存放软件升级包。/usr/share/doc: 系统说明文件存放目录。/usr/share/man: 程序说明文件存放目录。
- /var：放置系统执行过程中经常变化的文件，如随时更改的日志文件 /var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下。

## 用户目录
位于/home/user，称之为用户工作目录或家目录,表示方式：

![image](https://github.com/user-attachments/assets/eaf20e58-6f7c-40cc-bc84-8aad1bf6baf6)

从/目录开始描述的路径为绝对路径，如：

![image](https://github.com/user-attachments/assets/8a4aeef9-a92f-4d97-b7d5-5cdf8a90e721)

从当前位置开始描述的路径为相对路径，如：

![image](https://github.com/user-attachments/assets/9b197c74-56a8-4113-9bae-610d33d042cc)

每个目录下都有**.和…**

. 表示当前目录

… 表示上一级目录，即父目录

根目录下的.和…都表示当前目录

![image](https://github.com/user-attachments/assets/aa159871-f2bb-4709-b756-2367821caedb)

# 命令行基本操作
## 命令使用方法
Linux命令格式：

![image](https://github.com/user-attachments/assets/8864d76c-3bb6-4d72-811b-cbe6f6a19543)


command: 命令名； [-options]：选项,可用来对命令进行控制，也可以省略，[]代表可选 parameter1 …：传给命令的参数：可以是零个一个或多个

## 查看帮助文档
### help
一般是linux命令自带的帮助信息

如：ls --help

### man(manual)
man是linux提供的一个手册，包含了绝大部分的命令、函数使用说明

该手册分成很多章节（section），使用man时可以指定不同的章节来浏览。

例：man ls ; man 2 printf

man中各个section意义如下：

  1.Standard commands（标准命令）

  2.System calls（系统调用，如open,write）

  3.Library functions（库函数，如printf,fopen）

  4.Special devices（设备文件的说明，/dev下各种设备）

  5.File formats（文件格式，如passwd）
 
  6.Games and toys（游戏和娱乐）

  7.Miscellaneous（杂项、惯例与协定等，例如Linux档案系统、网络协定、ASCII 码；environ全局变量）

  8.Administrative Commands（管理员命令，如ifconfig）

man是按照手册的章节号的顺序进行搜索的。

man设置了如下的功能键：

![image](https://github.com/user-attachments/assets/6038bc91-b7fa-472b-82a1-ea9e75b22b63)

![image](https://github.com/user-attachments/assets/2806ce46-92be-4454-9831-5aa21a6ff20e)

注意：实际上，我们不用指定第几个章节也用查看，如，man ls

## tab键自动补全
在敲出命令的前几个字母的同时，按下tab键，系统会自动帮我们补全命令

## history游览历史
当系统执行过一些命令后，可按上下键翻看以前的命令，history将执行过的命令列举出来

history保留了最近执行的命令记录，默认可以保留1000。
历史清单从0开始编号到最大值。

常见用法：

![image](https://github.com/user-attachments/assets/68f13927-69d7-4ebc-b861-d34b7ab11070)

## 命令行中的ctrl组合键
- Ctrl+c 结束正在运行的程序

- Ctrl+d 结束输入或退出shell

- Ctrl+s 暂停屏幕输出【锁住终端】

- Ctrl+q 恢复屏幕输出【解锁终端】

- Ctrl+l 清屏，【是字母L的小写】等同于Clear

- 当前光标到行首：ctrl+a

- 当前光标到行尾：ctrl+e

- 删除当前光标到行首：ctrl+u

- 删除当前光标到行尾：ctrl+k

- Ctrl+y 在光标处粘贴剪切的内容

- Ctrl+r 查找历史命令【输入关键字，就能调出以前执行过的命令】

- Ctrl+t 调换光标所在处与其之前字符位置，并把光标移到下个字符

- Ctrl+x+u 撤销操作

- Ctrl+z 转入后台运行

# Linux命令
## 权限管理
### 列出目录的内容：ls
Linux文件或者目录名称最长可以有265个字符，“.”代表当前目录，“…”代表上一级目录，以“.”开头的文件为隐藏文件，需要用 -a 参数才能显示。

ls常用参数：

![image](https://github.com/user-attachments/assets/e65b56e4-f459-44ad-b7cc-1065d6e5d320)

![image](https://github.com/user-attachments/assets/fd7c6ad1-b51e-40fe-a5a2-2905d4280f4d)

列出的信息的含义：

![image](https://github.com/user-attachments/assets/e257a49b-549e-418f-8f26-fda12ddf5196)


ls支持通配符：

![image](https://github.com/user-attachments/assets/71f3b6b1-5bb0-4ce9-b4a9-148b90727c3e)


### 显示inode的内容：stat
![image](https://github.com/user-attachments/assets/c9db5078-68e0-4911-8f24-6cb43a58e95d)


查看 testfile 文件的inode内容内容，可以用以下命令：

![image](https://github.com/user-attachments/assets/a7492c87-2bfb-43b5-ab62-9dc80b363749)


### 文件访问权限
用户能够控制一个给定的文件或目录的访问程度，一个文件或目录可能有读、写及执行权限：

- 读权限（r） ：对于文件，具有读取文件内容的权限；对于目录，具有浏览目录的权限。
- 写权限（w） ：对于文件，具有修改文件内容的权限；对于目录，具有删除、移动目录内文件的权限。
- 可执行权限（x）： 对于文件，具有执行文件的权限；对于目录，该用户具有进入目录的权限。
- 
通常，Unix/Linux系统只允许文件的属主(所有者)或超级用户改变文件的读写权限。

示例：

![image](https://github.com/user-attachments/assets/33ccac74-77ac-4b64-8376-ec005021595f)

第1个字母代表文件的类型：

- “d” 代表文件夹
- “-” 代表普通文件
- “c” 代表硬件字符设备
- “b” 代表硬件块设备
- “s”表示管道文件
- “l” 代表软链接文件。

后9个字母分别代表三组权限：文件所有者、用户组、其他用户拥有的权限。

### 修改文件权限：chmod
chmod 修改文件权限有两种使用格式：字母法与数字法。

字母法：chmod u/g/o/a +/-/= rwx 文件

![image](https://github.com/user-attachments/assets/bffb9be0-bf7d-431f-a5f7-b202f1df59bd)


数字法：“rwx” 这些权限也可以用数字来代替

![image](https://github.com/user-attachments/assets/c2b13aa1-a864-416e-9824-79aa47b50e19)

如执行：chmod u=rwx,g=rx,o=r filename 就等同于：chmod u=7,g=5,o=4 filename

chmod 751 file：

- 文件所有者：读、写、执行权限
- 同组用户：读、执行的权限
- 其它用户：执行的权限

chmod 777 file：所有用户拥有读、写、执行权限

注意：如果想递归所有目录加上相同权限，需要加上参数“ -R ”。 如：chmod 777 test/ -R 递归 test 目录下所有文件加 777 权限

### 修改文件所有者：chown
![image](https://github.com/user-attachments/assets/ab5308e7-85bd-4d5b-97e9-32af1ee83031)


### 修改文件所属组：chgrp
![image](https://github.com/user-attachments/assets/65e566f9-b69b-4f91-a4d6-2987f4f0dce9)


## 文件内容查看
Linux系统中使用以下命令来查看文件的内容：

- cat 由第一行开始显示文件内容
- tac 从最后一行开始显示
- nl 显示的时候，顺道输出行号
- more 一页一页的显示文件内容
- less与more 类似，但可以往前翻页
- head 只看头几行
- tail 只看尾巴几行

### 基本显示：cat、tac
语法：

![image](https://github.com/user-attachments/assets/b894b3de-3671-4b05-9e72-5a4090b32867)

选项与参数：

- -A ：相当于 -vET 的整合选项，可列出一些特殊字符而不是空白而已；
- -v ：列出一些看不出来的特殊字符
- -E ：将结尾的断行字节 $ 显示出来；
- -T ：将 [tab] 按键以 ^I 显示出来；
- -b ：列出行号，空白行不标行号
- -n ：列出行号，连同空白行也会有行号

![image](https://github.com/user-attachments/assets/bb7d62b6-8a80-439c-b098-a8c4387b92dc)

tac与cat命令刚好相反，文件内容从最后一行开始显示，可以看出 tac 是 cat 的倒着写！如：

![image](https://github.com/user-attachments/assets/0090223b-a5fc-41b3-a7ad-119b0928626b)


### 显示行号：nl

语法：

![image](https://github.com/user-attachments/assets/3cec30ad-78d5-4141-a5f4-0542182f5ddf)


选项与参数：

- -b ：指定行号指定的方式，主要有两种：
- -b a ：表示不论是否为空行，也同样列出行号(类似 cat -n)；
- -b t ：如果有空行，空的那一行不要列出行号(默认值)；
- -n ：列出行号表示的方法，主要有三种：
- -n ln ：行号在荧幕的最左方显示；
- -n rn ：行号在自己栏位的最右方显示，且不加 0 ；
- -n rz ：行号在自己栏位的最右方显示，且加 0 ；
- -w ：行号栏位的占用的位数。

![image](https://github.com/user-attachments/assets/ec63187a-020a-454a-948b-e6f3ad7bd168)


分屏显示：more、less

![image](https://github.com/user-attachments/assets/261decd4-ae7c-450b-bd4b-c761329b60da)


more运行时可以输入的命令有：

- 空白键 (space)：代表向下翻一页；
- Enter ：代表向下翻『一行』；
- /字串 ：代表在这个显示的内容当中，向下搜寻『字串』这个关键字；
- :f ：立刻显示出档名以及目前显示的行数；
- q ：代表立刻离开 more ，不再显示该文件内容。
- b 或 [ctrl]-b ：代表往回翻页，不过这动作只对文件有用，对管线无用。

![image](https://github.com/user-attachments/assets/452c9a91-1235-4d22-8a3a-28a7c2a6aa15)

less运行时可以输入的命令有：

- 空白键 ：向下翻动一页；
- [pagedown]：向下翻动一页；
- [pageup] ：向上翻动一页；
- /字串 ：向下搜寻『字串』的功能；
- ?字串 ：向上搜寻『字串』的功能；
- n ：重复前一个搜寻 (与 / 或 ? 有关！)
- N ：反向的重复前一个搜寻 (与 / 或 ? 有关！)
- q ：离开 less 这个程序；

### 取首尾n行：head、tail
head取出文件前面几行

语法：

![image](https://github.com/user-attachments/assets/237cfcb5-1192-4044-9248-4f9bf395ec42)


选项与参数：

- -n ：后面接数字，代表显示几行的意思

![image](https://github.com/user-attachments/assets/3b7c95b6-db0d-4447-ad5c-4505011a6099)

默认的情况中，显示前面 10 行！若要显示前 20 行，就得要这样：

![image](https://github.com/user-attachments/assets/3df175cc-17dc-44b2-9f72-9b324c994745)


tail取出文件后面几行

语法：

![image](https://github.com/user-attachments/assets/76615980-4ac2-4c23-ae9e-d8a44dcbc4ab)


选项与参数：

- -n ：后面接数字，代表显示几行的意思
- -f ：表示持续侦测后面所接的档名，要等到按下[ctrl]-c才会结束tail的侦测

![image](https://github.com/user-attachments/assets/77d51cba-c85e-4b8b-9276-8b8c4bd1fad7)


## 文件管理
### 输出重定向：>
可将本应显示在终端上的内容保存到指定文件中。

如：ls > test.txt ( test.txt 如果不存在，则创建，存在则覆盖其内容 )

注意： >输出重定向会覆盖原来的内容，>>输出重定向则会追加到文件的尾部。

### 管道：|
管道：一个命令的输出可以通过管道做为另一个命令的输入。

“ | ”的左右分为两端，从左端写入到右端。

![image](https://github.com/user-attachments/assets/c8806610-147d-44df-a72d-5151ad1320d7)

### 清屏：clear
clear作用为清除终端上的显示(类似于DOS的cls清屏功能)，快捷键：Ctrl + l ( “l” 为字母 )。

### 切换工作目录： cd
Linux所有的目录和文件名大小写敏感

cd后面可跟绝对路径，也可以跟相对路径。如果省略目录，则默认切换到当前用户的主目录。

![image](https://github.com/user-attachments/assets/aaac8b69-04db-40ea-8507-6c4697e57948)


### 显示当前路径：pwd

![image](https://github.com/user-attachments/assets/53a9bfd5-7c41-4806-92ff-6319fdd32bb4)


选项与参数：

- -P ：显示出确实的路径，而非使用连结 (link) 路径。

![image](https://github.com/user-attachments/assets/f66b0f56-9e2d-43b8-9696-6ad2ca8cc0e4)


### 创建目录：mkdir
mkdir可以创建一个新的目录。

注意：新建目录的名称不能与当前目录中已有的目录或文件同名，并且目录创建者必须对当前目录具有写权限。

语法：

![image](https://github.com/user-attachments/assets/a69dacdd-74b4-4217-9aa6-2e3b96efeb91)


选项与参数：

- -m ：指定被创建目录的权限，而不是根据默认权限 (umask) 设定
- -p ：递归创建所需要的目录

实例：-p递归创建目录：

![image](https://github.com/user-attachments/assets/d266bfa4-bc77-4f95-a14f-ae3b8bb002ab)

mkdir创建的目录权限默认根据umask得到，而-m参数可以指定被创建目录的权限：

![image](https://github.com/user-attachments/assets/8624fc59-c65d-4154-8d92-afd476f82564)


### 删除文件：rm
可通过rm删除文件或目录。使用rm命令要小心，因为文件删除后不能恢复。为了防止文件误删，可以在rm后使用-i参数以逐个确认要删除的文件。

常用参数及含义如下表所示：

![image](https://github.com/user-attachments/assets/25187e8a-9705-4339-89bd-f098271bef73)


### 建立链接文件：ln
软链接：ln -s 源文件 链接文件

硬链接：ln 源文件 链接文件

软链接类似于Windows下的快捷方式，如果软链接文件和源文件不在同一个目录，源文件要使用绝对路径，不能使用相对路径。

硬链接只能链接普通文件不能链接目录。 两个文件占用相同大小的硬盘空间，即使删除了源文件，链接文件还是存在，所以-s选项是更常见的形式。

### 文本搜索：grep
Linux系统中grep命令是一种强大的文本搜索工具，grep允许对文本文件进行模式查找。如果找到匹配模式， grep打印包含模式的所有行。

grep一般格式为：

![image](https://github.com/user-attachments/assets/df830730-601a-4810-9f7f-9eff65a5e3f8)

在grep命令中输入字符串参数时，最好引号或双引号括起来。例如：grep 'a' 1.txt。

在当前目录中，查找前缀有test字样的文件中包含 test 字符串的文件，并打印出该字符串的行。此时，可以使用如下命令：

![image](https://github.com/user-attachments/assets/de07afdc-c57e-4eee-852d-30602d86eb52)


以递归的方式查找符合条件的文件。例如，查找指定目录/etc/acpi 及其子目录（如果存在子目录的话）下所有文件中包含字符串"update"的文件，并打印出该字符串所在行的内容，使用的命令为：

![image](https://github.com/user-attachments/assets/1550cb4c-c141-41e7-9495-7ee6f76a1ddd)


反向查找。前面各个例子是查找并打印出符合条件的行，通过"-v"参数可以打印出不符合条件行的内容。

查找文件名中包含 test 的文件中不包含test 的行，此时，使用的命令为：

![image](https://github.com/user-attachments/assets/a9b0714a-122c-4022-ae96-c0f4936a474e)


### 查找文件：find
常用用法：

![image](https://github.com/user-attachments/assets/811a7fd2-50d8-4ca0-ad98-5feb160ed995)

Linux find命令用来在指定目录下查找文件。任何位于参数之前的字符串都将被视为欲查找的目录名。如果使用该命令时，不设置任何参数，则find命令将在当前目录下查找子目录与文件。并且将查找到的子目录和文件全部进行显示。

语法：

![image](https://github.com/user-attachments/assets/ebeb763c-6fe4-431c-8686-51fa7054ad4a)


常用参数说明 :

- -perm xxxx：权限为 xxxx的文件或目录
- -user： 按照文件属主来查找文件。
- -size n : n单位,b:512位元组的区块,c:字元数,k:kilo bytes,w:二个位元组
- -mount, -xdev : 只检查和指定目录在同一个文件系统下的文件，避免列出其它文件系统中的文件
- -amin n : 在过去 n 分钟内被读取过
- -anewer file : 比文件 file 更晚被读取过的文件
- -atime n : 在过去n天内被读取过的文件
- -cmin n : 在过去 n 分钟内被修改过
- -cnewer file :比文件 file 更新的文件
- -ctime n : 在过去n天内被修改过的文件
- -empty : 空的文件
- -gid n or -group name : gid 是 n 或是 group 名称是 name
- -ipath p, -path p : 路径名称符合 p 的文件，ipath 会忽略大小写
- -name name, -iname name : 文件名称符合 name 的文件。iname 会忽略大小写
- -type 查找某一类型的文件：
b - 块设备文件,
d - 目录,
c - 字符设备文件,
p - 管道文件,
l - 符号链接文件,
f - 普通文件
- -exec 命令名{} \ (注意：“}”和“\”之间有空格)

find实例：

![image](https://github.com/user-attachments/assets/03c01562-c9cf-4c3d-9c39-f1d0512c04ee)


### 拷贝文件：cp
cp命令的功能是将给出的文件或目录复制到另一个文件或目录中，相当于DOS下的copy命令。

常用选项说明：

![image](https://github.com/user-attachments/assets/3372a325-07a6-427f-95d8-4685242c4f49)

cp vim_configure/ code/ -ivr 把文件夹 vim_configure 拷贝到 code 目录里。

### 移动文件：mv
mv命令用来移动文件或目录，也可以给文件或目录重命名。

常用选项说明：

![image](https://github.com/user-attachments/assets/b249e284-8b8a-48c0-a612-034a2fff1fcd)


### 归档管理：tar
此命令可以把一系列文件归档到一个大文件中，也可以把档案文件解开以恢复数据。

tar使用格式 tar [参数] 打包文件名 文件

tar命令参数很特殊，其参数前面可以使用“-”，也可以不使用。

常用参数：

![image](https://github.com/user-attachments/assets/af052ff4-2d31-42cf-ba6b-eab5030df790)


注意：除了f需要放在参数的最后，其它参数的顺序任意。

![image](https://github.com/user-attachments/assets/45d9539d-09cd-44aa-be5a-afdfefb56f4a)


### 文件压缩解压：gzip、bzip2
tar与gzip命令结合使用实现文件打包、压缩。 tar只负责打包文件，但不压缩，用gzip压缩tar打包后的文件，其扩展名一般用xxxx.tar.gz。

gzip使用格式如下：

![image](https://github.com/user-attachments/assets/b6b8df0c-f9a8-475a-b580-104f230e7178)


常用选项：

![image](https://github.com/user-attachments/assets/8b3b35fd-8523-429a-93e7-7231dde101da)

![image](https://github.com/user-attachments/assets/b267bfb0-2994-4363-b239-567b80974352)

tar命令中-z选项可以调用gzip实现了一个压缩的功能，实行一个先打包后压缩的过程。

压缩用法：tar zcvf 压缩包包名 文件1 文件2 …

例如： tar zcvf test.tar.gz 1.c 2.c 3.c 4.c把 1.c 2.c 3.c 4.c 压缩成 test.tar.gz

![image](https://github.com/user-attachments/assets/fe32efcf-c00b-46d7-a3d3-6923a439fb4d)


解压用法： tar zxvf 压缩包包名

例如：

![image](https://github.com/user-attachments/assets/c823abe7-bda0-403b-86cf-6269d143dcd2)


解压到指定目录：-C （解压时可以不指定-z选项）

![image](https://github.com/user-attachments/assets/4241bbae-e7e8-4b59-baf7-9ae8cba7c667)


bzip2命令跟gzip用法类似

压缩用法：tar jcvf 压缩包包名 文件…(tar jcvf bk.tar.bz2 *.c)

解压用法：tar jxvf 压缩包包名 (tar jxvf bk.tar.bz2)

### 文件压缩解压：zip、unzip
通过zip压缩文件的目标文件不需要指定扩展名，默认扩展名为zip。

压缩文件：zip [-r] 目标文件(没有扩展名) 源文件

解压文件：unzip -d 解压后目录文件 压缩文件

![image](https://github.com/user-attachments/assets/0450f939-8a3a-48c7-9846-c0285cc3cdbb)


### 查看命令位置：which

![image](https://github.com/user-attachments/assets/e5ece9f3-0b92-445d-841f-5e784bc06be1)



## 用户和用户组管理
用户管理包括用户与组账号的管理。

在Unix/Linux系统中，不论是由本机或是远程登录系统，每个系统都必须拥有一个账号，并且对于不同的系统资源拥有不同的使用权限。

Unix/Linux系统中的root账号通常用于系统的维护和管理，它对Unix/Linux操作系统的所有部分具有不受限制的访问权限。

在Unix/Linux安装的过程中，系统会自动创建许多用户账号，而这些默认的用户就称为“标准用户”。

在大多数版本的Unix/Linux中，都不推荐直接使用root账号登录系统。

### 查看当前用户：whoami
查看当前系统当前账号的用户名。可通过cat /etc/passwd查看系统用户信息。

![image](https://github.com/user-attachments/assets/4acf62ab-34d9-4109-a14c-84912600147e)


### 查看登录用户：who
who命令用于查看当前所有登录系统的用户信息。

常用选项：

![image](https://github.com/user-attachments/assets/d789b59e-ed7b-4fd7-9d90-983657efe547)

### 退出登录账户： exit
如果是图形界面，退出当前终端；

如果是使用ssh远程登录，退出登陆账户；

如果是切换后的登陆用户，退出则返回上一个登陆账号。

### 添加用户账号：useradd
在Unix/Linux中添加用户账号可以使用adduser或useradd命令，因为adduser命令是指向useradd命令的一个链接，因此，这两个命令的使用格式完全一样。

useradd命令的使用格式如下： useradd [参数] 新建用户账号

![image](https://github.com/user-attachments/assets/29669c53-78f6-4c76-9f4d-67eb7e759e3e)


相关说明：

- Linux每个用户都要有一个主目录，主目录就是第一次登陆系统，用户的默认当前目录(/home/用户)；
- 每一个用户必须有一个主目录，所以用useradd创建用户的时候，一定给用户指定一个主目录；
- 如果创建用户的时候，不指定组名，那么系统会自动创建一个和用户名一样的组名。

若创建用户时未指定家目录，后期可通过usermod -d /home/abc abc指定

![image](https://github.com/user-attachments/assets/9d44343c-9836-4167-b08a-364ef6af98d1)


### 修改用户：usermod
![image](https://github.com/user-attachments/assets/ea9becbe-20be-4005-b376-4860011de519)


### 设置用户密码：passwd
![image](https://github.com/user-attachments/assets/a8f7f440-4f27-498e-bab9-ef02ecb98f89)


### 删除用户：userdel
![image](https://github.com/user-attachments/assets/7749a8b8-c60a-4eb4-bccd-c289c7042a98)

### 切换用户：su
su后面可以加“-”会将当前的工作目录自动转换到切换后的用户主目录.

![image](https://github.com/user-attachments/assets/e28f01b9-c921-4b11-b168-7feb6f0e2ca7)


注意：对于ubuntu平台，只能通过sudo su进入root账号。

sudo允许系统管理员让普通用户执行一些或者全部的root命令的一个工具。

### 以root身份执行指令：sudo
![image](https://github.com/user-attachments/assets/37d3f24b-1719-4d07-871e-73cf6d7202bd)


### 添加、删除组账号：groupadd、groupdel
groupadd 新建组账号 groupdel 组账号 cat /etc/group 查看用户组

![image](https://github.com/user-attachments/assets/f2a5a804-0bfe-4427-bcda-f28fca161647)


### 用户组管理：groupmod
![image](https://github.com/user-attachments/assets/9607be49-3efe-405f-9ed8-ebb024dbbff7)


## 系统管理
### 查看当前日历：cal
cal命令用于查看当前日历，-y显示整年日历：

![image](https://github.com/user-attachments/assets/0d93e323-6b8f-47c2-833b-4acf931e59cd)


### 显示或设置时间：date
设置时间格式（需要管理员权限）：

![image](https://github.com/user-attachments/assets/6c1fc749-3623-4da1-8995-d4e4815160f1)

MM为月，DD为天，hh为小时，mm为分钟；CC为年前两位，YY为年的后两位，ss为秒。

如： date 010203042016.55。

显示时间格式（date ‘+%y,%m,%d,%H,%M,%S’）：

![image](https://github.com/user-attachments/assets/aa0b166c-c2aa-4b50-80a7-840cf03a9210)


### 查看网络状态：netstat
netstat命令用于显示网络状态。

利用netstat指令可让你得知整个Linux系统的网络情况。

语法：

![image](https://github.com/user-attachments/assets/019b3f94-5230-4b29-bdef-52a7da09289c)


参数说明：

- -a或–all 显示所有连线中的Socket。
- -A<网络类型>或–<网络类型> 列出该网络类型连线中的相关地址。
- -c或–continuous 持续列出网络状态。
- -C或–cache 显示路由器配置的快取信息。
- -e或–extend 显示网络其他相关信息。
- -F或–fib 显示FIB。
- -g或–groups 显示多重广播功能群组组员名单。
- -h或–help 在线帮助。
- -i或–interfaces 显示网络界面信息表单。
- -l或–listening 显示监控中的服务器的Socket。
- -M或–masquerade 显示伪装的网络连线。
- -n或–numeric 直接使用IP地址，而不通过域名服务器。
- -N或–netlink或–symbolic 显示网络硬件外围设备的符号连接名称。
- -o或–timers 显示计时器。
- -p或–programs 显示正在使用Socket的程序识别码和程序名称。
- -r或–route 显示Routing Table。
- -s或–statistice 显示网络工作信息统计表。
- -t或–tcp 显示TCP传输协议的连线状况。
- -u或–udp 显示UDP传输协议的连线状况。
- -v或–verbose 显示指令执行过程。
- -V或–version 显示版本信息。
- -w或–raw 显示RAW传输协议的连线状况。
- -x或–unix 此参数的效果和指定"-A unix"参数相同。
- –ip或–inet 此参数的效果和指定"-A inet"参数相同。

常用：

![image](https://github.com/user-attachments/assets/bde5df16-01eb-4765-9d37-eaf4b8a258f8)


### 查看进程信息：ps
进程是一个具有一定独立功能的程序，它是操作系统动态执行的基本单元。

ps命令选项：

- ps a 显示现行终端机下的所有程序，包括其他用户的程序。
- ps -A 显示所有程序。
- ps c 列出程序时，显示每个程序真正的指令名称，而不包含路 径，参数或常驻服务的标示。
- ps -e 此参数的效果和指定"A"参数相同。
- ps e 列出程序时，显示每个程序所使用的环境变量。
- ps f 用ASCII字符显示树状结构，表达程序间的相互关系。
- ps -H 显示树状结构，表示程序间的相互关系。
- ps -N 显示所有的程序，除了执行ps指令终端机下的程序之外。
- ps s 采用程序信号的格式显示程序状况。
- ps u 以用户为主的格式来显示程序状况。
- ps x 显示所有程序，不以终端机来区分。

![image](https://github.com/user-attachments/assets/df3c43c4-889a-4346-b377-de4fe492a86b)


常见用法：

- ps -e 查看所有进程信息（瞬时的）
- ps -u root -N 查看所有不是root运行的进程
- ps ax 显示所有进程状态状态
- ps -ef |grep xxx 显示含有xxx的进程

实例：

![image](https://github.com/user-attachments/assets/95ef183d-a0ed-481d-8ba9-b7343018267b)


显示指定用户信息：

![image](https://github.com/user-attachments/assets/b9bba7bf-b469-417c-a0aa-b582c880289a)


显示所有进程信息，连同命令行

![image](https://github.com/user-attachments/assets/57ad61f9-2dc1-41b7-8148-5e52f75f2c07)


### 以树状图显示进程关系：pstree
![image](https://github.com/user-attachments/assets/943e49e3-b5ac-455d-99ce-ede12aff67d4)



### 动态显示进程：top
top命令用来动态显示运行中的进程。top命令能够在运行后，在指定的时间间隔更新显示信息。-d参数可以指定显示信息更新的时间间隔。

在top命令执行后，可以按下按键得到对显示的结果进行排序：

![image](https://github.com/user-attachments/assets/11773fff-9555-4d8b-8bde-605e091f1104)

![image](https://github.com/user-attachments/assets/a9dd6744-9000-4803-a645-37908d6d324d)

更高级的命令是htop，但需要安装：

![image](https://github.com/user-attachments/assets/c16500d6-f784-4e87-97d4-fed5790d1b6d)


### 终止进程：kill
kill命令指定进程号的进程，需要配合 ps 使用。

使用格式：

![image](https://github.com/user-attachments/assets/24998b81-1934-421f-bbdb-d6fc10641848)


信号值从0到15，其中9为绝对终止，可以处理一般信号无法终止的进程。

### 关机重启：reboot、shutdown、init
![image](https://github.com/user-attachments/assets/d3811c52-7196-4920-bef2-0e46e7dd554d)


### 检测磁盘空间：df
df命令用于检测文件系统的磁盘空间占用和空余情况，可以显示所有文件系统对节点和磁盘块的使用情况。

![image](https://github.com/user-attachments/assets/913685cb-ade1-46dc-b006-89e460d5c0df)

![image](https://github.com/user-attachments/assets/895487c7-c949-4170-b0b2-afcf65e37b18)

### 检测目录所占磁盘空间：du
du命令用于统计目录或文件所占磁盘空间的大小，该命令的执行结果与df类似，du更侧重于磁盘的使用状况。

du命令的使用格式如下： du [选项] 目录或文件名
![image](https://github.com/user-attachments/assets/b00bc6b3-5b1a-4891-8292-5f3ec08c5ed2)

![image](https://github.com/user-attachments/assets/d6b465a6-0f92-4940-b2ce-b5d115e2b322)

### 查看或配置网卡信息：ifconfig
ifconfig显示所有网卡的信息：

![image](https://github.com/user-attachments/assets/a68e82b2-e814-4e4a-a6d9-187fec6c4c85)


修改ip:

![image](https://github.com/user-attachments/assets/8fd009ec-6e06-45c5-afa0-c3b196a86f62)


### 测试远程主机连通性：ping

```txt
python@ubuntu:~$ ping 192.168.40.1
PING 192.168.40.1 (192.168.40.1) 56(84) bytes of data.
64 bytes from 192.168.40.1: icmp_seq=1 ttl=64 time=0.699 ms
64 bytes from 192.168.40.1: icmp_seq=2 ttl=64 time=0.372 ms
^C
--- 192.168.40.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.372/0.535/0.699/0.165 ms
python@ubuntu:~$ ping 192.168.40.1 -c 3
PING 192.168.40.1 (192.168.40.1) 56(84) bytes of data.
64 bytes from 192.168.40.1: icmp_seq=1 ttl=64 time=0.409 ms
64 bytes from 192.168.40.1: icmp_seq=2 ttl=64 time=0.367 ms
64 bytes from 192.168.40.1: icmp_seq=3 ttl=64 time=0.373 ms

--- 192.168.40.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2000ms
rtt min/avg/max/mdev = 0.367/0.383/0.409/0.018 ms
python@ubuntu:~$ 
```

## Linux 磁盘管理
Linux磁盘管理常用三个命令为df、du和fdisk。

df：列出文件系统的整体磁盘使用量
du：检查磁盘空间使用量
fdisk：用于磁盘分区

### df
获取硬盘被占用了多少空间，目前还剩下多少空间等信息。

语法：

```txt
df [-ahikHTm] [目录或文件名]
```

选项与参数：

- -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；
- -k ：以 KBytes 的容量显示各文件系统；
- -m ：以 MBytes 的容量显示各文件系统；
- -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；
- -H ：以 M=1000K 取代 M=1024K 的进位方式；
- -T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；
- -i ：不用硬盘容量，而以 inode 的数量来显示

```txt
[root@VM_0_9_centos ~]# df -hT
Filesystem     Type      Size  Used Avail Use% Mounted on
/dev/vda1      ext4       50G  4.9G   42G  11% /
devtmpfs       devtmpfs  909M     0  909M   0% /dev
tmpfs          tmpfs     920M   24K  920M   1% /dev/shm
tmpfs          tmpfs     920M  496K  919M   1% /run
tmpfs          tmpfs     920M     0  920M   0% /sys/fs/cgroup
tmpfs          tmpfs     184M     0  184M   0% /run/user/0
```

将系统内的所有特殊文件格式及名称都列出来

```txt
[root@www ~]# df -aT
Filesystem    Type 1K-blocks    Used Available Use% Mounted on
/dev/hdc2     ext3   9920624 3823112   5585444  41% /
proc          proc         0       0         0   -  /proc
sysfs        sysfs         0       0         0   -  /sys
devpts      devpts         0       0         0   -  /dev/pts
/dev/hdc3     ext3   4956316  141376   4559108   4% /home
/dev/hdc1     ext3    101086   11126     84741  12% /boot
tmpfs        tmpfs    371332       0    371332   0% /dev/shm
none   binfmt_misc         0       0         0   -  /proc/sys/fs/binfmt_misc
sunrpc  rpc_pipefs         0       0         0   -  /var/lib/nfs/rpc_pipefs
```

### du
du命令是对文件和目录磁盘使用的空间的查看.

语法：

```txt
du [-ahskm] 文件或目录名称
```

选项与参数：

- -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已。
- -h ：以人们较易读的容量格式 (G/M) 显示；
- -s ：列出总量而已，而不列出每个各别的目录占用容量；
- -S ：不包括子目录下的总计，与 -s 有点差别。
- -k ：以 KBytes 列出容量显示；
- -m ：以 MBytes 列出容量显示；

du没有加任何选项时，只列出当前目录下的所有文件夹容量（包括隐藏文件夹）:

```txt
[root@www ~]# du
8       ./test4     <==每个目录都会列出来
8       ./test2
....中间省略....
12      ./.gconfd   <==包括隐藏文件的目录
220     .           <==这个目录(.)所占用的总量
```

直接输入 du 没有加任何选项时，则 du 会分析当前所在目录的文件与目录所占用的硬盘空间。

加-a选项才显示文件的容量：

```txt
[root@www ~]# du -a
12      ./install.log.syslog   <==有文件的列表了
8       ./.bash_logout
8       ./test4
8       ./test2
....中间省略....
12      ./.gconfd
220     .
```

检查根目录底下每个目录所占用的容量

```txt
[root@www ~]# du -sh /*
0       /bin
108M    /boot
4.0K    /data
.....中间省略....
0       /proc
.....中间省略....
40K     /tmp
2.4G    /usr
2.4G    /var
```

### fdisk
fdisk 是 Linux 的磁盘分区表操作工具。

语法：

```txt
fdisk [-l] 装置名称
```

选项与参数：

- -l ：输出后面接的装置所有的分区内容。若仅有 fdisk -l 时， 则系统将会把整个系统内能够搜寻到的装置的分区均列出来。

列出所有分区信息：

```txt
[root@AY120919111755c246621 tmp]# fdisk -l

Disk /dev/xvda: 21.5 GB, 21474836480 bytes
255 heads, 63 sectors/track, 2610 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00000000

    Device Boot      Start         End      Blocks   Id  System
/dev/xvda1   *           1        2550    20480000   83  Linux
/dev/xvda2            2550        2611      490496   82  Linux swap / Solaris

Disk /dev/xvdb: 21.5 GB, 21474836480 bytes
255 heads, 63 sectors/track, 2610 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x56f40944

    Device Boot      Start         End      Blocks   Id  System
/dev/xvdb2               1        2610    20964793+  83  Linux
```

查看根目录所在磁盘，并查阅该硬盘内的相关信息：

```txt
[root@www ~]# df /            <==注意：重点在找出磁盘文件名而已
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/hdc2              9920624   3823168   5585388  41% /

[root@www ~]# fdisk /dev/hdc  <==不要加上数字！
The number of cylinders for this disk is set to 5005.
There is nothing wrong with that, but this is larger than 1024,
and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
   (e.g., DOS FDISK, OS/2 FDISK)

Command (m for help):     <==等待你的输入！
```

输入 m 后，就会看到底下这些命令介绍

```txt
Command (m for help): m   <== 输入 m 后，就会看到底下这些命令介绍
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition            <==删除一个partition
   l   list known partition types
   m   print this menu
   n   add a new partition           <==新增一个partition
   o   create a new empty DOS partition table
   p   print the partition table     <==在屏幕上显示分割表
   q   quit without saving changes   <==不储存离开fdisk程序
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit  <==将刚刚的动作写入分割表
   x   extra functionality (experts only)
```

离开 fdisk 时按下 q，那么所有的动作都不会生效！相反的， 按下w就是动作生效的意思。

```txt
Command (m for help): p  <== 这里可以输出目前磁盘的状态

Disk /dev/hdc: 41.1 GB, 41174138880 bytes        <==这个磁盘的文件名与容量
255 heads, 63 sectors/track, 5005 cylinders      <==磁头、扇区与磁柱大小
Units = cylinders of 16065 * 512 = 8225280 bytes <==每个磁柱的大小

   Device Boot      Start         End      Blocks   Id  System
/dev/hdc1   *           1          13      104391   83  Linux
/dev/hdc2              14        1288    10241437+  83  Linux
/dev/hdc3            1289        1925     5116702+  83  Linux
/dev/hdc4            1926        5005    24740100    5  Extended
/dev/hdc5            1926        2052     1020096   82  Linux swap / Solaris
# 装置文件名 启动区否 开始磁柱    结束磁柱  1K大小容量 磁盘分区槽内的系统

Command (m for help): q
```


使用 p 可以列出目前这颗磁盘的分割表信息，这个信息的上半部在显示整体磁盘的状态。

### 磁盘格式化
磁盘分割完毕后自然就是要进行文件系统的格式化，格式化的命令非常的简单，使用 mkfs（make filesystem） 命令。

语法：

```txt
mkfs [-t 文件系统格式] 装置文件名
```

选项与参数：

- -t ：可以接文件系统格式，例如 ext3, ext2, vfat 等(系统有支持才会生效)

查看 mkfs 支持的文件格式：

```txt
[root@VM_0_9_centos web]# mkfs[tab]
mkfs         mkfs.cramfs  mkfs.ext3    mkfs.minix   
mkfs.btrfs   mkfs.ext2    mkfs.ext4    mkfs.xfs
```

按下两个[tab]，会发现 mkfs 支持的文件格式如上所示。

将分区 /dev/hdc6（可指定其他分区） 格式化为ext3文件系统：

```txt
[root@www ~]# mkfs -t ext3 /dev/hdc6
mke2fs 1.39 (29-May-2006)
Filesystem label=                <==这里指的是分割槽的名称(label)
OS type: Linux
Block size=4096 (log=2)          <==block 的大小配置为 4K 
Fragment size=4096 (log=2)
251392 inodes, 502023 blocks     <==由此配置决定的inode/block数量
25101 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=515899392
16 block groups
32768 blocks per group, 32768 fragments per group
15712 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912

Writing inode tables: done
Creating journal (8192 blocks): done <==有日志记录
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 34 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
# 这样就创建起来我们所需要的 Ext3 文件系统了！简单明了！
```

### 磁盘检验
fsck（file system check）用来检查和维护不一致的文件系统。

若系统掉电或磁盘发生问题，可利用fsck命令对文件系统进行检查。

语法：

```txt
fsck [-t 文件系统] [-ACay] 装置名称
```

选项与参数：

- -t : 给定档案系统的型式，若在 /etc/fstab 中已有定义或 kernel 本身已支援的则不需加上此参数
- -s : 依序一个一个地执行 fsck 的指令来检查
- -A : 对/etc/fstab 中所有列出来的 分区（partition）做检查
- -C : 显示完整的检查进度
- -d : 打印出 e2fsck 的 debug 结果
- -p : 同时有 -A 条件时，同时有多个 fsck 的检查一起执行
- -R : 同时有 -A 条件时，省略 / 不检查
- -V : 详细显示模式
- -a : 如果检查有错则自动修复
- -r : 如果检查有错则由使用者回答是否修复
- -y : 选项指定检测每个文件是自动输入yes，在不确定那些是不正常的时候，可以执行 # fsck -y 全部检查修复。

查看系统有多少文件系统支持的 fsck 命令：

```txt
[root@www ~]# fsck[tab][tab]
fsck         fsck.cramfs  fsck.ext2    fsck.ext3    fsck.msdos   fsck.vfat
```

强制检测 /dev/hdc6 分区:

```txt
[root@www ~]# fsck -C -f -t ext3 /dev/hdc6 
fsck 1.39 (29-May-2006)
e2fsck 1.39 (29-May-2006)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
vbird_logical: 11/251968 files (9.1% non-contiguous), 36926/1004046 blocks
```

如果没有加上 -f 的选项，则由于这个文件系统不曾出现问题，检查的经过非常快速！若加上 -f 强制检查，才会一项一项的显示过程。

### 磁盘挂载与卸除
Linux 的磁盘挂载使用 mount 命令，卸载使用 umount 命令。

磁盘挂载语法：

```txt
mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n]  装置文件名  挂载点
```

用默认的方式，将刚刚创建的 /dev/hdc6 挂载到 /mnt/hdc6 上面！

```txt
[root@www ~]# mkdir /mnt/hdc6
[root@www ~]# mount /dev/hdc6 /mnt/hdc6
[root@www ~]# df
Filesystem           1K-blocks      Used Available Use% Mounted on
.....中间省略.....
/dev/hdc6              1976312     42072   1833836   3% /mnt/hdc6
```

磁盘卸载命令 umount 语法：

```txt
umount [-fn] 装置文件名或挂载点
```

选项与参数：

- -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下；
- -n ：不升级 /etc/mtab 情况下卸除。

卸载/dev/hdc6

```txt
[root@www ~]# umount /dev/hdc6     
```
