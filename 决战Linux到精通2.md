## Linux管道命令
Linux的管道命令是’|’，通过它可以对数据进行连续处理，其示意图如下：

![image](https://github.com/user-attachments/assets/51bd7cae-2b76-4969-a323-29b34dee73c6)

注意：

1）管道命令仅处理标准输出，对于标准错误输出，将忽略

2）管道命令右边命令，必须能够接收标准输入流命令才行，否则传递过程中数据会抛弃。

常用来作为接收数据管道命令有： less,more,head,tail，而ls, cp, mv就不行。

### wc - 统计字数
可以计算文件的Byte数、字数、或是列数，若不指定文件名称、或是所给予的文件名为"-"，则wc指令会从标准输入设备读取数据。

```txt
wc [-lwm] [filename]
-l: 统计行数
-w：统计英文单词
-m：统计字符数
python@xxx:~$ wc -l /etc/passwd
49 /etc/passwd
python@xxx:~$ wc -w /etc/passwd
81 /etc/passwd
python@xxx:~$ wc -m /etc/passwd
2696 /etc/passwd
```

在默认的情况下，wc将计算指定文件的行数、字数，以及字节数。使用的命令为：

```txt
$ wc testfile           # testfile文件的统计信息  
3 92 598 testfile       # testfile文件的行数为3、单词数92、字节数598 
```

其中，3 个数字分别表示testfile文件的行数、单词数，以及该文件的字节数。

如果想同时统计多个文件的信息，例如同时统计testfile、testfile_1、testfile_2，可使用如下命令：

```txt
$ wc testfile testfile_1 testfile_2  #统计三个文件的信息  
3 92 598 testfile                    #第一个文件行数为3、单词数92、字节数598  
9 18 78 testfile_1                   #第二个文件的行数为9、单词数18、字节数78  
3 6 32 testfile_2                    #第三个文件的行数为3、单词数6、字节数32  
15 116 708 总用量                    #三个文件总共的行数为15、单词数116、字节数708 
```

### cut - 列选取命令

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

### grep - 行选取命令
grep一般格式为：

```txt
grep [-cinv] '查找的字符串' filename
```

在grep命令中输入字符串参数时，最好引号或双引号括起来。例如：grep 'a' 1.txt。

常用选项说明：

![image](https://github.com/user-attachments/assets/abf0c37d-4e57-4caa-8785-51c9f7415ccb)

grep搜索内容串可以是正则表达式，常用正则表达式：

![image](https://github.com/user-attachments/assets/9e2b9391-f81d-4d86-bb73-fe1d6c3e3ae2)


实例：

显示所有以“h”结尾的行

grep h$

匹配所有以“a”开头且以“e”结尾的，中间包含2个字符的单词

grep ‘<a…e>’

显示所有包含一个”y”或”h”字符的行

grep [yh]

显示不包含字母a~k 且后紧跟“pple”的单词

grep [^a-k]pple

从系统词典中选择所有以“c”开头且以“o”结尾的单词

grep '\<c.*o\>'

找出一个文件中或者输出中找到包含*的行

grep '\*'

显示所有包含每个字符串至少有20个连续字母的单词的行

grep [a-Z]\{20,\}

### sort - 排序
语法：

![image](https://github.com/user-attachments/assets/04d8e200-8df8-4306-be20-4f8b851b4de1)


参数说明：

- -f ：忽略大小写的差异，例如 A 与 a 视为编码相同；
- -b ：忽略最前面的空格符部分；
- -M ：以月份的名字来排序，例如 JAN, DEC 等等的排序方法；
- -n ：使用『纯数字』进行排序(默认是以文字型态来排序的)；
- -r ：反向排序；
- -u ：就是 uniq ，相同的数据中，仅出现一行代表；
- -t ：分隔符，默认是用 [tab] 键来分隔；
- -k ：以哪个区间 (field) 来进行排序

默认是以第一个字符升序排序:

![image](https://github.com/user-attachments/assets/fe5bd912-de6e-4931-8832-7037d3550947)


以第3列排序：

![image](https://github.com/user-attachments/assets/02514c17-858a-43aa-9ddd-0e1f445e57f6)


使用数字排序：

![image](https://github.com/user-attachments/assets/e478c5d0-eed8-42c3-9e14-9f35a019d552)

倒序排序：

![image](https://github.com/user-attachments/assets/aeb71805-84ea-4deb-bced-e409709af89c)


先以第六个域的第2个字符到第4个字符进行正向排序，再基于第一个域进行反向排序：

![image](https://github.com/user-attachments/assets/d024bf0e-17be-41a9-a9b3-491ba4657de0)

查看/etc/passwd有多少个shell:

方法对/etc/passwd的第七个域排序并去重，然后统计行数：

![image](https://github.com/user-attachments/assets/3495ec35-ae03-4022-bc5c-a8fafa55900e)

### uniq - 去重
![image](https://github.com/user-attachments/assets/f41f354a-2e56-4c55-8540-8b7c42cfa36a)

该命令用于排完序之后，对排序结果进行去重

![image](https://github.com/user-attachments/assets/5c8f5982-7f18-4484-b19e-d4e0303c067c)


排序文件，默认是去重：

![image](https://github.com/user-attachments/assets/8ef749e5-3271-4bd1-a3d2-25459e5f4446)

排序之后删除了重复行，同时在行首位置输出该行重复的次数：

![image](https://github.com/user-attachments/assets/9de3e84a-7989-4754-9bef-a2b3d95a022c)


仅显示存在重复的行，并在行首显示该行重复的次数：

![image](https://github.com/user-attachments/assets/98e25f62-724d-4cae-9ca6-0c8723a0b9b2)


仅显示不重复的行：

![image](https://github.com/user-attachments/assets/701c22b4-4268-41f6-913f-6f671bd5f290)


### tee - 同时输出多个文件
从标准输入设备读取数据，将其内容输出到标准输出设备，同时保存成文件。

一般情况下用重定向实现，需要同时输出多个文件时可以使用该命令。

参数：

- -a或–append 　附加到既有文件的后面，而非覆盖它．

将输出同时保存到多个文件中，同时将输出内容显示到控制台：

![image](https://github.com/user-attachments/assets/cf177a05-a23d-41fc-acc1-a7c9aa6cf123)

### tr - 替换指定的字符
不指定参数时，即表示替换指定的字符为另一个字符，支持指定的字符集合。

参数说明：

- -d, --delete：删除指定的字符
- -s, --squeeze-repeats：缩减连续重复的字符成指定的单个字符

字符集合的范围：

- \NNN 八进制值的字符 NNN (1 to 3 为八进制值的字符)
- \ 反斜杠
- \a Ctrl-G 铃声
- \b Ctrl-H 退格符
- \f Ctrl-L 走行换页
- \n Ctrl-J 新行
- \r Ctrl-M 回车
- \t Ctrl-I tab键
- \v Ctrl-X 水平制表符
- CHAR1-CHAR2 ：字符范围从 CHAR1 到 CHAR2 的指定，范围的指定以 ASCII 码的次序为基础，只能由小到大，不能由大到小。
- [CHAR*] ：这是 SET2 专用的设定，功能是重复指定的字符到与 SET1 相同长度为止
- [CHAR*REPEAT] ：这也是 SET2 专用的设定，功能是重复指定的字符到设定的 REPEAT 次数为止(REPEAT 的数字采 8 进位制计算，以 0 为开始)
- [:alnum:] ：所有字母字符与数字
- [:alpha:] ：所有字母字符
- [:blank:] ：所有水平空格
- [:cntrl:] ：所有控制字符
- [:digit:] ：所有数字
- [:graph:] ：所有可打印的字符(不包含空格符)
- [:lower:] ：所有小写字母
- [:print:] ：所有可打印的字符(包含空格符)
- [:punct:] ：所有标点字符
- [:space:] ：所有水平与垂直空格符
- [:upper:] ：所有大写字母
- [:xdigit:] ：所有 16 进位制的数字
- [=CHAR=] ：所有符合指定的字符(等号里的 CHAR，代表你可自订的字符)

将文件testfile中的小写字母全部转换成大写字母：

![image](https://github.com/user-attachments/assets/c3050f00-fa98-48e4-9dfd-6ffbbd46d329)

缩减连续重复的字符成指定的单个字符：

![image](https://github.com/user-attachments/assets/fd9b4cce-f711-4529-9669-f9558a8d6e72)

删除指定的字符：

![image](https://github.com/user-attachments/assets/4df589cd-5a92-44d6-a86b-73281ae2cf57)


### join - 文件按行连接
将两个文件中指定栏位相同的行连接起来。即按照两个文件中共同拥有的某一列，将对应的行拼接成一行。

注意：在使用join之前所处理的文件要事先经过排序。

![image](https://github.com/user-attachments/assets/5f8a732a-c6d4-4d8e-83fc-afc51db65ede)


使用join命令，将两个文件连接：

![image](https://github.com/user-attachments/assets/4ad45242-7f90-455e-ad3e-a7f2a0223607)


两个文件互换，输出结果的变化：

![image](https://github.com/user-attachments/assets/69e0d797-e21f-4aa3-a525-13f08837f727)


参数：

- -a<1或2> 除了显示原来的输出内容之外，还显示指令文件中没有相同栏位的行。
- -e<字符串> 若[文件1]与[文件2]中找不到指定的栏位，则在输出中填入选项中的字符串。
- -i或–igore-case 比较栏位内容时，忽略大小写的差异。
- -o<格式> 按照指定的格式来显示结果。
- -t<字符> 使用栏位的分隔字符。
- -v<1或2> 跟-a相同，但是只显示文件中没有相同栏位的行。
- -1<栏位> 连接[文件1]指定的栏位。
- -2<栏位> 连接[文件2]指定的栏位。

### paste-将多个文件对应行链接在一起
paste 指令会把每个文件以列对列的方式，一列列地加以合并。

语法：

![image](https://github.com/user-attachments/assets/e5ff5fa6-da42-493c-b66e-1ff642a171f0)


参数：

- -d<间隔字符>或–delimiters=<间隔字符> 　用指定的间隔字符取代跳格字符。
- -s或–serial 　串列进行而非平行处理。
- [文件…] 指定操作的文件路径

使用paste指令将文件"file"、“testfile”、"testfile1"进行合并，输入如下命令：

![image](https://github.com/user-attachments/assets/5f935553-4778-452c-8562-e6790151a02d)

参数"-s"可以将一个文件中的多行数据合并为一行进行显示：

![image](https://github.com/user-attachments/assets/1eb88b15-4158-45b1-b814-6732d0b64e1c)

如果将文件位置改为-，表示接收标准输入：

![image](https://github.com/user-attachments/assets/ad9806ba-a264-4dff-87cc-dbc5da410b4a)


### split - 文件切割
split命令用于将一个文件分割成数个。

该指令将大文件分割成较小的文件，在默认情况下将按照每1000行切割成一个小文件。

语法：

![image](https://github.com/user-attachments/assets/f7bcff52-e0e3-46b6-acf7-272608562095)


参数说明：

- -<行数> : 指定每多少行切成一个小文件
- -b<字节> : 指定每多少字节切成一个小文件
- -C<字节> : 与参数"-b"相似，但是在切 割时将尽量维持每行的完整性
- [输出文件名] : 设置切割后文件的前置文件名， split会自动在前置文件名后再加上编号

使用指令"split"将文件"README"每6行切割成一个文件，输入如下命令：

![image](https://github.com/user-attachments/assets/1aba281d-8500-434d-9e6f-fd2e3243b543)

以上命令执行后，指令"split"会将原来的大文件"README"切割成多个以"x"开头的小文件。而在这些小文件中，每个文件都只有6行内容。

以大小切割：

![image](https://github.com/user-attachments/assets/9be08faf-c4c5-4ed2-9296-5dd75691eab3)


### xargs - 参数代换
不是所有的命令都支持管道，如ls，对于不支持管道的命令，可以通过xargs让其有管道命令的效果，如下所示：

![image](https://github.com/user-attachments/assets/06942bde-5c06-4c53-955b-1678582c1f39)


如果没有xargs，ls -l的结果将不是前面find的标准输出，因为ls不支持管道命令。

xargs 用作替换工具，读取输入数据重新格式化后输出。

定义一个测试文件，内有多行文本数据：

![image](https://github.com/user-attachments/assets/c895f920-60b9-40be-9fba-71f615fe2661)


多行输入单行输出：

![image](https://github.com/user-attachments/assets/a4258475-6dd3-42c1-b642-c299a6ff2649)


-n 选项多行输出：

![image](https://github.com/user-attachments/assets/7a5d2462-8630-4d56-8001-8a2112e4e6ae)


-d 选项可以自定义一个定界符：

![image](https://github.com/user-attachments/assets/4975c79c-7c4c-4a7c-a5f1-6a5e08682ba3)


结合 -n 选项使用：

![image](https://github.com/user-attachments/assets/4163a0c5-996f-4c5c-9867-24ba35ecd154)


读取 stdin，将格式化后的参数传递给命令:

![image](https://github.com/user-attachments/assets/23aed75e-6fc2-401a-a822-c0309495a1e5)


选项-I指定一个替换字符串 {}，这个字符串在 xargs 扩展时会被替换掉。

复制所有图片文件到 /data/images 目录下：

![image](https://github.com/user-attachments/assets/e7693289-d974-4feb-bd2b-5835e574c29b)


选项-n 后面加次数，表示命令在执行的时候一次用的argument的个数，默认是用所有的。

xargs 结合 find 使用

用 rm 删除太多的文件时候，可能得到一个错误信息：/bin/rm Argument list too long. 用 xargs 去避免这个问题：

![image](https://github.com/user-attachments/assets/95ca4374-9341-4c03-8a2a-f0f4698ee887)


xargs -0 将 \0 作为定界符。

统计一个源代码目录中所有 php 文件的行数：

![image](https://github.com/user-attachments/assets/86f89678-daf9-434a-8642-f13ded0464ed)


查找所有的 jpg 文件，并且压缩它们：

![image](https://github.com/user-attachments/assets/aaa27854-5eca-4266-bbac-e2eb79ca6138)

批量下载：

![image](https://github.com/user-attachments/assets/4d5ef3dd-6ef6-4df4-a52a-1e72a8c01967)

wget的-c选项表示断点续传。



# Linux命令练习
## 常用命令
![image](https://github.com/user-attachments/assets/1dde65f0-2880-45f8-97d3-b10c3329beb7)


## 系统命令
![image](https://github.com/user-attachments/assets/3f334ef2-8a22-48b4-adae-e2df1244c086)

## 用户和组
![image](https://github.com/user-attachments/assets/43903c3d-5606-403c-8978-386a40cb8588)


## 权限
![image](https://github.com/user-attachments/assets/d5d6591d-94d2-408c-ad91-2ca4fbf300ac)


## 帮助文档
![image](https://github.com/user-attachments/assets/b08ded26-d795-4d15-9d53-61f82d225490)


文件相关命令

![image](https://github.com/user-attachments/assets/2f863d1c-3264-4ee2-9519-5a5b3e5c086d)


## VIM
![image](https://github.com/user-attachments/assets/e9ea800e-869d-48b8-8136-a9d09a1b5675)

## 查找
![image](https://github.com/user-attachments/assets/612d3054-ef2e-4342-b7a5-21ec5332cc6b)

## 打包与压缩
![image](https://github.com/user-attachments/assets/89616999-7e1a-465d-843f-d82732800f78)


## 正则表达式
![image](https://github.com/user-attachments/assets/5c4c742e-a35b-4faf-ab02-651340bff624)

## 输入输出重定向
![image](https://github.com/user-attachments/assets/fc37f2f3-6dce-4fac-b714-154a41772190)


## 进程控制
![image](https://github.com/user-attachments/assets/4cf0161b-e37b-4cf6-b71f-3e4fc0275093)


## 其他命令
### 远程文件复制：scp
scp 命令用于 Linux 之间复制文件和目录，scp是 secure copy 的缩写是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。

scp 是加密的，rcp 是不加密的，scp 是 rcp 的加强版。

使用scp命令要确保使用的用户具有可读取远程服务器相应文件的权限，否则scp命令是无法起作用的。

从本地复制到远程命令格式：

![image](https://github.com/user-attachments/assets/3d3a477a-1e2d-4d50-9839-48bb67e18e45)


实例：

![image](https://github.com/user-attachments/assets/89851cd2-f7ec-4517-922f-3b16b128d4f6)


从远程复制到本地：

![image](https://github.com/user-attachments/assets/b5604b22-fa92-4630-8905-fa787cb93f0d)


-P 参数来设置命令的端口号：

![image](https://github.com/user-attachments/assets/6ec43f54-77a6-4545-a01c-0e771c502a4c)


## locate查找
locate命令会去保存文档和目录名称的数据库内，查找文件或目录。

一般情况我们只需要输入locate your_file_name 即可查找指定文件。

参数：

- -d或–database= 配置locate指令使用的数据库。locate指令预设的数据库位于/var/lib/mlocate目录里，文档名为mlocate.db。

查找passwd文件，输入以下命令：

![image](https://github.com/user-attachments/assets/2f04d857-1918-4453-bd96-571f97bf0dae)


locate与find的区别: find 是去硬盘找，locate 只在/var/lib/slocate资料库中找。

locate的速度比find快，它并不是真的查找，而是查数据库，一般文件数据库在/var/lib/mlocate/mlocate.db中，所以locate的查找并不是实时的，而是以数据库的更新为准，一般是系统自己维护，也可以手工升级数据库 ，命令为：

![image](https://github.com/user-attachments/assets/b003b6df-a38f-413b-a9bd-9d55763c7ccb)


## which命令
which查找$PATH中设置命令及安装文件目录所在位置

![image](https://github.com/user-attachments/assets/ea09276c-ab2e-426c-b6f0-2c8de1301f01)


## echo
常见用法：

![image](https://github.com/user-attachments/assets/b4c841dc-369b-46fa-a761-227f239d3482)


## 设置或显示环境变量：export
在 shell 中执行程序时，shell 会提供一组环境变量。export 可新增，修改或删除环境变量，供后续执行的程序使用。export 的效力仅限于该次登陆操作。

![image](https://github.com/user-attachments/assets/cc1c87c8-0c40-4145-aac1-71ed61823f67)


参数说明：

- -f 　代表[变量名称]中为函数名称。
- -n 　删除指定的变量。变量实际上并未删除，只是不会输出到后续指令的执行环境中。
- -p 　列出所有的shell赋予程序的环境变量。

![image](https://github.com/user-attachments/assets/e993e325-ad1f-40ed-90d9-ea2746ee10ad)


## 修改主机名&ip地址
显示主机名：hostname

临时修改：hostname xxx

**永久修改**

对于Ubuntu 系统

![image](https://github.com/user-attachments/assets/bacd6ea7-6353-431f-ac8f-e7dec04b9f5d)


对于centos系统

![image](https://github.com/user-attachments/assets/e9c31d90-2f64-4b4a-bd7b-3f8e51318063)

在此配置文件中添加一条HOSTNAME=node1

针对centos7系统，可以使用如下命令

![image](https://github.com/user-attachments/assets/4bd680d7-72f9-46d5-b4b5-fbe46d1426b6)


一般需要重开shell甚至重启操作系统才能生效。

**修改IP地址**

ifconfig eth0 192.168.12.22(重启后无效)

![image](https://github.com/user-attachments/assets/7bf82c3d-7a62-4c42-8838-25fb04cccf53)


## mount挂载
mount 挂载外部存储设备到文件系统中

![image](https://github.com/user-attachments/assets/b9710f59-aebc-4b08-adae-7a6749dd43ba)

将设备/dev/cdrom挂载到 挂载点 ： /mnt/cdrom中

![image](https://github.com/user-attachments/assets/6df98863-8ee6-43a3-a140-0eff01600489)


## ssh免密登陆
假如 A 要登陆 B

在A上操作：

首先生成密钥对

![image](https://github.com/user-attachments/assets/fe1e582e-eee4-40ed-b1bc-78ecfcafa34c)


再将A自己的公钥拷贝并追加到B的授权列表文件authorized_keys中

![image](https://github.com/user-attachments/assets/5099204e-6eb8-4ecc-8c56-84470a6408b7)

## 批量添加用户
### 与用户账号有关的系统文件
完成用户管理的工作本质都是对有关的系统文件进行修改，这些系统文件包括/etc/passwd, /etc/shadow, /etc/group等。

**/etc/passwd记录用户的基本属性**

它的内容类似下面的例子：

![image](https://github.com/user-attachments/assets/12b60bfa-3ea8-401a-a0b0-5a66329e23a9)

/etc/passwd中一行记录对应着一个用户，每行记录又被冒号(:)分隔为7个字段，其格式和具体含义如下：

![image](https://github.com/user-attachments/assets/7ed8cdeb-ef75-432e-969a-9d0c678a7671)


**用户名：**

通常长度不超过8个字符，由大小写字母和/或数字组成，不能有冒号(😃。登录名中不能有冒号(😃，因为冒号在这里是分隔符。

为了兼容起见，登录名中最好不要包含点字符(.)，并且不使用连字符(-)和加号(+)打头。

**口令：**

本身存放用户口令的加密串，但现在许多Linux 系统都使用了shadow技术，把真正的加密后的用户口令字存放到/etc/shadow文件中，而/etc/passwd文件的口令字段中只存放一个特殊的字符，例如“x”或者“*”。

**用户标识号：**

是一个整数，系统内部用它来标识用户。一般情况下它与用户名是一一对应的，如果几个用户名对应的用户标识号是一样的，系统内部将把它们视为同一个用户，但是它们可以有不同的口令、不同的主目录以及不同的登录Shell等。

通常用户标识号的取值范围是0～65 535。0是超级用户root的标识号，1～99由系统保留，作为管理账号，普通用户的标识号从100开始。

**组标识号：**

记录用户所属的用户组，对应着/etc/group文件中的一条记录。

**注释性描述：**

一段任意编写的注释，创建账户时可以通过useradd -c 用户名的-c参数指定。

**主目录：**

用户的起始工作目录，用户在登录到系统之后所处的目录。

**登录Shell：**

用户登录后，要启动一个进程，负责将用户的操作传给内核，这个进程是用户登录到系统后运行的命令解释器或某个特定的程序，即Shell。

Shell是用户与Linux系统之间的接口。Linux的Shell有许多种，每种都有不同的特点。常用的有sh(Bourne Shell), csh(C Shell), ksh(Korn Shell), tcsh(TENEX/TOPS-20 type C Shell), bash(Bourne Again Shell)等。

可以通过usermod的-s参数为用户指定某个Shell。如果useradd不通过-s参数指定shell，那么系统使用bash为默认的登录Shell，即这个字段的值为/bin/bash。

为用户的登录指定特定的Shell可以限制用户只能运行指定的应用程序，在该应用程序运行结束后，用户就自动退出了系统。不过大部分Linux系统要求只有在系统中登记过的shell才能出现在这个字段中。

**伪用户（pseudo users）**

这些用户的登陆shell为/usr/sbin/nologin，即不能登录。它们的存在主要是方便系统管理，满足相应的系统进程对文件属主的要求。

常见的伪用户如下所示：

![image](https://github.com/user-attachments/assets/5673c290-d3f9-430c-97d4-30cf2b0b0029)


还有许多标准的伪用户，例如：audit, cron, mail, usenet等，它们也都各自为相关的进程和文件所需要。

**/etc/shadow**

对安全性要求较高的Linux系统都把/etc/passwd文件中的口令字段保存在/etc/shadow文件中，超级用户才拥有该文件读权限。

/etc/shadow中的记录行与/etc/passwd中的一一对应，它由pwconv命令根据/etc/passwd中的数据自动产生

字段是：

![image](https://github.com/user-attachments/assets/b3aff99d-a403-4f3f-8247-86269a80d3b0)


1."登录名"是与/etc/passwd文件中的登录名相一致的用户账号

2."口令"字段存放的是加密后的用户口令字，长度为13个字符。如果为空，则对应用户没有口令，登录时不需要口令；如果含有不属于集合 { ./0-9A-Za-z }中的字符，则对应的用户不能登录。

3."最后一次修改时间"表示的是从某个时刻起，到用户最后一次修改口令时的天数。大部分linux系统的时间起点是1970年1月1日。

4."最小时间间隔"指的是两次修改口令之间所需的最小天数。

5."最大时间间隔"指的是口令保持有效的最大天数。

6."警告时间"字段表示的是从系统开始警告用户到用户密码正式失效之间的天数。

7."不活动时间"表示的是用户没有登录活动但账号仍能保持有效的最大天数。

8."失效时间"字段给出的是一个绝对的天数，如果使用了这个字段，那么就给出相应账号的生存期。期满后，该账号就不再是一个合法的账号，也就不能再用来登录了。

下面是/etc/shadow的一个例子：

![image](https://github.com/user-attachments/assets/cf44a272-aa80-4112-836c-fccd5957f3c7)


**/etc/group记录用户组信息**

每个用户都属于某个用户组；一个组中可以有多个用户，一个用户也可以属于不同的组。

当一个用户同时是多个组中的成员时，在/etc/passwd文件中记录的是用户所属的主组，也就是登录时所属的默认组，而其他组称为附加组。

用户要访问属于附加组的文件时，必须首先使用newgrp命令使自己成为所要访问的组中的成员。

用户组的所有信息都存放在/etc/group文件中，字段有：

![image](https://github.com/user-attachments/assets/35b73c0a-911e-482c-8f1d-fc393e6873f9)


1."组名"是用户组的名称，由字母或数字构成。与/etc/passwd中的登录名一样，组名不应重复。

2."口令"字段存放的是用户组加密后的口令字。一般Linux 系统的用户组都没有口令，即这个字段一般为空，或者是*。

3."组标识号"与用户标识号类似，也是一个整数，被系统内部用来标识组。

4."组内用户列表"是属于这个组的所有用户的列表，不同用户之间用逗号(,)分隔。这个用户组可能是用户的主组，也可能是附加组。

/etc/group文件的一个例子如下：

![image](https://github.com/user-attachments/assets/c4e8eccb-d8f4-4b8e-8fd5-e9ac899cfeed)

## 实操
**先编辑一个文本用户文件**

每一列按照/etc/passwd密码文件的格式书写，要注意每个用户的用户名、UID、宿主目录都不可以相同，其中密码栏可以留做空白或输入x号。一个范例文件user.txt内容如下：

![image](https://github.com/user-attachments/assets/c606d312-ecea-4319-86ed-d93f62cf140a)

**执行/usr/sbin/newusers命令**

需要root权限：

![image](https://github.com/user-attachments/assets/12442a3a-c23f-47a9-8244-6022a77eb129)

可以执行命令 vipw 或 vi /etc/passwd 检查 /etc/passwd 文件是否已经出现这些用户的数据，并且用户的宿主目录是否已经创建。

**取消 shadow password 功能**

将 /etc/shadow 产生的 shadow 密码解码，然后回写到 /etc/passwd 中，并将/etc/shadow的shadow密码栏删掉。这是为了方便下一步的密码转换工作，即先取消 shadow password 功能。

执行/usr/sbin/pwunconv命令:

![image](https://github.com/user-attachments/assets/22edc501-54d9-4010-9681-470f44aecffc)

**编辑每个用户的密码对照文件**

格式为：

![image](https://github.com/user-attachments/assets/f7602e99-b577-47bd-81d2-b3d534833b7a)


实例文件 passwd.txt 内容如下：

![image](https://github.com/user-attachments/assets/91c33fee-fcf2-4027-ad2d-ba94946a1916)

**执行 /usr/sbin/chpasswd命令**

需要root权限：

创建用户密码，chpasswd 会将经过 /usr/bin/passwd 命令编码过的密码写入 /etc/passwd 的密码栏。

![image](https://github.com/user-attachments/assets/cbb1942a-3a85-46c7-b8d0-e0041b4ed59f)

**将密码编码为 shadow password**

执行命令 /usr/sbin/pwconv 将密码编码为 shadow password，并将结果写入 /etc/shadow。

![image](https://github.com/user-attachments/assets/97e10694-059f-416d-aba3-f44f977363b9)


这样就完成了大量用户的创建了，之后您可以到/home下检查这些用户宿主目录的权限设置是否都正确，并登录验证用户密码是否正确。

**完整步骤**

先准备好用户文件user和密码文件passwd

然后运行：

![image](https://github.com/user-attachments/assets/ba3e974a-8e7d-488e-90ea-aa631e4330f7)


## crontab的使用
crontab命令是cron table的简写，它是cron的配置文件，也可以叫它作业列表。

相关配置文件如下：

- /var/spool/cron/ 目录下存放的是每个用户包括root的crontab任务，每个任务以创建者的名字命名
- /etc/crontab 这个文件负责调度各种管理和维护任务。
- /etc/cron.d/ 这个目录用来存放任何要执行的crontab文件或脚本。
- 还可以把脚本放在/etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly、/etc/cron.monthly目录中，让它每小时/天/星期、月执行一次。

命令格式：

![image](https://github.com/user-attachments/assets/c0814c53-9f16-48d7-8491-7271b0e77bc4)


**crontab -e**进入当前用户的工作表编辑，是常见的vim界面。每行是一条命令。

crontab的命令构成为 时间+动作，其时间有**分、时、日、月、周**五种，操作符有

- ***** 取值范围内的所有数字
- / 每过多少个数字
- - 从X到Z
- **，**散列数字
  
基本格式 :

![image](https://github.com/user-attachments/assets/5fa4754b-05bf-4c30-970a-fe1bcbd51845)

![image](https://github.com/user-attachments/assets/4903bf20-05e9-4f8c-9b24-fd47e1cc7bf7)

- 其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。command表示要执行的命令。
- 当 f1 为 * 时表示每分钟都要执行 program，f2 为 * 时表示每小时都要执行程序，以此类推
- 当 f1 为 a-b 时表示从第 a 分钟到第 b 分钟这段时间内要执行，f2 为 a-b 时表示从第 a 到第 b 小时都要执行，以此类推
- 当 f1 为 */n 时表示每 n 分钟个时间间隔执行一次，f2 为 */n 表示每 n 小时个时间间隔执行一次，以此类推
- 当 f1 为 a, b, c,… 时表示第 a, b, c,… 分钟要执行，f2 为 a, b, c,… 时表示第 a, b, c…个小时要执行，以此类推

在 12 月内, 每天的早上 6 点到 12 点，每隔 3 个小时 0 分钟执行一次 /usr/bin/backup

![image](https://github.com/user-attachments/assets/d6ecbd61-2169-4d5d-b803-8279da664348)

周一到周五每天下午 5:00 寄一封信给 alex@domain.name

![image](https://github.com/user-attachments/assets/8daad7dd-1704-419e-ba9a-cc83e141f4e9)


每月每天的午夜 0 点 20 分, 2 点 20 分, 4 点 20 分…执行 echo “haha”

![image](https://github.com/user-attachments/assets/07612cbc-5baa-45b5-a242-b728d7fc5813)


示例1：

![image](https://github.com/user-attachments/assets/90f6b651-7804-4818-ba6a-6302d20c0a65)


示例2：

```txt
0 */2 * * * /sbin/service httpd restart  每两个小时重启一次apache 

50 7 * * * /sbin/service sshd start  每天7：50开启ssh服务 

50 22 * * * /sbin/service sshd stop  每天22：50关闭ssh服务 

0 0 1,15 * * fsck /home  每月1号和15号检查/home 磁盘 

1 * * * * /home/bruce/backup  每小时的第一分执行 /home/bruce/backup这个文件 

00 03 * * 1-5 find /home "*.xxx" -mtime +4 -exec rm {} \;  每周一至周五3点钟，在目录/home中，查找文件名为*.xxx的文件，并删除4天前的文件。

30 6 */10 * * ls  每月的1、11、21、31日是的6：30执行一次ls命令
```

**环境变量问题：**

有时创建了一个crontab，但是这个任务却无法自动执行，而手动执行这个任务却没有问题，这种情况一般是由于在crontab文件中没有配置环境变量引起的。

所以注意如下3点：

1）脚本中涉及文件路径时写全局路径；

2）脚本执行要用到java或其他环境变量时，通过source命令引入环境变量，如：

![image](https://github.com/user-attachments/assets/1d00a935-806d-486d-a527-8a8da14554cd)


3）当手动执行脚本OK，但是crontab死活不执行时，可以尝试在crontab中直接引入环境变量解决问题。如：

![image](https://github.com/user-attachments/assets/748d5bac-424d-4a1b-918f-eb2dab2ff8d4)


# 特殊权限
linux共12位权限，除了9位基础权限还有3个特殊权限。

## 三种特殊的权限
### SetUID(suid)
命令功能： **临时使用命令的属主权限执行该命令。**即如果文件有suid权限时，那么普通用户去执行该文件时，会以该文件的所属用户的身份去执行。

SetUID（简写suid）：会在属主权限位的执行权限上写个s。 如果该属主权限位上有执行权限，则会在属主权限位的执行权限上写个s（小写）； 如果该属主权限位上没有执行权限，则会在属主权限位的执行权限上写个S（大写）。

suid数字权限是4000,设置方法：

![image](https://github.com/user-attachments/assets/a045d368-f3c0-422a-baf9-b636fc2471b0)

查看passwd命令的权限

```txt
`[root@localhost ftl]``# ll /usr/bin/passwd ` `问题： ``passwd``文件的属组是root,表示只有root用户可以访问的文件，为什么普通用户依然可以使用该命令更改自己的密码？``答案：当普通用户[omd]使用``passwd``命令的时候，系统看到``passwd``命令文件的属性有大写s后，表示这个命令的属主权限被omd用户获得,也就是omd用户获得文件``/etc/shadow``的root的rwx权限`
```

由于passwd具有s权限，普通用户使用该命令的时候，就会以该命令的属主身份root执行该命令，于是能够顺利修改普通用户不具备修改权限的/etc/shadow文件。

希望普通用户user1可以删除某个自己没有权限删除的文件的操作方法：

- sudo给user1授权rm权限
- rm设置suid
- 修改被删除文件上级目录的权限

**SetUID（简称suid）总结：**

1.让普通用户对可执行的二进制文件，临时拥有二进制文件的属主权限；

2.如果设置的二进制文件没有执行权限，那么suid的权限显示就是S（大写字母S）；

3.特殊权限suid仅对二进制可执行程序有效，其他文件或目录则无效。

4.suid极其危险，如果给vim或者rm命令设置了setUID，那么任何文件都能编辑或者删除了，相当于有root权限了。

### setGID（sgid）
**命令功能：**使用sgid可以使得多个用户之间共享一个目录的所有文件变得简单。当某个目录设置了sgid后，在该目录中新建的文件不在是创建该文件的默认所属组。

如果该属组权限位上有执行权限，则会在属组主权限位的执行权限上写个s（小写字母）； 如果该属组权限位上没有执行权限，则会在属组主权限位的执行权限上写个S（大写字母S）。

write命令的权限：

![image](https://github.com/user-attachments/assets/5b7039fd-d92d-4bc0-95b5-4cb90066ca33)


sgid数字权限是2000，设置方法：

![image](https://github.com/user-attachments/assets/7ceef0d3-a92f-4eb5-8617-7ec6e2e8958a)

在设置SetGID的文件夹创建文件的属组是父目录的属组：

![image](https://github.com/user-attachments/assets/b51de2bd-cdb0-47b7-b424-240a45a6fd63)

### sticky(sbit)粘滞位
**命令功能：**粘滞位，只对目录有效，对某目录设置粘滞位后，普通用户就算有w权限也只能删除该目录下自己建立的文件，而不能删除其他用户建立的文件。

如果该其他用户权限位上有执行权限，则会在其他用户权限位的执行权限上写个t（小写）； 如果该其它用户权限位上没有执行权限，则会在其他用户权限位的执行权限上写个T（大写）。

系统中存在的/tmp目录是经典的粘滞位目录，谁都有写权限，因此安全成问题，常常是木马第一手跳板。

![image](https://github.com/user-attachments/assets/5fdcbe08-6be1-43b6-9997-7e13e07a3052)

sbit数字权限是1000，设置方法：

![image](https://github.com/user-attachments/assets/c0c3cc6d-873a-4462-8f2f-ca751c33949f)


## chattr权限
chattr概述：凌驾于r、w、x、suid、sgid之上的权限。

### lsattr：查看特殊权限

![image](https://github.com/user-attachments/assets/1ec3a39e-fac9-4d2a-8b46-5d3a9352f07a)


### chattr：设置特殊权限

![image](https://github.com/user-attachments/assets/9bd3beaf-7da6-4fae-9082-70a248780ae1)


防止系统中某个关键文件被修改：

![image](https://github.com/user-attachments/assets/3b372815-4da8-4094-9802-b635442b9407)

让某个文件只能往里面追加内容，不能删除，一些日志文件适用于这种操作：

![image](https://github.com/user-attachments/assets/57d99a24-b1e0-444c-a5a6-71b0aa4a7507)


## 掩码umask
### umask的作用
umask值用于设置用户在创建文件时的默认权限，当我们在系统中创建目录或文件时，目录或文件所具有的默认权限就是由umask值决定的。

对于root用户，系统默认的umask值是0022；对于普通用户，系统默认的umask值是0002。执行umask命令可以查看当前用户的umask值。

![image](https://github.com/user-attachments/assets/7b00494b-9e4b-4e0b-b3cb-c5efa8001d50)

### umask是如何改变新文件的权限
umask值一共有4组数字，其中第1组数字用于定义特殊权限，一般不予考虑，与一般权限有关的是后3组数字。

默认情况下，对于目录，用户所能拥有的最大权限是777；对于文件，用户所能拥有的最大权限是目录的最大权限去掉执行权限，即666。因为x执行权限对于目录是必须的，没有执行权限就无法进入目录，而对于文件则不必默认赋予x执行权限。

对于root用户，他的umask值是022。当root用户创建目录时，默认的权限就是用最大权限777去掉相应位置的umask值权限，即对于所有者不必去掉任何权限，对于所属组要去掉w权限，对于其他用户也要去掉w权限，所以目录的默认权限就是755；当root用户创建文件时，默认的权限则是用最大权限666去掉相应位置的umask值，即文件的默认权限是644。

通过umask命令可以修改umask值，比如将umask值设为0077。

![image](https://github.com/user-attachments/assets/867586e7-d49a-45a4-9b12-8647c02ef9b5)


### 永久修改umask
umask命令只能临时修改umask值，系统重启之后umask将还原成默认值。如果要永久修改umask值，可修改/etc/bashrc或/etc/profile文件。

例如要将默认umask值设置为027，那么可以在文件中增加一行umask 027。

# linux软件安装
## Ubuntu软件安装与卸载
### 更新Ubuntu软件下载地址
开源软件镜像站 ：https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

Ubuntu 的软件源配置文件是 /etc/apt/sources.list。将系统自带的该文件做个备份，将该文件替换为下面内容，即可使用 TUNA 的软件源镜像。

ubuntu版本: 16.04 LTS

![image](https://github.com/user-attachments/assets/1aaf6740-c22f-4cee-b829-b714aa397191)


然后

![image](https://github.com/user-attachments/assets/6923fd6b-9fe2-4c3f-9902-bda9711d3e3c)


再sudo vim /etc/apt/sources.list修改为以上内容

### Ubuntu软件操作的相关命令


## yum安装命令
yum（ Yellow dog Updater, Modified）是一个在Fedora和RedHat以及SUSE中的Shell前端软件包管理器。

基於RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软体包，无须繁琐地一次次下载、安装。

yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

### 更新国内yum源
网易（163）yum源是国内最好的yum源之一 ，无论是速度还是软件版本，都非常的不错。

将yum源设置为163 yum，可以提升软件包安装和更新的速度，同时避免一些常见软件版本无法找到。

首先备份/etc/yum.repos.d/CentOS-Base.repo

```txt
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

下载对应版本 repo 文件, 放入 /etc/yum.repos.d/

- CentOS5 ：http://mirrors.163.com/.help/CentOS5-Base-163.repo
- CentOS6 ：http://mirrors.163.com/.help/CentOS6-Base-163.repo
- CentOS7 ：http://mirrors.163.com/.help/CentOS7-Base-163.repo



运行以下命令生成缓存

```txt
yum clean all
yum makecache
```

除了网易之外，国内还有其他不错的 yum 源，比如中科大和搜狐。

中科大的 yum 源，安装方法查看：https://lug.ustc.edu.cn/wiki/mirrors/help/centos

sohu 的 yum 源安装方法查看: http://mirrors.sohu.com/help/centos.html

## yum常用命令
yum 语法：

```txt
yum [options] [command] [package ...]
```


选项：

- **options：**可选，选项包括-h（帮助），-y（当安装过程提示选择全部为"yes"），-q（不显示安装的过程）等等。
- **command：**要进行的操作。
- **package：**操作的对象。

实例：

- 列出所有可更新的软件清单命令：yum check-update
- 更新所有软件命令：yum update
- 仅安装指定的软件命令：yum install <package_name>
- 仅更新指定的软件命令：yum update <package_name>
- 显示包信息：yum info <package_name>
- 列出所有可安裝的软件清单命令：yum list
- 删除软件包命令：yum remove <package_name>
- 查找软件包 命令：yum search <keyword>
- 清除缓存命令:

1.yum clean packages: 清除缓存目录下的软件包
  
2.yum clean headers: 清除缓存目录下的 headers

3.yum clean oldheaders: 清除缓存目录下旧的 headers

4.yum clean, yum clean all (= yum clean packages; yum clean oldheaders) :清除缓存目录下的软件包及旧的headers

## yum在线安装MySQL5.7
Step1: 检测系统是否自带安装mysql

```txt
yum list installed | grep mysql
```

Step2: 删除系统自带的mysql及其依赖

```txt
yum -y remove mysql-libs.x86_64
```

Step3: 给CentOS添加rpm源，并且选择较新的源

```txt
wget dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
yum localinstall mysql-community-release-el7-5.noarch.rpm
yum repolist all | grep mysql
yum-config-manager --disable mysql55-community
yum-config-manager --disable mysql56-community
yum-config-manager --enable mysql57-community-dmr
yum repolist enabled | grep mysql
```

Step4:安装mysql 服务器

```txt
yum install mysql-community-server
```

Step5: 启动mysql

```txt
service mysqld start
```

grep “password” /var/log/mysqld.log(查看临时密码)

```txt
SET PASSWORD = PASSWORD('your new password');
ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
flush privileges;
```

默认的要求必须的设置格式：

**包含数字、小写或大写字母以及特殊字符**

默认的要求必须的设置格式：

**包含数字、小写或大写字母以及特殊字符**

如果不想复杂，可以使用以下方式

```txt
set global validate_password_policy=0;
set global validate_password_length=1;
```

Step6: 查看mysql是否自启动,并且设置开启自启动

```txt
# chkconfig --list | grep mysqld
# chkconfig mysqld on
```
Step7: mysql安全设置

```txt
mysql_secure_installation
```

## rpm
RPM是Red Hat公司随Redhat Linux推出了一个软件包管理器，通过它能够更加轻松容易地实现软件的安装。

**常见用法：**

- rpm -ivh <rpm包名> 安装软件
- rpm -e <rpm包名> 卸载安装
- rpm -qi <rpm包名> 显示软件安装信息
- rpm -qa | grep xxx 查询软件是否安装（包括相关依赖）
- rpm -Uvh <rpm包名> 升级一个rpm

**具体参数详解：**

-i, --install 安装包

-v, --verbose 列出更多详细信息，安装进度

-h, --hash 安装时列出hash标记 (与 -v连用)

-e, --erase 卸载安装包

-U, --upgrade=+ 升级包

–replacepkge 无论软件包是否已被安装，都强行安装软件包

–test 安装测试，并不实际安装

–nodeps 忽略软件包的依赖关系强行安装

–force 忽略软件包及文件的冲突

-q,–query:

-a, --all 查询/校验所有的安装包

-p, --package 查询/校验一个安装文件

-l, --list 列出安装文件

-d, --docfiles 列出所有文档文件

-f, --file 查询/校验安装包中所包含的文件

安装软件：

```txt
# rpm -hvi dejagnu-1.4.2-10.noarch.rpm 
警告：dejagnu-1.4.2-10.noarch.rpm: V3 DSA 签名：NOKEY, key ID db42a60e
准备...           
########################################### [100%]
```

显示软件安装信息：

```txt
# rpm -qi dejagnu-1.4.2-10.noarch.rpm
```

【第1次更新 教程、类似命令关联】


## Linux的基本配置
1.修改主机名

```txt
vi /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=hadoop1
```

2.修改ip地址

```txt
vi /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
TYPE=Ethernet
ONBOOT=yes
BOOTPROTO=static
IPADDR=192.168.100.101
NETMASK=255.255.255.0

service network restart
```

3.修改ip地址和主机名的映射关系

```txt
vi /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.100.101 hadoop1
```

4.关闭iptables并设置其开机启动/不启动

```txt
service iptables stop
chkconfig iptables on
chkconfig iptables off
```

## 安装JDK

```txt
1.上传jdk-7u45-linux-x64.tar.gz到Linux上
2.解压jdk到/usr/local目录
tar -zxvf jdk-7u45-linux-x64.tar.gz -C /usr/local/
3.设置环境变量，在/etc/profile文件最后追加相关内容(技巧r:!pwd)
vi /etc/profile
export JAVA_HOME=/usr/local/jdk1.7.0_45
export PATH=$PATH:$JAVA_HOME/bin
4.刷新环境变量
source /etc/profile
5.测试java命令是否可用
java -version
```

## 制作本地YUM源
上传CentOS-6.7-x86_64-bin-DVD1.iso到服务器

将CentOS-6.7-x86_64-bin-DVD1.iso镜像挂载到某个目录:

```txt
mkdir /var/iso
mount -o loop CentOS-6.7-x86_64-bin-DVD1.iso /var/iso
```

安装并启动Apache服务器：

```txt
yum install -y httpd
service httpd start
```

使用浏览器访问http://192.168.100.101（如果访问不通，检查防火墙是否开启了80端口或关闭防火墙）

将YUM源配置到httpd中：

```txt
cp -r /var/iso/ /var/www/html/CentOS-6.7
umount /var/iso
```


在浏览器中访问http://192.168.100.101/CentOS-6.7/

![image](https://github.com/user-attachments/assets/8e4b747f-5be5-47e0-b21a-1e531dac7218)


**配置使用YUM源：**

备份原有的YUM源的配置文件

```txt
cd /etc/yum.repos.d/
rename .repo .repo.bak *
```

修改YUM源配置文件

```txt
vi CentOS-Local.repo
[base]
name=CentOS-Local
baseurl=http://192.168.100.101/CentOS-6.7
gpgcheck=1
enabled=1   #很重要，1才启用
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
```

重建yum缓存

```txt
#清除yum缓存文件，重新新建
yum clean all && yum makecache
#列出可用的YUM源
yum repolist
```

**rpm包生成yum源目录**

如果已经下载好了rpm包，可以自行制作一个yum源（yum仓库）。将下载的rpm包上传到centos服务器上（比如/data/rpm目录下），然后进入存放rpm包的目录，执行以下命令：

```txt
# cd /data/rpm
# createrepo .
```

这样，rpm包存放的目录就可以作为yum源目录使用。

如果提示找不到createrepo命令，可以使用yum install createrepo安装该程序。

# Shell编程
这里说的Shell 脚本（shell script），是在Linux 环境下运行的脚本程序

Shell 编程跟 JavaScript、php 编程一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

Linux 的 Shell 种类众多，常见的有：

- Bourne Shell（/usr/bin/sh或/bin/sh）
- Bourne Again Shell（/bin/bash）
- C Shell（/usr/bin/csh）
- K Shell（/usr/bin/ksh）
- Shell for Root（/sbin/sh）
- ……

Bash是大多数Linux 系统默认的 Shell，本文也仅关注Bash Shell。

在一般情况下，并不区分 Bourne Shell 和 Bourne Again Shell，所以，像 **#!/bin/sh**，它同样也可以改为 **#!/bin/bash。**

**#!** 告诉系统其后路径所指定的程序即是解释此脚本文件的 Shell 程序。

## 入门
### 运行Shell脚本
编写shell脚本：

```txt
vi test.sh

#!/bin/bash
echo "Hello World !"
```

#! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。

echo 命令用于向窗口输出文本。

运行 Shell 脚本有两种方法：

**1、作为可执行程序**

```txt
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```

默认情况下，一定要写成 ./test.sh，而不是 test.sh，运行其它二进制的程序也一样。

除非将当前目录.加入到PATH环境变量中，配置方法：

```txt
sudo vi /etc/profile
加入一行
export PATH=$PATH:.
保存之后，执行
source /etc/profile
```

**2、作为解释器参数**

直接运行解释器，其参数就是 shell 脚本的文件名：

```txt
/bin/sh test.sh
```

这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。

## 编写一个快捷创建shell脚本的命令

```txt
#!/bin/bash
if test -z $1;then
  newfile="./script_`date +%m%d_%s`"
else
  newfile=$1
fi
echo $newfile
if  ! grep "^#!" $newfile &>/dev/null; then
cat >> $newfile << EOF
#!/bin/bash
# Author:
# Date & Time: `date +"%F %T"`
#Description:
EOF
fi
vim +5 $newfile
chmod +x $newfile
```

将以上内容编写好之后保存为shell文件，然后执行

```txt
chmod u+x shell
sudo mv shell /usr/bin/
```

## echo命令
Shell 的 echo 指令与 PHP 的 echo 指令类似，都是用于字符串的输出。命令格式：

```txt
echo string
```

显示普通字符串:

```txt
echo "It is a test"
```

这里的双引号完全可以省略，以下命令与上面实例效果一致：

```txt
echo It is a test
```

显示转义字符:

```txt
echo "\"It is a test\""
```

结果将是:

```txt
"It is a test"
```

同样，双引号也可以省略

read 命令从标准输入中读取一行,并把输入行的每个字段的值指定给 shell 变量

```txt
#!/bin/sh
read name 
echo "$name It is a test"
```

以上代码保存为 test.sh，name 接收标准输入的变量，结果将是:

```txt
[root@www ~]# sh test.sh
OK                     #标准输入
OK It is a test        #输出
```

**显示换行**

```txt
echo -e "OK! \n" # -e 开启转义
echo "It is a test"
```

输出结果：

```txt
OK!

It is a test
```

**显示不换行**

![image](https://github.com/user-attachments/assets/063e14db-e91e-4706-9af6-b4a524bbd916)

输出结果：

```txt
OK! It is a test
```

## printf 命令
printf 命令的语法：

```txt
printf  format-string  [arguments...]
```

**参数说明：**

- format-string: 为格式控制字符串
- arguments: 为参数列表。

实例如下：

```txt
#!/bin/bash
 
printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234 
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543 
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876 
```

执行脚本，输出结果如下所示：

```txt
姓名     性别   体重kg
郭靖     男      66.12
杨过     男      48.65
郭芙     女      47.99
```

- %s %c %d %f都是格式替代符
- %-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。
- %-4.2f 指格式化为小数，其中.2指保留2位小数。

printf的转义序列：

![image](https://github.com/user-attachments/assets/7d5512b1-7b18-4f0c-bdfc-9eb4cd2fc6b7)

例子：

```txt
python@ubuntu:~/test$ printf "a string, no processing:<%s>\n" "A\nB"
a string, no processing:<A\nB>
python@ubuntu:~/test$ printf "a string, no processing:<%b>\n" "A\nB"
a string, no processing:<A
B>
python@ubuntu:~/test$ printf "www.runoob.com \a"
www.runoob.com python@ubuntu:~/test$ 
```

## Shell 注释
以 # 开头的行就是注释，会被解释器忽略：

```txt
#--------------------------------------------
# 这是一个注释
# author：菜鸟教程
# site：www.taobao.com
# slogan：学的不仅是技术，更是梦想！
#--------------------------------------------
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
# 
#
##### 用户配置区 结束  #####
```

多行注释还可以使用以下格式：

```txt
:<<EOF
注释内容...
注释内容...
注释内容...
EOF
```

EOF 也可以使用其他符号:

```txt
:<<'
注释内容...
注释内容...
注释内容...
'

:<<!
注释内容...
注释内容...
注释内容...
!
```

# Shell变量
## 定义变量

```txt
your_name="taobao.com"
```

变量名的命名须遵循如下规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线（_）。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

## 使用变量
在变量名前面加美元符号即可，如：

```txt
your_name="qinjx"
echo $your_name
echo ${your_name}
```

加花括号可以帮助解释器识别变量的边界，比如：

```txt
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```

## 只读变量
使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

下面的例子尝试更改只读变量，结果报错：

```txt
python@ubuntu:~/shell$ myUrl="http://www.google.com"
python@ubuntu:~/shell$ readonly myUrl
python@ubuntu:~/shell$ myUrl="http://www.baidu.com"
-bash: myUrl: 只读变量
```

## 删除变量
使用 unset 命令可以删除变量，但不能删除只读变量：

```txt
#!/bin/sh
myUrl="http://www.baidu.com"
unset myUrl
echo $myUrl
```

## 变量类型
运行shell时，会同时存在三种变量：

- **1) 局部变量** 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- **2) 环境变量** 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- **3) shell变量** shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

## Shell 函数
shell中函数的定义格式如下：

```txt
[ function ] funname [()]
{
    action;
    [return int;]
}
```

说明：

- 1、可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
- 2、参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255)

示例：

```txt
#!/bin/bash

funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"
```

输出，类似下面：

```txt
这个函数会对输入的两个数字进行相加运算...
输入第一个数字: 
1
输入第二个数字: 
2
两个数字分别为 1 和 2 !
输入的两个数字之和为 3 !
```

函数返回值在调用该函数后通过 $? 来获得。

注意：所有函数在使用前必须定义。这意味着必须将函数放在脚本开始部分，直至shell解释器首次发现它时，才可以使用。调用函数仅使用其函数名即可。

在Shell中，调用函数时可以向其传递参数。在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数…

带参数的函数示例：

```txt
#!/bin/bash

funWithParam(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "第十个参数为 $10 !"
    echo "第十个参数为 ${10} !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73
```

输出结果：

```txt
第一个参数为 1 !
第二个参数为 2 !
第十个参数为 10 !
第十个参数为 34 !
第十一个参数为 73 !
参数总数有 11 个!
作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9 34 73 !
```

当n>=10时，需要使用${n}来获取参数。

另外，还有几个特殊字符用来处理参数：

![image](https://github.com/user-attachments/assets/9f32a7fe-7706-4525-a113-945cf9c00602)


## 文件包含
Shell 文件包含的语法格式如下：

```txt
. filename   # 注意点号(.)和文件名中间有一空格
或
source filename
```

**实例**

创建两个 shell 脚本文件。

test1.sh 代码如下：

```txt
#!/bin/bash

url="http://www.baidu.com"
```

test2.sh 代码如下：

```txt
#!/bin/bash

#使用 . 号来引用test1.sh 文件
. ./test1.sh
# 或者使用以下包含文件代码
# source ./test1.sh

echo "url地址：$url"
```

接下来，我们为 test2.sh 添加可执行权限并执行：

```txt
$ chmod +x test2.sh 
$ ./test2.sh 
url地址：http://www.baidu.com
```

![image](https://github.com/user-attachments/assets/e83b1663-fdd6-4c30-8e98-159c869a7867)

# shell数据类型
## 字符串
字符串可以用单引号，也可以用双引号，也可以不用引号。

单引号：

```txt
str='this is a string'
```

单引号字符串的限制：

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

双引号：

```txt
your_name='taobao'
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
```

输出结果为：

```txt
Hello, I know you are "taobao"! 
```

双引号的优点：

- 双引号里可以有变量
- 双引号里可以出现转义字符

拼接字符串：

```txt
your_name="taobao"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

输出结果为：

```txt
hello, taobao ! hello, taobao !
hello, taobao ! hello, ${your_name} !
```

**获取字符串长度${#s}**

```txt
string="abcd"
echo ${#string} #输出 4
```

**截取字符串${s:n1:n2}**

以下实例从字符串第 2 个字符开始截取 4 个字符：

```txt
string="taobao is a great site"
echo ${string:1:4} # 输出 unoo
```

**查找字符出现的位置expr index**

查找字符 i 或 o 的位置(哪个字母先出现就计算哪个)：

```txt
string="taobao is a great site"
echo `expr index "$string" io`  # 输出 3
```

**注意：** 以上脚本中 ` 是反引号，而不是单引号 '。

## 数组
bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

数组元素的下标由 0 开始编号。

### 定义数组
在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：

```txt
array_name=(value0 value1 value2 value3)
```

或者

```txt
array_name=(
value0
value1
value2
value3
)
```

或单独定义数组的各个分量：

```txt
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```

可以不使用连续的下标，而且下标的范围没有限制。

### 读取数组
读取数组元素值的一般格式是：

```txt
#!/bin/bash

my_array=(A B "C" D)

echo "第一个元素为: ${my_array[0]}"
echo "第二个元素为: ${my_array[1]}"
echo "第三个元素为: ${my_array[2]}"
echo "第四个元素为: ${my_array[3]}"
```

例子：

```txt
#!/bin/bash

my_array=(A B "C" D)

echo "第一个元素为: ${my_array[0]}"
echo "第二个元素为: ${my_array[1]}"
echo "第三个元素为: ${my_array[2]}"
echo "第四个元素为: ${my_array[3]}"
```

执行脚本，输出结果如下所示：

```txt
$ chmod +x test.sh 
$ ./test.sh
第一个元素为: A
第二个元素为: B
第三个元素为: C
第四个元素为: D
```

使用 @或* 符号可以获取数组中的所有元素，例如：

```txt
echo ${array_name[@]}
```

例子：

```txt
#!/bin/bash

my_array[0]=A
my_array[1]=B
my_array[2]=C
my_array[3]=D

echo "数组的元素为: ${my_array[*]}"
echo "数组的元素为: ${my_array[@]}"
```

执行脚本，输出结果如下所示：

```txt
$ chmod +x test.sh 
$ ./test.sh
数组的元素为: A B C D
数组的元素为: A B C D
```


### 获取数组的长度
获取数组长度的方法与获取字符串长度的方法相同，例如：

```txt
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
```


例子：

```txt
#!/bin/bash

my_array[0]=A
my_array[1]=B
my_array[2]=C
my_array[3]=D

echo "数组元素个数为: ${#my_array[*]}"
echo "数组元素个数为: ${#my_array[@]}"
```

执行脚本，输出结果如下所示：

```txt
$ chmod +x test.sh 
$ ./test.sh
数组元素个数为: 4
数组元素个数为: 4
```

## Shell传递参数
执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n。**

**n**代表一个数字，**1** 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

**$0** 为执行的文件名

test.sh文件内容如下：

```txt
vi test.sh
#!/bin/bash

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

运行结果：

```txt
python@ubuntu:~/test$ sh test.sh 1 2 3
Shell 传递参数实例！
执行的文件名：test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```

参数获取：

![image](https://github.com/user-attachments/assets/8da21610-129e-4329-8eb6-b862c15c1be4)

```txt
#!/bin/bash

echo "参数个数为：$#";
echo "$*传递的参数作为一个字符串显示：$*";
echo "$@传递的参数作为一个字符串显示：$@";
echo "脚本运行的当前进程ID号：$$";
echo "后台运行的最后一个进程的ID号：$!";
echo "$?"
```

执行脚本，输出结果如下所示：

```txt
python@ubuntu:~/test$ ./test.sh 1 2 3
参数个数为：3
1 2 3传递的参数作为一个字符串显示：1 2 3
1 2 3传递的参数作为一个字符串显示：1 2 3
脚本运行的当前进程ID号：5059
后台运行的最后一个进程的ID号：
0
```

$*与$@的区别：

- 只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则$* 等价于 “1 2 3”（传递了一个参数），而$@等价于 “1” “2” “3”（传递了三个参数）。

```txt
#!/bin/bash

echo "-- \"\$*\" 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \"\$@\" 演示 ---"
for i in "$@"; do
    echo $i
done

echo "-- \$* 演示 ---"
for i in $*; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in $@; do
    echo $i
done
```

执行脚本，输出结果如下所示：

```txt
python@ubuntu:~/test$ sh test 1 2 3
-- "$*" 演示 ---
1 2 3
-- "$@" 演示 ---
1
2
3
-- $* 演示 ---
1
2
3
-- $@ 演示 ---
1
2
3
```
