原文地址：https://cloud.tencent.com/developer/article/1991217



# Linux系统入门系列之一



在生物信息分析中，通常要借助于大型服务器来处理各种数据，而Linux系统是比较通用的服务器操作系统，因此Linux系统的学习十分重要，熟识Linux命令与Shell脚本能帮助我们高效的完成生信分析任务。



在Linux系统中，我们一般通过命令行指令来执行各种任务。无论是个人PC版Linux系统，还是远程[服务器](https://cloud.tencent.com/product/cvm/?from_column=20065&from=20065)，我们一般通过图形界面X Window软件与计算机进行交互。个人PC版Linux系统自带图形界面，可以打开终端（terminal）输入指令；对于远程服务器，我们则需要模拟终端软件的帮助，最常用的为Xshell，其界面如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/0858aa64f8131277ce6e4f62a0bdc1aa.png)

执行“文件”→“新建”，在“主机”一栏输入服务器IP，选择相应端口，就可以建立一个自己电脑与远程服务器的连接，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/7a6b888ede2b4d086760847b2e15bfbe.png)

点击“确定”之后就会出现登录界面，输入管理员分配的账号密码即可。除了Xshell之外，Xftp是一个很好的服务器与电脑文件传输管理工具，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/c09387e5fd44fc9797743e2c69817a3c.png)

点击“新建”就可以创建一个与服务器的连接，在Xshell中有开启Xftp的快捷方式Ctrl+Alt+F，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/04e188c2a66ffddc75067949efb4125a.png)

**在Xshell的命令行输入相应的命令（多个命令以分号“;”隔开）以及参数并按回车键Enter执行，就可以使用服务器完成各种任务。**

1

**基础操作**

##### 1.1时间与日期

命令：date

显示日期，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/a76dec919a8b819361dcb8e6b87d98ed.png)

显示年月日：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/7261f038435223bcea09ca77dfe619df.png)

显示时分：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/638eb64722898f96d5948d8dd89996cb.png)

显示时分秒：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/5caa1d9362166804ae5a76dd9050a54f.png)

命令：cal

列出当前月份的日历，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/b2268de5cb2c1bc3839be52630b65c7b.png)

列出指定年月的日历：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/659250c33b8dca855103c226d554f9bb.png)

​     通过两个基础命令的练习，希望学习者可以初步感受什么是指令操作。

##### 1.2基础工具

命令：bc

基础运算工具，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/8573820532aebdac71ee9c4f43fe16cb.png)

其中%为求余数，quit为退出。bc默认输出整数，要输出小数，可以使用scale参数，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/8ae1938881e3018447ed5084a3c03504.png)

命令：nano

简单好用的书写记录软件，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/3583466ebdfceff67576d08bcf3ebeb1.png)

通过“Ctrl+□”快捷键来控制保存（Ctrl+O）、退出（Ctrl+X）等：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/4c1a4e1cfe66737916f91b65b36c4eaf.png)

命令：echo

echo会将输入的字符串送往标准输出。输出的字符串间以空白字符隔开，并在最后加上换行号。在屏幕显示字符串，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/8873458cd5c243e9e5a5c956683cb9a7.png)

在文件中写入字符串(>为覆盖原来的内容，>>为追加到文件后面)：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/e42ef85574b54eed055aa7559fcc443f.png)

显示目前所支持的语言：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/8c714a1d541e42d510d2884937b0df44.png)

修改语言为中文并输出中文字符：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/77d9986e36149a12ef86b46eece6cac8.png)

如果想要在双引号内使用反斜杠转义字符，需添加-e参数。

命令：man

查询Linux内置的帮助文件，了解命令的使用方法，例如输入“man date”回车，就可显示命令date的帮助文档，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/e6dd821f58b1e0b54baff5d46a576d15.png)

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f926765b6111cf99ceb9eb755171171a.png)

通过以上练习，希望学习者可以初步感受Linux中软件的调用方式。

##### 1.3.快捷热键

热键：Tab

命令补全，若没有记全一个命令，可以只输入已知部分，紧接着按两次Tab，系统便会显示所有相关的命令，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f29adb789d82602e508e89dac94488e9.png)

文件补全：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/7505c5e1dc6c25671edb12c6a90182df.png)

对于非隐藏文件，输入部分文件名紧接着按一次tab，就会自动输入后续部分，如ls-al ~/prac[Tab]tice.[Tab]txt：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/e497e14f66caa571bf57b60ab57b4213.png)

热键：Ctrl+C

停止一个错误的命令或者退出一个输错的命令，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/8280eca20b0daf632c2717fb2174d1df.png)

热键：\+Enter

一般情况下Enter表示的是命令执行，反斜杠转义为换行，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/0f081e3a96691e91d8c308b6db6a9834.png)

2

**文件管理**

##### 2.1文件查看

命令：ls

添加参数-al列出当前路径下所有文件，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/9eaf6c705d8764b8a8388ffe1261030d.png)

添加参数-l列出非隐藏文件：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/ddd5f71cafa31032f0acdeac10f665d6.png)

或者简写为ll：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/49f379f13f65b525213119f0101d7701.png)

其中“-”后面为参数选项[Option]，对ls（或ll）命令常用选项如下：

-a：全部的文件，连同隐藏文件(开头为“.”的文件)一起列出来；

-d：仅列出目录本身，而不是列出目录内的文件数据；

-l：长数据串列出，包含文件的属性与权限等等数据；

-R：若列出对象为路径且目录下有文件，则将所有文件依序列出；

-t：按照最后修改时间顺序列出文件，由旧到新；

-h：文件大小显示单位（K、M、G等）。

命令：tree

将某路径下文件夹及文件以树状图展示，当前路径下使用示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/5eda5b20305a552b3254a8a2ee0df4a8.png)

命令tree的参数选项如下：

-d：只显示目录；

-D：列出文件或目录的更改时间；

-f：在每个文件或目录之前，显示完整的相对路径名称；

-L：后接数字，显示到第几级子目录；

-s：列出文件或目录大小；

-t：用文件和目录的更改时间排序。

命令：find

查找只知道部分名字的某文件及其路径，全盘搜索示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/33a9d92f4be15df8d144ef5ea32775e1.png)

只在当前目录下搜索：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/891363e2789a8700f8b6d72f50404964.png)

此命令常用到通配符来进行模糊查找，常用通配符如下：

| 符号 | 意义                                                         |
| :--- | :----------------------------------------------------------- |
| *    | 表示0个到无穷多个任意字符。例如a*可以表示a，ab，abc，...     |
| ？   | 表示1个任意字符。例如a？可以表示ab，ac，但是不能表示a或者abc |
| []   | 表示一个在中括号中的字符。例如[abc]表示a，b，c中的一个       |
| [-]  | 表示在编码顺序内的所有字符。例如[a-z]表示字母a到z；[0-9]表示数字0到9 |
| [^]  | 反向选择，表示在中括号中以外的一个字符。例如[^abc]表示字母a，b，c以外的其他字符 |

命令：locate

使用locate搜索linux系统中的文件，它比find命令速度快很多，因为它查询的是[数据库](https://cloud.tencent.com/product/tencentdb-catalog?from_column=20065&from=20065)(/var/lib/locatedb)，数据库包含本地所有的文件信息。使用locate加文件名便可在根目录下搜索相应文件，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/0190388648330bdf4dc746ab81daffdb.png)

 命令：cat

在屏幕上显示文件内容，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/48ada3d5e5c50d7103a58074ce43a3a8.png)

将两个文本文件整合为一个文本文件（行累加），示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/4481831340b24a8cbcfd52ded7b4197b.png)

添加参数-A查看文本文档的格式（显示tab空格等所有特殊键）：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/98fb51804b2ef359108ff8c0170123cc.png)

其中^I即为tab键。具体参数选项如下：

-A：相当于-vET的整合选项，可列出一些特殊字符而不是空格显示；

-b：列出行号，仅针对非空白行做行号显示，空白行不标行号；

-n：列印出行号，连同空白行也会有行号，与-b的选项不同；

-E：将结尾的断行字节$显示出来；

-T：将[tab]按键以^I显示出来；

-v：列出一些看不出来的特殊字符。

命令：nl

列出文本内容并打印行号，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/ccb8d38978f07dcff693ec13bcfd9da3.png)

命令：head

显示文件前面部分，例如显示前三行：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/ce3eae3ab89bd26801254a0ba5cacebc.png)

此外还有命令tail，从尾行提取特定行数，这两个命令搭配管道命令可选取文件特定的行数范围进行显示。

命令：less

对于大的文本文档cat查看比较困难，而less可以进行分页查看，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/35347088f547733d10e8f08834c9298f.png)

按键F向下翻页，B向上翻页，空格向下翻页，Enter滚动一行，Q退出less命令：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/4f36ce7ba180f7bc659310335a3c3102.png)

若要横向超出屏幕部分不强制换行展示，可添加-S参数：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/49adb75e8ba7ee33d94e306a8a583584.png)

若要查找内容使用/+内容（或?+内容向上搜索）然后回车即可，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/45fd6aad11be86cc0edc3d0441042f21.png)

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/3e3a2e5864fc5cb6a120d306cb0556b7.png)

此查找支持正则表达式。

 2.2文件路径

命令：ln

在当前路径下创建某文件的超链接，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/782c96102dbd5babc10acf0c81925667.png)

命令：cd

去往一个路径（路径切换），其中cd空格或者cd~表示返回用户主目录，cd ..表示返回上一级目录（返回上两级则是cd ../..表示返回上两级）示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/c028694aa8848da0ecc809ce0c9964eb.png)

命令：mkdir

在当前路径下新建路径（文件夹），示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f11ae2c3794e8362352b53699d009e18.png)

此命令具有以下选项：

-m：配置文件的权限；

-p：创建递归目录。

命令：rmdir

删除当前路径下的路径（文件夹），示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/af6c1423d42a38133ac312f9d5b7eefb.png)

命令：rm

删除当前路径下文件或路径（多个文件空格隔开），示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/6c5e97548f3f6d966a7da0df68e38ae2.png)

添加参数-r可删除路径以及所含有的文件：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/c6a180a790b39dfda570cadfd44e2cff.png)

命令：cp

复制文件或目录到一个新的目录，示例如下

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f09db85214d5e310a74f3dcadf7d394f.png)

复制多个文件，空格隔开，只要最后一个是目的路径即可：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/37db3d18471b1a0967ee08b75c0d4d98.png)

若是复制到当前文件夹，目的路径为“.”：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f40f807d7631613f389f65e7b4a46fa0.png)

将某路径下所有文件复制到一个新的文件夹：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f6ea3f5880dfcee4f55c2d26d947cf2d.png)

此命令具有以下常用选项：

-a：相当于-pdr；

-d：若source为链接文件(linkfile)，则复制链接属性而非文件本身；

-f：为强制(force)的意思，若目标文件已经存在且无法开启，则移除后再尝试一次；

-i：若目标文件(destination)已经存在时，在覆盖时会先进行询问(常用)；

-p：连同文件的属性一起复制过去，而非使用默认属性；

-r：递归持续复制，用于目录的复制行为。

命令：mv

移动当前路径下文件或目录到另一个文件夹，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/03ab57ca71cabc84ebebf43de3165a0c.png)

对文件重命名：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/968999174fda52a9f323e46b27feadb7.png)

此命令具有以下常用选项：

-f：force强制的意思，如果目标文件已经存在，不会询问而直接覆盖；

i：若目标文件(destination) 已经存在时，询问是否覆盖；

-u：若目标文件已经存在，且source比较新（即最后修改时间比较晚），才会覆盖（修改时间比较早的旧文件）。

命令：touch

创建新的文件（不是文件夹），示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/46753e1914ba3b490de5081f9e207fd4.png)

命令：du

查看文件或文件夹磁盘占用空间大小，如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/7b7234e0a360ae9351a3d98b60e48de5.png)

其参数选项如下所示：

-a：列出所有的文件与目录大小，因为默认仅列出路径

-h：以人们较易读的容量格式(G/M)显示；

-s：列出总量，而不列出每个各别的目录占用空间；

-S：不包括子目录下的总计，与-s有点差别。

-k：以KBytes列出容量显示；

-m：以MBytes列出容量显示。

命令：rz

从电脑传输文件到服务器，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/544a1f2ac27fbb0107238a00606f5754.png)

命令：sz

从服务器传输文件到电脑，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/5ff0b7d8a4586596f5fa3e73aacae775.png)

以上两个命令需要电脑预先安装Xftp。

##### 2.3文件压缩

命令：gzip, zcat

使用gzip压缩、读取、解压文件，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/c44fd07456fe5953719a77b3a66ce29c.png)

命令：bzip2, bzcat, zip, unzip

使用bzip2压缩，用法与gzip类似。

命令：tar

打包并压缩文件或目录，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/79c2fc7ef67dd801ea4825784589be17.png)

解压打包文件：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/f7b5b279854cf2cf4334a247ccc93210.png)

命令：file

在Linux系统中有时候文件名后缀不能完全显示文件格式，使用file命令可查看文件格式，是否被压缩以及使用什么软件压缩，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/005e953d1718d4879b3b72e3ba3a7c9e.png)

可以看出这时候文件虽然没有“.gz”的后缀，但是是gzip压缩文件，这时候不能直接解压，需要添加后缀并解压：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/468e43eb46b76a7d3d45d326a6540c2c.png)

##### 2.4文件下载

命令：wget

wget是linux最常用的下载命令，可以从网络上自动下载文件，它支持HTTP，HTTPS和FTP协议，可以使用HTTP代理。所谓的自动下载是指，wget可以在用户退出系统的之后在后台执行。其使用方法如下：

wget[Options] 要下载文件的网址（包含文件名）

其中Options：

-A：指定要下载文件的后缀名，多个后缀名之间使用逗号进行分隔

-c：断点续传，继续执行上次的下载命令

-b：启动后转入后台执行

-i：从指定文件获取要下载的URL地址，文件中每行指定一个网址

-O：指定下载后的文件路径及保存为的文件名

具体下载方法如下所示：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/ca94dd580c7e6a20fba8bb4b08c91242.png)

其中文件名支持使用通配符而进行批量下载。

##### 2.5文件权限

在查看文件的时候，最前面的信息即为文件权限，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/6641148babf4d35f3f6c7bfef4d3f94b.png)

一共有10位，第一位d代表路径（文件夹），-代表文件，之后每三位一组分别为文件所有者、用户组、其他人的权限，r为可读，w为可写，x为可执行，-为无权限。

命令：chmod

更改文件或路径的权限，示例如下：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/e6e588a2efda3f8559fd74ff89fa8e69.png)

其中r:4,w2,x1。更改目录及其下属文件的权限：

![img](https://ask.qcloudimg.com/http-save/yehe-9721155/167c834a9d4ba77cb79b776621cadf6e.png)

