# Shell脚本：常用100个shell命令使用讲解题



在大多数的Linux和Unix系统、及其他类Unix系统中，Shell是用户与操作系统内核交互的主要方式。作为一种强大的命令行解释器，它也支持编程功能，用户可以写脚本来处理各种任务。

无论你是新手还是专业人士，掌握Shell命令都是必不可少的技能。在这篇文章中，我将逐个解读和展示Shell脚本中最常用的100个命令，并为每个命令提供实际的例子。

------

# 目录

- 文件操作命令
- 搜索命令
- 目录操作命令
- 权限操作命令
- 网络操作命令
- 进程和系统控制命令
- 文本操作命令
- 压缩与解压命令
- 磁盘使用管理命令
- 包管理命令
- 进程管理命令
- 环境变量命令
- 系统信息发布命令
- 系统控制命令
- 文本编辑命令
- 其他有用命令

------

# 文件操作命令

以下是在Linux系统中操作文件的一些常用命令：

1. ls：列出目录的内容

```
ls /home
```

1. cd：改变目录

```
cd /home/user/Documents
```

1. pwd：打印当前工作目录

```
pwd
```

1. cat：查看文件内容

```
cat /etc/passwd
```

1. more：分页查看文件内容

```
more /var/log/syslog
```

1. less：反向分页查看文件内容

```
less /var/log/syslog
```

1. touch：创建一个空文件或更改文件的访问和修改时间

```
touch /home/user/newfile.txt
```

1. cp：复制文件或目录

```
cp /home/user/file.txt /home/user/Documents
```

1. mv：移动或重命名文件或目录

```
mv /home/user/file.txt /home/user/Documents/newfile.txt
```

1. rm：删除文件或目录

```
rm /home/user/unwantedfile.txt
```

1. find：在文件系统中搜索文件或目录

```
find / -name "*.log"
```

1. grep：在文件中搜索具有特定模式的行

```
grep "error" /var/log/syslog
```

1. head：输出文件的开始部分

```
head -n 10 /var/log/syslog
```

1. tail：输出文件的尾部

```
tail -n 20 /var/log/syslog
```

1. sort：对文本文件的行进行排序

```
sort /etc/passwd
```

1. wc：计算字数、行数和字节数

```
wc /var/log/syslog
```

1. cut：从文件的每一行中剪切字节、字符和字段

```
cut -d: -f1 /etc/passwd
```

1. nano,vi,emacs：常用的文本编辑器

```
nano /home/user/file.txt
vi /home/user/file.txt
emacs /home/user/file.txt
```

1. paste：合并文件的行。

```
paste file1.txt file2.txt
```

------

# 搜索命令

以下命令可以帮助你搜索文件或文本：

1. find：在文件系统中搜索文件或目录。

```
find / -name "*.log"
```

1. grep：在文本文件中搜索决定的文本模式。

```
grep "error" /var/log/syslog
```

1. locate：基于文件名在数据库中快速找到文件。

```
locate myFile.txt
```

1. which：返回可执行文件的路径。

```
which java
```

1. ack：特别为程序员设计的一款文件搜索工具。默认会忽略多数版本控制文件夹（如.git, .svn等）的内容。

```
ack "your_search_term"
```

1. ag（The Silver Searcher）：比ack更快的代码搜索工具，同样默认忽略 .git 等版本控制文件夹中的内容。

```
ag "your_search_term"
```

1. whereis：此命令可用于查找二进制程序、源文件、手册页以及其他文件的位置。

```
whereis ls
```

1. type：此命令用于确定某个命令是内部 shell 命令、可执行文件还是别名。

```
type pwd
```

1. apropos：如果你只记得关于某个命令的部分信息，你可以使用 apropos 命令来搜索帮助手册中的命令描述。

```
apropos partition
```

1. alias：如果你经常使用某些 Linux 命令，你可以使用 alias 命令为这些常用命令创建一个短名，以提升你的工作效率。

```
alias l='ls -al'
```

------

# 目录操作命令

以下是在Linux系统中操作目录的一些常用命令：

1. mkdir：创建一个新的目录

```
mkdir /home/user/new_directory
```

1. rmdir：删除一个空目录

```
rmdir /home/user/empty_directory
```

1. tree：以树形结构列出目录的内容

```
tree /home/user/
```

1. du：估计文件和目录的磁盘使用空间

```
du -sh /home/user/Documents
```

1. df：显示磁盘使用空间

```
df -h
```

------

# 权限操作命令

在Linux系统中，文件和目录的访问可以通过权限操作命令进行控制：

1. chmod：更改文件或目录的权限

```
 chmod 755 /home/user/file.txt
表示设置文件的主用户有读，写和执行权限（rwx = 7），同组的用户和其他用户有读和执行权限（rx = 5）。
```

1. chown：更改文件或目录的所有者和所属的组

```
chown newuser:newgroup /home/user/file.txt
表示将/home/user/file.txt的所有者更改为newuser，所属的组更改为newgroup。
```

1. chgrp：更改文件或目录的所属组

```
chgrp newgroup /home/user/file.txt
表示将/home/user/file.txt的所属的组更改为newgroup。
```

------

# 网络操作命令

以下是在Linux系统中与网络相关的一些常用命令：

1. ping：发送网络请求以测试网络连接

```
ping www.google.com
```

1. ifconfig：显示或配置网络接口

```
ifconfig eth0
```

1. netstat：显示网络连接、路由表等网络状态信息

```
netstat -ntlp
```

1. ssh：远程登录或执行远程命令

```
 ssh user@remote_host
```

1. scp：在本地和远程系统之间安全地复制文件

```
scp /path/to/file user@remote_host:/remote/path/
```

1. curl：获取网络资源

```
curl www.google.com
```

1. telnet：远程登录工具

```
 telnet remote_host 23
```

1. nslookup：查询 DNS 名称服务器的记录

```
nslookup www.google.com
```

1. ftp：在本地主机和FTP服务器之间建立FTP连接。

```
ftp ftp_server
```

1. wget：获取网络资源

```
wget www.google.com -o google.html 
```

------

# 进程和系统控制命令

以下是在Linux系统中管理进程和控制系统的一些常用命令：

1. ps：显示当前进程的状态

```
ps aux
```

1. top：动态显示运行中的进程
2. kill：发送信号以终止进程

```
kill 1234
```

1. shutdown：关闭机器

```
 shutdown -h now
```

1. reboot：重启机器
2. logout：退出登录会话

------

# 文本操作命令

在编写或处理文本文件时，下列命令可以帮助你完成各种复杂任务：

1. echo：打印信息到终端。

```
echo "Hello, World!"
```

1. printf：格式化并打印信息。

```
printf "Name: %s\nAge: %d\n" "Alice" 20
```

1. sed：流编辑器，用于对文本文件进行特定的行处理和替换。

```
echo "Hello, World!" | sed 's/World/Shell/g'
```

1. awk：在文本文件中进行模式扫描和处理语言。

```
echo -e "name\tage\nAlice\t20\nBob\t22" | awk '{if ($2 >= 21) print $1}'
```

------

# 压缩与解压命令

以下命令主要用于管理和操作文件压缩及解压：

1. tar：创建、展开及管理tar包。

```
tar -cvf archive.tar folder
```

1. gzip：用于文件压缩或解压。

```
gzip file
```

1. gunzip：用于解压gzip压缩的文件。

```
gunzip file.gz
```

1. zip/unzip：创建和解压zip格式的压缩包。

```
zip -r archive.zip folder
unzip archive.zip
```

------

# 磁盘使用管理命令

管理和查看磁盘使用情况：

1. df：报告文件系统磁盘空间使用情况。

```
df -h
```

1. du：估计并报告文件及文件夹的磁盘使用情况。

```
du -sh folder
```

1. fdisk：对磁盘进行分区管理。

```
sudo fdisk -l
```

1. hdparm：查看或修改SATA/ATA磁盘参数。

```
sudo hdparm -i /dev/sda
```

------

# 包管理命令

在Debian，Ubuntu及其他基于Debian的系统中，可以使用以下命令进行软件包管理：

1. apt-get：APT包处理工具，用于处理包。

```
sudo apt-get install package
```

1. dpkg：Debian包管理器。

```
sudo dpkg -i package.deb
```

在RedHat, CentOS及其他基于RPM的系统中，可以使用以下命令进行软件包管理：

1. yum：高级软件包管理器，用于处理rpm包。

```
sudo yum install package
```

1. rpm：RPM包管理器。

```
sudo rpm -i package.rpm
```

------

# 进程管理命令

查看和管理正在运行的进程：

1. ps：报告进程当前状态。

```
ps aux
 USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND 
root 1 0.0 0.4 225848 7836 ? Ss Nov10 4:05 /lib/systemd/systemd --system --deserialize 39 
root 2 0.0 0.0 0 0 ? S Nov10 0:00 [kthreadd] 
root 4 0.0 0.0 0 0 ? I< Nov10 0:00 [kworker/0:0H]
```

1. top：动态显示当前耗费系统资源最多的进程。
2. htop：比top更友好的动态进程查看工具。

```
htop
```

1. kill：终止或者发送一个信号到指定进程。
2. pkill：条件地终止或者发送一个信号到指定进程。

```
pkill process_name
```

------

# 环境变量命令

查看或设置环境变量：

1. env：显示当前所有的环境变量。

```
输入：env
输出：
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    SHELL=/bin/bash
    PWD=/home/user
```

1. set：显示当前shell所有的环境变量及函数。

```
 输入：set
输出：展示所环境变量以及函数
```

1. export：设置或显示环境变量。

```
输入：
export VARName="Value"
echo $VARName
输出结果：
Value
```

------

# 系统信息发布相关命令

有时，你可能想要查看有关你的系统或硬件的信息。以下命令可以帮助你做到这一点：

1. uname：会打印操作系统的名称。

```
输入：
uname
输出：
Linux
```

1. hostname：打印系统的主机名。

```
输入：
hostname
输出：
myhostname
```

1. dmesg：打印或控制内核环形缓冲区。

```
输入：
dmesg | less
```

1. df：展示文件系统的磁盘空间使用情况。

```
 输入：df -h
输出：
    Filesystem      Size  Used Avail Use% Mounted on
    udev            962M     0  962M   0% /dev
    tmpfs           200M  4.3M  196M   3% /run
    /dev/sda1        30G  4.7G   24G  17% /
```

1. free：展示系统中未使用和已经使用的物理和swap内存。

```
输入：free -h
输出：
                  total        used        free      shared  buff/cache   available
    Mem:           3.8G        487M        1.9G        122M        1.4G        3.0G
    Swap:            0B          0B          0B
```

1. uptime：展示系统已经运行了多久，有多少用户正在登录，以及系统负载。

```
输入：uptime
输出：    16:14:30 up 43 min,  1 user,  load average: 0.34, 0.36, 0.40
```

1. last：查看系统的重启和关机记录。

```
输入：last reboot
```

1. w：展示哪些用户正在登录。

```
输入：w
输出：    16:17:51 up  1:42,  1 user,  load average: 0.45, 0.47, 0.38
    USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
    user     tty1                      14:36    1:42m  1.55s  0.06s w
```

1. who：展示哪些用户正在登录，和w命令相似但信息更少。

```
输入：who
输出：    user     tty1         2022-01-28 14:36
```

1. id：展示当前用户的UID、GID以及所在的组。

```
 输入：id
 输出：uid=1000(user) gid=1000(user) groups=1000(user),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```

------

# 系统控制命令

在一些特殊情况下，你可能需要进行一些系统控制操作。以下命令可以帮助你做到这一点：

1. halt：关机。

```
输入：sudo halt
```

1. reboot：重启系统。

```
输入：sudo reboot
```

1. shutdown：关机或者重启，和上述两个命令一样，但是提供更多的选项。

```
关闭系统：sudo shutdown -h now
重启系统：sudo shutdown -r now
```

1. passwd：更改用户密码。

```
更改密码：passwd
```

------

# 文本编辑器命令

Linux提供了多种命令行文本编辑器。以下这些可能是你需要知道的：

1. vi/vim：vi是一个文本编辑器，而vim是vi的改进版，提供了更多的功能。
2. nano：一个简单易用的命令行文本编辑器。
3. emac：一个强大的文本编辑器，也是一个定制化的计算环境。

# 其他常用命令

1. man：查看命令的帮助文档。
2. whatis：显示一个命令的简单描述。

```
输入：whatis ls
输出：ls (1)               - list directory contents
```

1. whereis：查找命令的二进制文件、源文件及帮助文档位置。

```
输入：whereis ls
输出：ls: /bin/ls /usr/share/man/man1/ls.1.gz
```

1. which：查找并显示给定命令的完整路径。

```
 输入：which ls
输出：/bin/ls
```

1. whoami：打印当前有效的用户名。

```
输入：whoami
输出：user
```

1. date：显示或设置系统日期和时间

```
输入：date
输出： Tue Dec 21 02:16:12 UTC 2021
```

1. cal：显示日历

```
输入：cal
输出：
       January 2022      
    Su Mo Tu We Th Fr Sa  
                      1  
    2  3  4  5  6  7  8  
    9 10 11 12 13 14 15  
    16 17 18 19 20 21 22  
    23 24 25 26 27 28 29  
    30 31                 
```

1. alias：创建命令别名
2. unalias：删除别名
3. history：显示命令历史
4. clear：清除屏幕或窗口内容
5. watch：用于实时查看当前命令打印信息

```
输入：watch -n 2 date
解释：watch`命令会每2秒运行一次`date`命令，并实时显示输出
```

大多数人学习Shell脚本的最大动力是提高效率。使用Shell脚本，你可以编写一个任务，然后让计算机去做，而你可以去忙其他的事情；你可以编写一个任务，让计算机重复执行，而不需要你每次在命令行手动输入；你可以更灵活地处理任务，比如管理用户，管理程序等。就这样，Shell脚本赋予你控制计算机的能力，在你的指尖下，一切尽在掌握。

在未来，实践未知，探索无限，最好的方式是动手试试看，愿这完整的100个命令清单能够成为你在Linux世界里的指南针！掌握Shell命令并利用它们来编写脚本能够极大地提升你的工作效率，无论是进行系统管理还是进行程序设计，这都是一种强大的工具。善用它，享受编程带给你的乐趣吧！



原文地址：https://mp.weixin.qq.com/s/5rnAe-qNZNlxRsEnfSlqMg
