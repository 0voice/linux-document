# Linux shell及常用36类命令汇总

## 

使用Linux shell是一些程序员每天的基本工作，但我们经常会忘记一些有用的shell命令和技巧。当然，命令我能记住，但我不敢说能记得如何用它执行某个特定任务。需要注意一点的是，有些用法需要在你的linux系统里安装额外的软件。

shell是一种命令解释器，它提供了用户和操作系统之间的交互接口。shell是面向命令行的，而 X Window 则是图形界面。你在命令行输入命令，shell进行解释，然后送往操作系统执行。

shell可以执行 Linux 的系统内部命令，也可以执行应用程序。你还可以利用shell编程，执行复杂的命令程序。

Linux 提供几种shell程序以供选择。常用的有 Bourne ( b s h )、C( c s h )和Korn( k s h )，各个shell都能提供基本的功能，又有其各自的特点。

#### Bourne shell 

Bourne shell是由Steven Bourne 编写的，是UNIX 的缺省shell。Bourne shell的shell编程能力很强。但它不能处理命令的用户交互特征。bash 是Bourne shell的增强版。

#### Cshell 

Cshell是由加利福尼亚大学伯克利分校的Bill Joy编写的。它能提供Bourne shell所不能处理的用户交互特征，如命令补全、命令别名、历史命令替换等。很多人认为， C shell的编程能力不如Bourne shell，但它的语法和C语言类似，所以C程序员将发现C shell很顺手。tcsh 是Cshell的增强版本和Cshell完全兼容。

#### Korn 

K o r nshell是由Dave Korn 编写的。Korn shell融合了C shell和Bourne shell的优点，并和Bourne shell完全兼容。 Korn shell的效率很高，其命令交互界面和编程交互界面都很不错。Public Domain Korn shell( p d k s h )是Korn shell的增强版。

#### bash 

bash 是大多数L i n u x系统的缺省shell。它克服了Bourne shell的缺点，又和Bourne shell完全

兼容，B a s h有以下的特点：

> 1 补全命令行。 当你在bash 命令提示符下输入命令或程序名时，你不必输全命令或程序
>
> 名，按Tab 键，b a s h将自动补全命令或程序名。
>
> 2 通配符。 在b a s h下可以使用通配符 * 和？。*可以替代多个字符，而？则替代一个字符。
>
> 3 历史命令。 bash 能自动跟踪你每次输入的命令，并把输入的命令保存在历史列表缓冲区。
>
> 缓冲区的大小由HISTSIZE 变量控制。当你每次登录后，home 目录下的 .bash_history 文
>
> 件将初始化你的历史列表缓冲区。你也能通过history 和fc 命令执行、编辑历史命令。
>
> 4别名。 在b a s h下，可用alias 和unalias 命令给命令或可执行程序起别名和清除别名。这
>
> 样你可以用自己习惯的方式输入命令。

进入shell

Linux 启动后，给出 login 命令，等待用户登录。

Login: <输入用户名>

Password: <输入密码>

如果是正确的用户名和密码，那么你就会进入Linux 的shell， shell给出命令提示符，等待

你输入命令。使用 l o g o u t命令退出shell。

#### **shell的常用命令**

------

> 1、更改帐号密码

语法：passwd

Old password: <输入旧密码>

New password: <输入新密码〉

Retype new password: <再输入一次密码>

> 2、联机帮助

语法： man 命令

例如:

man ls

> 3、远程登录

语法：rlogin 主机名 [-l 用户名]

例如：

rlogin aa     远程登录到工作站 aa 中。

rlogin aa -l user 使用 user 帐号登录到工作站 aa 中。

语法：telnet 主机名 或 telnet IP地址

例如：

telnet aa

telnet 130.129.21.250

> 3、文件或目录处理

列出文件或目录下的文件名。

语法： ls [-atFlgR] [name]

ls 列出目前目录下的文件名。

ls -a 列出包括以 ．开始的隐藏文件的所有文件名。

ls -t 依照文件最后修改时间的顺序列出文件名。

ls -F 列出当前目录下的文件名及其类型。以/ 结尾表示为目录名，以* 结尾表示为

可执行文件，以@ 结尾表示为符号连接。

ls -l 列出目录下所有文件的权限、所有者、文件大小、修改时间及名称。

ls -lg 同上，并显示出文件的所有者工作组名。

ls -R 显示出目录下以及其所有子目录的文件名。

> 4、改变工作目录

语法：cd [name]

name：目录名、路径或目录缩写。

例如:

cd 改变目录位置至用户登录时的工作目录。

cd dir 改变目录位置至d i r目录下。

cd user 改变目录位置至用户的工作目录。

cd .. 改变目录位置至当前目录的父目录。

cd ../user 改变目录位置至相对路径 user 的目录下。

cd /../.. 改变目录位置至绝对路径的目录位置下。

cd 改变目录位置至用户登录时的工作目录。

> 5、复制文件

语法: cp [-r] 源地址 目的地址

例如：

cp file1 file2 将文件 file1 复制成 f i l e 2。

cp file1 dir1 将文件 file1 复制到目录 dir1 下，文件名仍为 f i l e 1。

cp /tmp/file1 . 将目录 /tmp 下的文件 file1 复制到当前目录下，文件名仍为 f i l e 1。

cp /tmp/file1 file2 将目录 /tmp 下的文件 file1 复制到当前目录下，文件名为f i l e 2。

cp -r dir1 dir2 复制整个目录。

> 6、移动或更改文件、目录名称

语法：mv 源地址 目的地址

例如：

mv file1 file2 将文件 f i l e 1更名为 f i l e 2。

mv file1 dir1 将文件 f i l e 1移到目录 dir1 下，文件名仍为 f i l e 1。

mv dir1 dir2 将目录 dir1 更改为目录 d i r 2。

> 7、建立新目录

语法： mkdir 目录名

mkdir dira 建立一新目录 d i ra。

> 8、删除目录

语法： rmdir 目录名 或 rm 目录名

例如：

rmdir dir1 删除目录 d i r 1，但 dir1 下必须没有文件存在，否则无法删除。

rm -r dir1 删除目录 d i r 1及其子目录下所有文件。

> 9、删除文件

语法： rm 文件名

例如：

rm file1 删除文件名为 file1 的文件。

rm file? 删除文件名中有五个字符且前四个字符为file 的所有文件。

rm f* 删除文件名中以 f 为字首的所有文件。

> 10、列出当前所在的目录位置

语法： p w d

> 11、查看文件内容

语法： cat 文件名

例如：

cat file1 以连续显示方式，查看文件名 file1 的内容。

> 12、分页查看文件内容

语法： more 文件名 或 cat 文件名 | more

例如：

more file1 以分页方式查看文件名 file1 的内容。

cat file1 | more 以分页方式查看文件名 file1 的内容。

> 13、查看目录所占磁盘容量

语法: du [-s] 目录

例如:

du dir1 显示目录 dir1 的总容量及其子目录的容量(以KB 为单位)。

du -s dir1 显示目录 dir1 的总容量。

> 14、文件传输

\1. 拷贝文件或目录至远程工作站

语法： rcp [-r] 源地址 主机名:目的地址

源地址文件名、目录名或路径。

例如：

rcp file1 doc:/home/user   将文件f i l e 1拷贝到工作站 doc 路径 /home/user 下。

rcp -r dir1 doc:/home/user   将目录 d i r 1拷贝到工作站 doc 路径/home/user 下。

\2. 自远程工作站，拷贝文件或目录

语法： rcp [-r] 主机名:源地址 目的地址

主机名工作站名。

源地址路径名。

目的地址、文件名、目录名或路径 。

例如：

rcp doc:/home/user/file1 file2   将工作站 d o c路径/home/user 下的目录 d i r 1，拷贝到当前工

作站的目录下，目录名仍为 d i r 1。

rcp -r doc:/home/user/dir1 .   将工作站doc 路径/home/user 下的目录 d i r 1，拷贝到当前工

作站的目录下，目录名仍为 d i r 1。

\3. 本地工作站与远程工作站之间的文件传输

必须拥有远程工作站的帐号及密码，才可进行传输工作。

语法： ftp 主机名 或 ftp ip地址

例如：

ftp doc 与远程工作站 doc 之间进行文件传输。

Name (doc:user-name): <输入帐号>

Password (doc:user-password): <输入密码>

ftp> help 列出 ftp 文件传输时可使用的命令。

ftp> !ls 列出本地工作站当前目录下的所有文件名。

ftp> !pwd 列出本地工作站当前所在的目录位置。

ftp> ls 列出远程工作站当前目录下的所有文件名。

ftp> dir 列出远程工作站当前目录下的所有文件名。

ftp> dir . |more 分页列出远程工作站当前目录下的所有文件名。

ftp> pwd 列出远程工作站当前所在的目录位置。

ftp> cd dir1 更改远程工作站的工作目录位置至 dir1 之下。

ftp> get file1 将远程工作站的文件 f i l e 1拷贝到本地工作站中。

ftp> put file2 将本地工作站的文件 f i l e 2拷贝到远程工作站中。

ftp> mget *.c 将远程工作站中扩展文件名为 c 的所有文件拷贝到本地工作站中。

ftp> mput *.txt 将本地工作站中扩展文件名为 txt 的所有文件拷贝到远程工作站中。

ftp> prompt 切换交互式指令(使用 mput/mget 时不是每个文件皆询问y e s / n o )。

ftp> quit 结束 ftp 工作。

ftp> bye 结束 ftp 工作。

注意 从PC与工作站间的文件传输也可透过在 PC端的 FTP指令进行文件传输，指令用

法与上述指令大致相同。

> 15、文件权限的设定

\1. 改变文件或目录的读、写、执行权限

语法：chmod [-R] mode name

n a m e :文件名或目录名。

mode: 3个8位数字或r w x的组合。r- r e a d (读)，w - w r i t e (写)，x - e x e c u t e (执行)，u - u s e r (当前用

户)，g - g r o u p（组） ，o - o t h e r（其他用户） 。

例如:

chmod 755 dir1 对于目录d i r 1，设定成任何使用者皆有读取及执行的权利，但只有所

有者可做修改。

chmod 700 file1 对于文件f i l e 1，设定只有所有者可以读、写和执行的权利。

chmod u+x file2 对于文件f i l e 2，增加当前用户可以执行的权利。

chmod g+x file3 对于文件f i l e 3，增加工作组使用者可执行的权利。

chmod o-r file4 对于文件f i l e 4，删除其他使用者可读取的权利。

2．改变文件或目录的所有权

语法：chown [-R] 用户名 name

n a m e：文件名或目录名。

例如 ：

chown user file1 将文件 file1 改为用户user 所有。

chown -R user dir1 将目录 d i r 1及其子目录下面的所有文件改为用户user 所有。

> 16、检查自己所属的工作组名称

语法：g r o u p s

> 17、 改变文件或目录工作组所有权

语法：chgrp [-R] 工作组名 name

n a m e：文件名或目录名

例如：

chgrp vlsi file1 将文件 file1 的工作组所有权改为 vlsi 工作组所有。

chgrp -R image dir1 将目录d i r 1及其子目录下面的所有文件，改为 image 工作组所有。

> 18、 改变文件或目录的最后修改时间

语法：touch name

n a m e：文件名或目录名。

> 19、文件的链接

同一文件，可拥有一个以上的名称，也就是把一个文件进行链接。

语法：ln 老文件名 新文件名

例如 ：

ln file1 file2 将文件 f i l e 2链接至文件 f i l e 1。

语法：ln -s 老文件名 新文件名

例如 ：

ln -s file3 file4 将文件 file4 链接至文件f i l e 3。

> 20、文件中字符串的查寻

语法：grep string file

例如 ：

grep abc file1   寻找文件f i l e 1中包含字符串 abc 所在行的文本内容。

查寻文件或命令的路径

语法：whereis command 显示命令的路径。

语法：which command 显示命令的路径，及使用者所定义的别名。

语法：whatis command 显示命令功能的摘要。

语法：find search-path -name filename -print   搜寻指定路径下某文件的路径 。

例如 ：

find / -name file1 -print 自根目录下寻找文件 file1 的路径。

> 21、比较文件或目录的内容

语法：d i ff [-r] name1 name2

name1 name2：可同时为文件名或目录名。

例如：

d i ff file1 file2 比较文件file1 与 file2 内各行的不同之处。

d i ff -r dir1 dir2 比较目录 dir1 与 dir2 内各文件的不同之处。

> 22、文件打印输出

用户可用 .login 文件中的 setenv PRINTER来设定打印机名。

例如 ：

setenv PRINTER sp 设定自 sp 打印机打印资料。

一般文件的打印

语法：lpr [-P打印机名] 文件名

例如：

lpr file1 或 lpr -Psp file1   自 s p打印机打印文件 f i l e 1。

语法：enscript [-P打印机名] 文件名

例如：

enscript file3 或 enscript -Psp file3   自 s p打印机打印文件 f i l e 3。

> 23、troff 文件的打印

语法：p t r o ff [-P打印机名] [-man][-ms] 文件名

例如：

ptroff -Psp -man /usr/man/man1/lpr1   以troff 格式，自 sp 打印机打印lpr1 命令的使用说明。

打印机控制命令

1．检查打印机状态、打印作业顺序号和用户名

第2章计shell及常用命令计计 15

下载

语法：lpq [-P打印机名]

例如：

lpq 或 lpq -Psp   检查 sp 打印机的状态。

\2. 删除打印机内的打印作业( 用户仅可删除自己的打印作业 )

语法：lprm [-P打印机名] 用户名 或 作业编号

例如：

lprm user或lprm -Psp user   删除s p打印机中用户user 的打印作业，此时用户名必须为u s e r。

lprm -Psp 456   删除 sp 打印机上编号为 456 的打印作业。

> 24、进程控制

1．查看系统中的进程

语法：ps [-aux]

例如:

p s或ps -x 查看系统中，属于自己的进程。

ps -au 查看系统中，所有用户的进程。

ps -aux 查看系统中，包含系统内部的及所有用户的进程。

\2. 结束或终止进程

语法：kill [-9] PID

P I D：利用 ps 命令所查出的进程号。

例如:

kill 456或kill -9 456   终止进程号为 456 的进程。

\3. 在后台执行进程的方式

语法：命令 &

例如:

cc file1.c &   将编译 file1.c 文件的工作置于后台执行。

语法：按下 C o n t r o l + Z键，暂停正在执行的进程。键入b g命令，将暂停的进程置于后台继

续执行。

例如:

cc file2.c

^ Z

S t o p p e d

b g

\4. 查看正在后台中执行的进程

语法：j o b s

\5. 结束或终止后台中的进程

语法：kill %n

n：利用j o b s命令查看出的后台作业号

例如：

kill % 终止在后台中的第一个进程。

kill %2 终止在后台中的第二个进程。

> 25、shell变量

\1. 查看shell变量的设定值

语法：set 查看所有shell变量的设定值。

语法：echo $变量名 显示指定的shell变量的设定值。

\2. 设定shell变量

语法：set var = value

例如:

set term=vt100   设定shell变量 t e r m为 VT100 型终端。

\3. 删除shell变量

语法：unset var

例如:

unset PRINTER   删除shell变量 PRINTER 的设定值。

> 26、别名

\1. 查看所定义的命令的别名

语法： a l i a s 查看自己目前定义的所有命令，及所对应的别名。

语法： alias name 查看指定的name 命令的别名。

例如:

alias dir 查看别名 dir 所定义的命令。

ls -atl

\2. 定义命令的别名

语法： alias name‘command line’

例如:

alias dir ‘ls -l’ 将命令 ls - l 定义别名为 d i r。

\3. 删除所定义的别名

语法： unalias name

例如：

unalias dir 删除别名 dir 的定义。

unalias * 删除所有别名的设定。

> 27、历史命令

\1. 设定命令记录表的长度

语法： set history = n

例如:

set history = 40   设定命令记录表的长度为 40 (可记录执行过的前面 40 个命令)。

\2. 查看命令记录表的内容

语法： h i s t o r y

\3. 使用命令记录表

语法： !!   重复执行前一个命令。

语法： ! n

n：命令记录表的命令编号。

语法： ! s t r i n g 重复前面执行过的以 string 为起始字符串的命令。

例如: ! c a t 重复前面执行过的以 cat 为起始字符串的命令。

\4. 显示前一个命令的内容

语法： ! !：p

\5. 更改前一个命令的内容并执行

语法： ^oldstring ^newstring   将前一个命令中 oldstring 的部份改成 n e w s t r i n g并执

行。

例如：

find . -name file1.c -print

^ f i l e 1 . c ^ c o r e

find . -name core -print

> 28、文件的压缩

\1. 压缩文件

语法：compress 文件名 压缩文件

语法：compressdir 目录名 压缩目录

\2. 解压缩文件

语法：uncompress 文件名 解压缩文件

语法：uncompressdir 目录名 解压缩目录

> 29、管道命令的使用

语法：命令1 | 命令2   将命令1的执行结果送到命令2，做为命令2的输入。

例如：

ls -Rl | more   以分页方式列出当前目录及其子目录下所有文件的名称。

cat file1 | more   以分页方式列出文件 file1 的内容。

30、输入/输出控制

\1. 标准输入的控制

语法：命令 < 文件 将文件做为命令的输入。

例如：

mail -s “mail test” 电子邮件地址 < file1  将文件file 当做信件的内容，主

题名称为 mail test，送给收信人。

\2. 标准输出的控制

语法：命令 > 文件 将命令的执行结果送至指定的文件中。

例如:

ls -l > list   将执行 “ls -l” 命令的结果写入文件list 中。

语法：命令>! 文件 将命令的执行结果送至指定的文件中，若文件已经存在，则覆盖。

例如：

ls -lg >! list   将执行 “ls - lg” 命令的结果覆盖写入文件 list 中。

语法：命令 >& 文件 将命令执行时屏幕上所产生的任何信息写入指定的文件中。

例如：

cc file1.c >& error   将编译 file1.c 文件时所产生的任何信息写入文件 error 中。

语法：命令>> 文件 将命令执行的结果附加到指定的文件中。

例如:

ls - lag >> list   将执行 “ls - lag” 命令的结果附加到文件 list 中。

语法：命令 >>& 文件 将命令执行时屏幕上所产生的任何信息附加到指定的文件中。

例如:

cc file2.c >>& error   将编译 file2.c 文件时屏幕所产生的任何信息附加到文件error 中。

> 31、查看系统中的用户

语法： who 或 f i n g e r

语法： w

语法： finger 用户名 或 finger 用户名@域名

改变用户名

语法： su 用户名

例如:

su user 进入用户user 的帐号。

p a s s w r o d : <输入用户user 的密码>

> 32、查看用户名

语法： who am i 查看登录时的用户名。

语法： w h o a m i 查看当前的用户名。若已执行过s u命令，则显示出此用户的用

户名。

> 33、查看当前系统上所有工作站的用户

语法: rusers

按Ctrl+C> 结束

> 34、与某工作站上的用户交谈

语法: talk 用户名@主机名或talk 用户名@ I P地址

例如:

\1) 可先利用 rusers 指令查看网络上的用户；

\2) 假设自己的帐号是 ddd ，在工作站 aaa上使用，现在想要与 bbb 上的ccc 交谈。

talk ccc@bbb

可按Ct r l + C结束。

> 35、检查网络是否连通

语法：ping 主机名或ping IP地址

> 36、电子邮件的使用简介

\1. 将文件当做电子邮件的内容送出

语法：mail -s “主题”电子邮件地址 < 文件

例如：

mail -s “hello” 电子邮件地址 < file.c

\2. 传送电子邮件给本系统用户

语法：mail 用户名

\3. 传送电子邮件至外地用户

语法： mail 电子邮件地址

例如：

mail xxx@163.com

Subject : mail test

:

按下 Ctrl+D 键或 . 键结束正文。

连按两次C t r l + C键则中断工作，不送此信件。

Cc( Carbon copy) : 复制一份正文，给其他的收信人。

\3. 检查所传送的电子邮件是否送出，或滞留在邮件服务器中

语法：/usr/magedu/sendmail -bp

若屏幕显示为 “Mail queue is empty” 的信息，表示 mail 已送出。

若为其他错误信息，表示电子邮件因故尚未送出。



原文地址：https://mp.weixin.qq.com/s/euh8YCm5IQN7pTm5JVObjA
