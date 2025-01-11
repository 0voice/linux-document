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

![image](https://github.com/user-attachments/assets/698a99ed-9356-4264-9397-69da5e1ed019)

选项-n 后面加次数，表示命令在执行的时候一次用的argument的个数，默认是用所有的。

xargs 结合 find 使用

用 rm 删除太多的文件时候，可能得到一个错误信息：/bin/rm Argument list too long. 用 xargs 去避免这个问题：

![image](https://github.com/user-attachments/assets/97257714-e6c6-4c54-90bc-35301112305a)

xargs -0 将 \0 作为定界符。

统计一个源代码目录中所有 php 文件的行数：

![image](https://github.com/user-attachments/assets/90b81d90-bcf7-4d00-9d51-16c962e85006)

查找所有的 jpg 文件，并且压缩它们：

![image](https://github.com/user-attachments/assets/82e186ec-9280-45e2-8df7-fbcb4130fb49)

批量下载：

![image](https://github.com/user-attachments/assets/e96b0721-c1bc-4dae-9f2f-8b64d9c7fb04)

wget的-c选项表示断点续传。



# Linux命令练习
## 常用命令
![image](https://github.com/user-attachments/assets/bb406a7c-7f0a-460f-88bb-fb6f4ae6a185)

## 系统命令
![image](https://github.com/user-attachments/assets/2ebdfba0-ff67-4b14-8f12-1cbc0a8b0d5f)

## 用户和组
![image](https://github.com/user-attachments/assets/0104d2cc-db43-4453-bfd1-0fe3475cf4f5)

## 权限
![image](https://github.com/user-attachments/assets/b0c99f8f-34b4-4bf9-9aff-ff5ebb86ac40)

## 帮助文档
![image](https://github.com/user-attachments/assets/3ad5a8e8-7ea9-4f4f-b197-4aac0075b35f)

文件相关命令

![image](https://github.com/user-attachments/assets/5f0fd033-2dcc-4742-91d0-b8f810e2645c)

## VIM
![image](https://github.com/user-attachments/assets/4693faa8-15db-41e3-a198-c9e232c81bfa)

## 查找
![image](https://github.com/user-attachments/assets/e03c93c0-cd66-49dc-896b-719b03742324)

## 打包与压缩
![image](https://github.com/user-attachments/assets/158e39ca-f975-4672-82f3-e66fddc3e658)

## 正则表达式
![image](https://github.com/user-attachments/assets/67218c3b-4e78-410d-9406-e759dadb1b0a)

## 输入输出重定向
![image](https://github.com/user-attachments/assets/e382d65e-4dee-4e08-bb8c-d79ddab1026d)

## 进程控制
![image](https://github.com/user-attachments/assets/0e1a8968-e207-4183-b5bb-595eaac336c7)

## 其他命令
### 远程文件复制：scp
scp 命令用于 Linux 之间复制文件和目录，scp是 secure copy 的缩写是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。

scp 是加密的，rcp 是不加密的，scp 是 rcp 的加强版。

使用scp命令要确保使用的用户具有可读取远程服务器相应文件的权限，否则scp命令是无法起作用的。

从本地复制到远程命令格式：

![image](https://github.com/user-attachments/assets/f224abe6-ff73-4c5b-ba0e-0f266e2702bb)

实例：

![image](https://github.com/user-attachments/assets/65cdb656-b1ed-47dd-a7df-3d16576ac8e8)

从远程复制到本地：

![image](https://github.com/user-attachments/assets/4a307c74-9ddb-4c98-b163-e0f59bf7229d)

-P 参数来设置命令的端口号：

![image](https://github.com/user-attachments/assets/fefcc24e-e811-4ba4-9d1e-80e4d42a498d)

## locate查找
locate命令会去保存文档和目录名称的数据库内，查找文件或目录。

一般情况我们只需要输入locate your_file_name 即可查找指定文件。

参数：

- -d或–database= 配置locate指令使用的数据库。locate指令预设的数据库位于/var/lib/mlocate目录里，文档名为mlocate.db。

查找passwd文件，输入以下命令：

![image](https://github.com/user-attachments/assets/4f712959-a0b3-4c88-a6fd-92ee2a5861bc)

locate与find的区别: find 是去硬盘找，locate 只在/var/lib/slocate资料库中找。

locate的速度比find快，它并不是真的查找，而是查数据库，一般文件数据库在/var/lib/mlocate/mlocate.db中，所以locate的查找并不是实时的，而是以数据库的更新为准，一般是系统自己维护，也可以手工升级数据库 ，命令为：

![image](https://github.com/user-attachments/assets/e9ec9c10-1b84-4d81-a193-07259359c5ad)

## which命令
which查找$PATH中设置命令及安装文件目录所在位置

![image](https://github.com/user-attachments/assets/51849d5e-78e8-4108-a053-3d17c65150fa)

## echo
常见用法：

![image](https://github.com/user-attachments/assets/2a35821e-17b0-4354-a31d-c0132ecce52d)

## 设置或显示环境变量：export
在 shell 中执行程序时，shell 会提供一组环境变量。export 可新增，修改或删除环境变量，供后续执行的程序使用。export 的效力仅限于该次登陆操作。

![image](https://github.com/user-attachments/assets/82b34ec1-a4cc-4a76-ac9f-505f97adabd6)

参数说明：

- -f 　代表[变量名称]中为函数名称。
- -n 　删除指定的变量。变量实际上并未删除，只是不会输出到后续指令的执行环境中。
- -p 　列出所有的shell赋予程序的环境变量。

![image](https://github.com/user-attachments/assets/c626bfd4-c27e-436e-ad2e-894ec4f6d2c8)

## 修改主机名&ip地址
显示主机名：hostname

临时修改：hostname xxx

**永久修改**

对于Ubuntu 系统

![image](https://github.com/user-attachments/assets/649679b8-b3cd-4be1-8cb1-163f3d705a8e)

对于centos系统

![image](https://github.com/user-attachments/assets/28447559-1ae7-4fab-9c98-47017165cb18)

在此配置文件中添加一条HOSTNAME=node1

针对centos7系统，可以使用如下命令

![image](https://github.com/user-attachments/assets/db191330-957c-454a-9990-5452ed8a6977)

一般需要重开shell甚至重启操作系统才能生效。

**修改IP地址**

ifconfig eth0 192.168.12.22(重启后无效)

![image](https://github.com/user-attachments/assets/c1223ac4-f88e-464d-8873-39953a99d2ec)

## mount挂载
mount 挂载外部存储设备到文件系统中

![image](https://github.com/user-attachments/assets/819a391d-4af8-4668-b2f6-8ac83ced923b)

将设备/dev/cdrom挂载到 挂载点 ： /mnt/cdrom中

![image](https://github.com/user-attachments/assets/24e5a0bc-afa8-460d-90bb-a3c42fa7c17a)

## ssh免密登陆
假如 A 要登陆 B

在A上操作：

首先生成密钥对

![image](https://github.com/user-attachments/assets/429252c7-5754-49dc-a4f0-e4cd44dfe953)

再将A自己的公钥拷贝并追加到B的授权列表文件authorized_keys中

![image](https://github.com/user-attachments/assets/5e6362c4-67c1-4419-9b31-474571697798)

## 批量添加用户
### 与用户账号有关的系统文件
完成用户管理的工作本质都是对有关的系统文件进行修改，这些系统文件包括/etc/passwd, /etc/shadow, /etc/group等。

**/etc/passwd记录用户的基本属性**

它的内容类似下面的例子：

![image](https://github.com/user-attachments/assets/40b7680f-06f2-465c-8c7e-a62cd18f75f7)

/etc/passwd中一行记录对应着一个用户，每行记录又被冒号(:)分隔为7个字段，其格式和具体含义如下：

![image](https://github.com/user-attachments/assets/b8d5aeaf-d66e-419f-8f1e-363fc608cf49)

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

![image](https://github.com/user-attachments/assets/529f9417-8851-40b0-95a6-a40e948d4757)

还有许多标准的伪用户，例如：audit, cron, mail, usenet等，它们也都各自为相关的进程和文件所需要。

**/etc/shadow**

对安全性要求较高的Linux系统都把/etc/passwd文件中的口令字段保存在/etc/shadow文件中，超级用户才拥有该文件读权限。

/etc/shadow中的记录行与/etc/passwd中的一一对应，它由pwconv命令根据/etc/passwd中的数据自动产生

字段是：

![image](https://github.com/user-attachments/assets/79cd2b04-8252-470c-a45d-b0b4dc21907e)

1."登录名"是与/etc/passwd文件中的登录名相一致的用户账号

2."口令"字段存放的是加密后的用户口令字，长度为13个字符。如果为空，则对应用户没有口令，登录时不需要口令；如果含有不属于集合 { ./0-9A-Za-z }中的字符，则对应的用户不能登录。

3."最后一次修改时间"表示的是从某个时刻起，到用户最后一次修改口令时的天数。大部分linux系统的时间起点是1970年1月1日。

4."最小时间间隔"指的是两次修改口令之间所需的最小天数。

5."最大时间间隔"指的是口令保持有效的最大天数。

6."警告时间"字段表示的是从系统开始警告用户到用户密码正式失效之间的天数。

7."不活动时间"表示的是用户没有登录活动但账号仍能保持有效的最大天数。

8."失效时间"字段给出的是一个绝对的天数，如果使用了这个字段，那么就给出相应账号的生存期。期满后，该账号就不再是一个合法的账号，也就不能再用来登录了。

下面是/etc/shadow的一个例子：

![image](https://github.com/user-attachments/assets/2f99a4e1-e2fe-4f6c-8cdf-9fa4558d4c85)

**/etc/group记录用户组信息**

每个用户都属于某个用户组；一个组中可以有多个用户，一个用户也可以属于不同的组。

当一个用户同时是多个组中的成员时，在/etc/passwd文件中记录的是用户所属的主组，也就是登录时所属的默认组，而其他组称为附加组。

用户要访问属于附加组的文件时，必须首先使用newgrp命令使自己成为所要访问的组中的成员。

用户组的所有信息都存放在/etc/group文件中，字段有：

![image](https://github.com/user-attachments/assets/e0f0ea47-5e8f-44fa-91ba-8db127adcc3c)

1."组名"是用户组的名称，由字母或数字构成。与/etc/passwd中的登录名一样，组名不应重复。

2."口令"字段存放的是用户组加密后的口令字。一般Linux 系统的用户组都没有口令，即这个字段一般为空，或者是*。

3."组标识号"与用户标识号类似，也是一个整数，被系统内部用来标识组。

4."组内用户列表"是属于这个组的所有用户的列表，不同用户之间用逗号(,)分隔。这个用户组可能是用户的主组，也可能是附加组。

/etc/group文件的一个例子如下：

![image](https://github.com/user-attachments/assets/91000c1f-b32d-4809-acc1-6e7b4eb95601)

## 实操
**先编辑一个文本用户文件**

每一列按照/etc/passwd密码文件的格式书写，要注意每个用户的用户名、UID、宿主目录都不可以相同，其中密码栏可以留做空白或输入x号。一个范例文件user.txt内容如下：

![image](https://github.com/user-attachments/assets/79c468d4-0082-4283-a83e-3993fd87bad9)

**执行/usr/sbin/newusers命令**

需要root权限：

![image](https://github.com/user-attachments/assets/3652d9b1-d14e-4727-b04f-81f2ec477d6e)

可以执行命令 vipw 或 vi /etc/passwd 检查 /etc/passwd 文件是否已经出现这些用户的数据，并且用户的宿主目录是否已经创建。

**取消 shadow password 功能**

将 /etc/shadow 产生的 shadow 密码解码，然后回写到 /etc/passwd 中，并将/etc/shadow的shadow密码栏删掉。这是为了方便下一步的密码转换工作，即先取消 shadow password 功能。

执行/usr/sbin/pwunconv命令:

![image](https://github.com/user-attachments/assets/45e555c3-dab4-4415-a5cf-7d03cd53a19b)

**编辑每个用户的密码对照文件**

格式为：

![image](https://github.com/user-attachments/assets/92f35f21-0be8-4f60-a2be-ef5fd6407311)

实例文件 passwd.txt 内容如下：

![image](https://github.com/user-attachments/assets/eca1db51-b159-4a7c-9c64-70870a697f91)

**执行 /usr/sbin/chpasswd命令**

需要root权限：

创建用户密码，chpasswd 会将经过 /usr/bin/passwd 命令编码过的密码写入 /etc/passwd 的密码栏。

![image](https://github.com/user-attachments/assets/8d1b64e9-28e4-4cf2-b4f8-bfb55041f81e)

**将密码编码为 shadow password**

执行命令 /usr/sbin/pwconv 将密码编码为 shadow password，并将结果写入 /etc/shadow。

![image](https://github.com/user-attachments/assets/1a7e1193-c70a-4766-a745-feb9c607a674)

这样就完成了大量用户的创建了，之后您可以到/home下检查这些用户宿主目录的权限设置是否都正确，并登录验证用户密码是否正确。

**完整步骤**

先准备好用户文件user和密码文件passwd

然后运行：

![image](https://github.com/user-attachments/assets/54734440-86ea-459d-8ecb-463c886ff025)

## crontab的使用
crontab命令是cron table的简写，它是cron的配置文件，也可以叫它作业列表。

相关配置文件如下：

- /var/spool/cron/ 目录下存放的是每个用户包括root的crontab任务，每个任务以创建者的名字命名
- /etc/crontab 这个文件负责调度各种管理和维护任务。
- /etc/cron.d/ 这个目录用来存放任何要执行的crontab文件或脚本。
- 还可以把脚本放在/etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly、/etc/cron.monthly目录中，让它每小时/天/星期、月执行一次。

命令格式：

![image](https://github.com/user-attachments/assets/ba49a2cd-cf78-4302-ae12-02b01b311d9b)

**crontab -e**进入当前用户的工作表编辑，是常见的vim界面。每行是一条命令。

crontab的命令构成为 时间+动作，其时间有**分、时、日、月、周**五种，操作符有

- ***** 取值范围内的所有数字
- / 每过多少个数字
- - 从X到Z
- **，**散列数字
  
基本格式 :

![image](https://github.com/user-attachments/assets/ad6fbea9-84b8-4bb3-8ecf-2ba01ccdcaac)

![image](https://github.com/user-attachments/assets/426ed76b-27ee-4448-9420-732c9cd7169f)

- 其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。command表示要执行的命令。
- 当 f1 为 * 时表示每分钟都要执行 program，f2 为 * 时表示每小时都要执行程序，以此类推
- 当 f1 为 a-b 时表示从第 a 分钟到第 b 分钟这段时间内要执行，f2 为 a-b 时表示从第 a 到第 b 小时都要执行，以此类推
- 当 f1 为 */n 时表示每 n 分钟个时间间隔执行一次，f2 为 */n 表示每 n 小时个时间间隔执行一次，以此类推
- 当 f1 为 a, b, c,… 时表示第 a, b, c,… 分钟要执行，f2 为 a, b, c,… 时表示第 a, b, c…个小时要执行，以此类推

在 12 月内, 每天的早上 6 点到 12 点，每隔 3 个小时 0 分钟执行一次 /usr/bin/backup

![image](https://github.com/user-attachments/assets/1786b4e6-a888-40a3-a5e4-fbc6872e3af6)

周一到周五每天下午 5:00 寄一封信给 alex@domain.name

![image](https://github.com/user-attachments/assets/5218ae3a-6863-42ac-b8c3-e54031939e0a)

每月每天的午夜 0 点 20 分, 2 点 20 分, 4 点 20 分…执行 echo “haha”

![image](https://github.com/user-attachments/assets/7966e7a6-909a-467e-a669-e4d7fbf12d07)

示例1：

![image](https://github.com/user-attachments/assets/44b4bb24-770b-49a5-917b-eecb35df5f58)

示例2：

![image](https://github.com/user-attachments/assets/bd3bae38-d7e9-41a1-a03b-72c6699614a3)

**环境变量问题：**

有时创建了一个crontab，但是这个任务却无法自动执行，而手动执行这个任务却没有问题，这种情况一般是由于在crontab文件中没有配置环境变量引起的。

所以注意如下3点：

1）脚本中涉及文件路径时写全局路径；

2）脚本执行要用到java或其他环境变量时，通过source命令引入环境变量，如：

![image](https://github.com/user-attachments/assets/abbba1e0-083c-4d75-a751-ee333279885b)

3）当手动执行脚本OK，但是crontab死活不执行时，可以尝试在crontab中直接引入环境变量解决问题。如：

![image](https://github.com/user-attachments/assets/17de4fdc-e7b8-4563-988b-f0bfd82088af)

# 特殊权限
linux共12位权限，除了9位基础权限还有3个特殊权限。

## 三种特殊的权限
### SetUID(suid)
命令功能： **临时使用命令的属主权限执行该命令。**即如果文件有suid权限时，那么普通用户去执行该文件时，会以该文件的所属用户的身份去执行。

SetUID（简写suid）：会在属主权限位的执行权限上写个s。 如果该属主权限位上有执行权限，则会在属主权限位的执行权限上写个s（小写）； 如果该属主权限位上没有执行权限，则会在属主权限位的执行权限上写个S（大写）。

suid数字权限是4000,设置方法：

![image](https://github.com/user-attachments/assets/033342a8-442f-4392-961c-5276e001fb3f)

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

![image](https://github.com/user-attachments/assets/35daa859-6041-4a63-85dd-698e504343c4)

sgid数字权限是2000，设置方法：

![image](https://github.com/user-attachments/assets/ffd9bbac-bd73-41cf-8c47-e8a6a93c03f3)

在设置SetGID的文件夹创建文件的属组是父目录的属组：

![image](https://github.com/user-attachments/assets/4c0c13d9-6277-40b2-b11e-d3497705a428)

### sticky(sbit)粘滞位
**命令功能：**粘滞位，只对目录有效，对某目录设置粘滞位后，普通用户就算有w权限也只能删除该目录下自己建立的文件，而不能删除其他用户建立的文件。

如果该其他用户权限位上有执行权限，则会在其他用户权限位的执行权限上写个t（小写）； 如果该其它用户权限位上没有执行权限，则会在其他用户权限位的执行权限上写个T（大写）。

系统中存在的/tmp目录是经典的粘滞位目录，谁都有写权限，因此安全成问题，常常是木马第一手跳板。

![image](https://github.com/user-attachments/assets/f7d66473-30f1-4a8e-8e45-048dac2934a2)

sbit数字权限是1000，设置方法：

![image](https://github.com/user-attachments/assets/d80582e4-d6a6-4cd6-a73e-2da077f7ad89)

## chattr权限
chattr概述：凌驾于r、w、x、suid、sgid之上的权限。

### lsattr：查看特殊权限

![image](https://github.com/user-attachments/assets/6d9f8047-7bb0-4159-989b-3e04cff9e6d6)

### chattr：设置特殊权限

![image](https://github.com/user-attachments/assets/585e7536-9086-42c5-8760-59756db1bfd7)

防止系统中某个关键文件被修改：

![image](https://github.com/user-attachments/assets/4aa95274-0d04-47ae-a407-7466f3ee4dee)

让某个文件只能往里面追加内容，不能删除，一些日志文件适用于这种操作：

![image](https://github.com/user-attachments/assets/0299160e-a3c6-4fc5-a439-9342aff3e564)

## 掩码umask
### umask的作用
umask值用于设置用户在创建文件时的默认权限，当我们在系统中创建目录或文件时，目录或文件所具有的默认权限就是由umask值决定的。

对于root用户，系统默认的umask值是0022；对于普通用户，系统默认的umask值是0002。执行umask命令可以查看当前用户的umask值。

![image](https://github.com/user-attachments/assets/8a64382b-a676-4b1e-800f-579c9fb0ecb9)

### umask是如何改变新文件的权限
umask值一共有4组数字，其中第1组数字用于定义特殊权限，一般不予考虑，与一般权限有关的是后3组数字。

默认情况下，对于目录，用户所能拥有的最大权限是777；对于文件，用户所能拥有的最大权限是目录的最大权限去掉执行权限，即666。因为x执行权限对于目录是必须的，没有执行权限就无法进入目录，而对于文件则不必默认赋予x执行权限。

对于root用户，他的umask值是022。当root用户创建目录时，默认的权限就是用最大权限777去掉相应位置的umask值权限，即对于所有者不必去掉任何权限，对于所属组要去掉w权限，对于其他用户也要去掉w权限，所以目录的默认权限就是755；当root用户创建文件时，默认的权限则是用最大权限666去掉相应位置的umask值，即文件的默认权限是644。

通过umask命令可以修改umask值，比如将umask值设为0077。

![image](https://github.com/user-attachments/assets/c32bf5e3-1a7f-480d-adcb-7598dea72821)

### 永久修改umask
umask命令只能临时修改umask值，系统重启之后umask将还原成默认值。如果要永久修改umask值，可修改/etc/bashrc或/etc/profile文件。

例如要将默认umask值设置为027，那么可以在文件中增加一行umask 027。

# linux软件安装
## Ubuntu软件安装与卸载
### 更新Ubuntu软件下载地址
开源软件镜像站 ：https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

Ubuntu 的软件源配置文件是 /etc/apt/sources.list。将系统自带的该文件做个备份，将该文件替换为下面内容，即可使用 TUNA 的软件源镜像。

ubuntu版本: 16.04 LTS

![image](https://github.com/user-attachments/assets/70a80062-39a8-4fef-af7e-7dae921a7dbe)

然后

![image](https://github.com/user-attachments/assets/64d376b6-1ab2-41a0-b866-caab397d804b)

再sudo vim /etc/apt/sources.list修改为以上内容

### Ubuntu软件操作的相关命令

![image](https://github.com/user-attachments/assets/5d5f727a-17ae-4b33-8b14-91fd2bd5de89)

## yum安装命令
yum（ Yellow dog Updater, Modified）是一个在Fedora和RedHat以及SUSE中的Shell前端软件包管理器。

基於RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软体包，无须繁琐地一次次下载、安装。

yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

### 更新国内yum源
网易（163）yum源是国内最好的yum源之一 ，无论是速度还是软件版本，都非常的不错。

将yum源设置为163 yum，可以提升软件包安装和更新的速度，同时避免一些常见软件版本无法找到。

首先备份/etc/yum.repos.d/CentOS-Base.repo

![image](https://github.com/user-attachments/assets/28353354-9bcd-4018-8e19-3bbbb78b5fe0)

下载对应版本 repo 文件, 放入 /etc/yum.repos.d/

- CentOS5 ：http://mirrors.163.com/.help/CentOS5-Base-163.repo
- CentOS6 ：http://mirrors.163.com/.help/CentOS6-Base-163.repo
- CentOS7 ：http://mirrors.163.com/.help/CentOS7-Base-163.repo

![image](https://github.com/user-attachments/assets/b388f38c-2b77-4144-a296-9ec328089ada)

运行以下命令生成缓存

![image](https://github.com/user-attachments/assets/6d9a270e-13bf-4375-aa39-45337887d6d8)

除了网易之外，国内还有其他不错的 yum 源，比如中科大和搜狐。

中科大的 yum 源，安装方法查看：https://lug.ustc.edu.cn/wiki/mirrors/help/centos

sohu 的 yum 源安装方法查看: http://mirrors.sohu.com/help/centos.html

## yum常用命令
yum 语法：

![image](https://github.com/user-attachments/assets/e870e089-44d4-4188-a7b2-3d84e27e8a42)

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

![image](https://github.com/user-attachments/assets/f6f5209d-ce32-4a61-8ec4-bfdcd3534a72)

Step2: 删除系统自带的mysql及其依赖

![image](https://github.com/user-attachments/assets/08dd7f37-39b5-4eb0-94e7-10d4bc4eedbe)

Step3: 给CentOS添加rpm源，并且选择较新的源

![image](https://github.com/user-attachments/assets/123b4393-efa8-44be-8224-dbac87088314)

Step4:安装mysql 服务器

![image](https://github.com/user-attachments/assets/994d5573-c3e0-45c8-8516-52fe04e10643)

Step5: 启动mysql

![image](https://github.com/user-attachments/assets/927a9779-325b-4499-baa8-7d6d055b158a)

grep “password” /var/log/mysqld.log(查看临时密码)

![image](https://github.com/user-attachments/assets/49e10bea-1496-40e3-8ad9-034f1908c76b)

默认的要求必须的设置格式：

**包含数字、小写或大写字母以及特殊字符**

默认的要求必须的设置格式：

**包含数字、小写或大写字母以及特殊字符**

如果不想复杂，可以使用以下方式

![image](https://github.com/user-attachments/assets/79ef6bda-6622-4fa5-89bc-48f0e282164e)

Step6: 查看mysql是否自启动,并且设置开启自启动

![image](https://github.com/user-attachments/assets/e7d8dad6-7401-43dc-8635-ea6c600ebb19)

Step7: mysql安全设置

![image](https://github.com/user-attachments/assets/a9ab7c60-e2c8-4807-8c86-9f017dbc7dd8)

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

![image](https://github.com/user-attachments/assets/24b6f420-8208-46e9-ada9-e32121b7b1d6)

显示软件安装信息：

![image](https://github.com/user-attachments/assets/e67fde58-754c-45b3-878e-5bbce0e7d81a)

## Linux的基本配置
1.修改主机名

![image](https://github.com/user-attachments/assets/7666f3d1-dd3b-4431-8253-f70317519b0b)

2.修改ip地址

![image](https://github.com/user-attachments/assets/9f687992-b724-4ba4-bc44-3d889342d890)

3.修改ip地址和主机名的映射关系

![image](https://github.com/user-attachments/assets/33c21074-703d-4c72-975e-65d6fefdc184)

4.关闭iptables并设置其开机启动/不启动

![image](https://github.com/user-attachments/assets/f391520b-440a-41b5-9017-4ce0cd48e563)

## 安装JDK
![image](https://github.com/user-attachments/assets/de75f8f9-dd1b-4776-8274-b1402e45678f)

## 制作本地YUM源
上传CentOS-6.7-x86_64-bin-DVD1.iso到服务器

将CentOS-6.7-x86_64-bin-DVD1.iso镜像挂载到某个目录:

![image](https://github.com/user-attachments/assets/1307b225-46b3-4ad7-9720-fec1f7335db3)

安装并启动Apache服务器：

![image](https://github.com/user-attachments/assets/72a06075-22ef-421a-bf07-5c80a81670ed)

使用浏览器访问http://192.168.100.101（如果访问不通，检查防火墙是否开启了80端口或关闭防火墙）

将YUM源配置到httpd中：

![image](https://github.com/user-attachments/assets/9aaa3971-d48d-47cb-97c8-8816e9099bde)

在浏览器中访问http://192.168.100.101/CentOS-6.7/

![image](https://github.com/user-attachments/assets/f2f5b28e-e4c0-4391-8691-b6866f35ed87)

**配置使用YUM源：**

备份原有的YUM源的配置文件

![image](https://github.com/user-attachments/assets/35aa3ee1-c9b5-4f5d-beae-b4f2db0b0ba0)

修改YUM源配置文件

![image](https://github.com/user-attachments/assets/e8674601-9834-44b4-823e-3dc86aa9bb47)

重建yum缓存

![image](https://github.com/user-attachments/assets/208b9199-ba72-4167-a2f2-d98e3aaee430)

**rpm包生成yum源目录**

如果已经下载好了rpm包，可以自行制作一个yum源（yum仓库）。将下载的rpm包上传到centos服务器上（比如/data/rpm目录下），然后进入存放rpm包的目录，执行以下命令：

![image](https://github.com/user-attachments/assets/9bb7733a-c3d9-47ea-a021-97201305a4b8)

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

![image](https://github.com/user-attachments/assets/1c74a9f0-460f-45fa-b3dd-44c8ba88585b)

#! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。

echo 命令用于向窗口输出文本。

运行 Shell 脚本有两种方法：

**1、作为可执行程序**

![image](https://github.com/user-attachments/assets/ebb55027-a163-4865-9819-5c7d2487c371)

默认情况下，一定要写成 ./test.sh，而不是 test.sh，运行其它二进制的程序也一样。

除非将当前目录.加入到PATH环境变量中，配置方法：

![image](https://github.com/user-attachments/assets/3514d96d-f1b4-4fe7-982f-c5a2e58f01c5)

**2、作为解释器参数**

直接运行解释器，其参数就是 shell 脚本的文件名：

![image](https://github.com/user-attachments/assets/c9f60835-dd25-4c99-a572-296e119e3c90)

这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。

## 编写一个快捷创建shell脚本的命令

![image](https://github.com/user-attachments/assets/2adadd5f-73c4-41d6-9c33-cac594ba5040)

将以上内容编写好之后保存为shell文件，然后执行

![image](https://github.com/user-attachments/assets/07d6db10-2ef1-4588-acfb-a047d8326abc)

## echo命令
Shell 的 echo 指令与 PHP 的 echo 指令类似，都是用于字符串的输出。命令格式：

![image](https://github.com/user-attachments/assets/5f3c1002-7a95-404a-885f-7a6fd934d073)

显示普通字符串:

![image](https://github.com/user-attachments/assets/06fae384-3d5f-4ac6-95dc-d6dec17f4dcb)

这里的双引号完全可以省略，以下命令与上面实例效果一致：

![image](https://github.com/user-attachments/assets/e65e6102-4c6b-498e-a358-e5e36e4140ed)

显示转义字符:

![image](https://github.com/user-attachments/assets/566bd546-34d9-4b13-ae4c-6fe8f4e450ee)

结果将是:

![image](https://github.com/user-attachments/assets/0acee32d-ea65-421c-9139-314bc1198cf0)

同样，双引号也可以省略

read 命令从标准输入中读取一行,并把输入行的每个字段的值指定给 shell 变量

![image](https://github.com/user-attachments/assets/00d955d2-75bf-4fe8-b446-6f9432ab2325)

以上代码保存为 test.sh，name 接收标准输入的变量，结果将是:

![image](https://github.com/user-attachments/assets/6952f6a6-f17a-4eb9-aa5a-4f09637f3318)

**显示换行**

![image](https://github.com/user-attachments/assets/96670c47-53b3-4ef8-9226-c3fa83edbd6f)

输出结果：

![image](https://github.com/user-attachments/assets/15c387d3-4c59-4e4e-b2ba-203dc1cd4093)

**显示不换行**

![image](https://github.com/user-attachments/assets/063e14db-e91e-4706-9af6-b4a524bbd916)

输出结果：

![image](https://github.com/user-attachments/assets/719bbf29-0543-4752-9475-70b387a28745)

## printf 命令
printf 命令的语法：

![image](https://github.com/user-attachments/assets/51b31f21-dc28-4e74-9f81-273af36de435)

**参数说明：**

- format-string: 为格式控制字符串
- arguments: 为参数列表。

实例如下：

![image](https://github.com/user-attachments/assets/aa2cc8c8-824b-46cf-9f7f-4b4a9620ebc8)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/08451484-77a9-4e71-93c8-7d6f54262355)

- %s %c %d %f都是格式替代符
- %-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。
- %-4.2f 指格式化为小数，其中.2指保留2位小数。

printf的转义序列：

![image](https://github.com/user-attachments/assets/59d99bf0-fdbb-4562-a426-a73bf509e67f)

例子：

![image](https://github.com/user-attachments/assets/5a69a278-d8dd-4d5c-b5e4-761011a0e4eb)

## Shell 注释
以 # 开头的行就是注释，会被解释器忽略：

![image](https://github.com/user-attachments/assets/41a7d732-dd1d-4403-be6b-58989e562252)

多行注释还可以使用以下格式：

![image](https://github.com/user-attachments/assets/fe172a39-2880-4c2c-b91b-fa1d85e0b827)

EOF 也可以使用其他符号:

![image](https://github.com/user-attachments/assets/76d3d52b-4efc-4d65-b538-7906e39c40d6)

# Shell变量
## 定义变量

![image](https://github.com/user-attachments/assets/c4eb0817-a135-49aa-a56e-964150cb165d)

变量名的命名须遵循如下规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线（_）。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

## 使用变量
在变量名前面加美元符号即可，如：

![image](https://github.com/user-attachments/assets/293c9aeb-5e50-4a90-835b-14105ae04a46)

加花括号可以帮助解释器识别变量的边界，比如：

![image](https://github.com/user-attachments/assets/8783cfdc-5e75-4867-bc6d-4bad6d9d8532)

## 只读变量
使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

下面的例子尝试更改只读变量，结果报错：

![image](https://github.com/user-attachments/assets/cc92e864-aa65-4bfa-bb9c-932cad87a41c)

## 删除变量
使用 unset 命令可以删除变量，但不能删除只读变量：

![image](https://github.com/user-attachments/assets/39c3fa07-fe7d-4dc2-ac01-37754a73c090)

## 变量类型
运行shell时，会同时存在三种变量：

- **1) 局部变量** 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- **2) 环境变量** 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- **3) shell变量** shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

## Shell 函数
shell中函数的定义格式如下：

![image](https://github.com/user-attachments/assets/d13ebff5-78b7-405d-b30a-3b7275cbda2f)

说明：

- 1、可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
- 2、参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255)

示例：

![image](https://github.com/user-attachments/assets/0796edb0-e332-49a9-a8a6-1469217ad5b2)

输出，类似下面：

![image](https://github.com/user-attachments/assets/f21221b8-cdb1-48c3-8070-c5c2dc57df09)

函数返回值在调用该函数后通过 $? 来获得。

注意：所有函数在使用前必须定义。这意味着必须将函数放在脚本开始部分，直至shell解释器首次发现它时，才可以使用。调用函数仅使用其函数名即可。

在Shell中，调用函数时可以向其传递参数。在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数…

带参数的函数示例：

![image](https://github.com/user-attachments/assets/2cb6e508-4645-4797-adcf-31cc7b05d9a8)

输出结果：

![image](https://github.com/user-attachments/assets/5d76f721-b3f1-4adc-a2cf-78b279ea3567)

当n>=10时，需要使用${n}来获取参数。

另外，还有几个特殊字符用来处理参数：

![image](https://github.com/user-attachments/assets/98d7cccf-f008-4ca4-9c58-799474999365)

## 文件包含
Shell 文件包含的语法格式如下：

![image](https://github.com/user-attachments/assets/92a41c03-8638-40c1-ab07-26c4062ea7b3)

**实例**

创建两个 shell 脚本文件。

test1.sh 代码如下：

![image](https://github.com/user-attachments/assets/1bd12f23-be4c-4e4e-b190-1ac307235ae0)

test2.sh 代码如下：

![image](https://github.com/user-attachments/assets/e6fde70b-544f-4744-83a4-3677a81d2f32)

接下来，我们为 test2.sh 添加可执行权限并执行：

![image](https://github.com/user-attachments/assets/193baee4-cbf8-46d9-a0e2-3571426db2a1)

![image](https://github.com/user-attachments/assets/9bd8d758-f3ee-4155-98d3-e609d34eb14b)

# shell数据类型
## 字符串
字符串可以用单引号，也可以用双引号，也可以不用引号。

单引号：

![image](https://github.com/user-attachments/assets/f1f4b93f-68c3-411f-9f92-e8c8fe27d09e)

单引号字符串的限制：

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

双引号：

![image](https://github.com/user-attachments/assets/6db1a0c0-f0bd-45c0-bd7d-d7bab8f9fb1c)

输出结果为：

![image](https://github.com/user-attachments/assets/89877d36-3417-4f9c-af7b-cc42ae431686)

双引号的优点：

- 双引号里可以有变量
- 双引号里可以出现转义字符

拼接字符串：

![image](https://github.com/user-attachments/assets/31e265a0-5abb-43a7-9907-1433678c656d)

输出结果为：

![image](https://github.com/user-attachments/assets/449e7d62-815c-4d8d-bee6-92c1f6848a60)

**获取字符串长度${#s}**

![image](https://github.com/user-attachments/assets/c28c23e3-0b2e-45cc-aa4e-e01be4cf7c65)

**截取字符串${s:n1:n2}**

以下实例从字符串第 2 个字符开始截取 4 个字符：

![image](https://github.com/user-attachments/assets/8554be06-278e-4bb2-8a5c-0dc83f6c4e4d)

**查找字符出现的位置expr index**

查找字符 i 或 o 的位置(哪个字母先出现就计算哪个)：

![image](https://github.com/user-attachments/assets/6dd9bc48-9dd4-4d85-a1a0-8af85b19244d)

**注意：** 以上脚本中 ` 是反引号，而不是单引号 '。

## 数组
bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

数组元素的下标由 0 开始编号。

### 定义数组
在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：

![image](https://github.com/user-attachments/assets/e4b22e4e-6dc5-4d12-b0e0-f544f6587d78)

或者

![image](https://github.com/user-attachments/assets/1f149b14-bc4f-4b7a-8990-a13394e683f2)

或单独定义数组的各个分量：

![image](https://github.com/user-attachments/assets/668c453d-0dff-419c-93f7-beedc952d985)

可以不使用连续的下标，而且下标的范围没有限制。

### 读取数组
读取数组元素值的一般格式是：

![image](https://github.com/user-attachments/assets/f2ce8ba0-4c8e-4bc8-9b7c-3d1832b46b0c)

例子：

![image](https://github.com/user-attachments/assets/9910b9a9-82b2-4ac0-9e1d-ce12973a2a5d)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/f4d2e835-b669-40dd-a15e-f3fdf7867f2d)

使用 @或* 符号可以获取数组中的所有元素，例如：

![image](https://github.com/user-attachments/assets/53a0ac2c-6046-4475-90a0-2f9eeef99416)

例子：

![image](https://github.com/user-attachments/assets/3d54b15e-ef77-4f23-9c1e-eafbc8e90961)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/16497979-5a55-4a2c-905d-9d0f1fec7e2f)

### 获取数组的长度
获取数组长度的方法与获取字符串长度的方法相同，例如：

![image](https://github.com/user-attachments/assets/f8e3f30f-4d44-4b91-80ea-43b0046ca945)

例子：

![image](https://github.com/user-attachments/assets/ae327bd4-eed0-46fa-9eab-fb9dea04ea1d)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/3bfa3578-50e2-443e-97b4-43cf7d495807)

## Shell传递参数
执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n。**

**n**代表一个数字，**1** 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

**$0** 为执行的文件名

test.sh文件内容如下：

![image](https://github.com/user-attachments/assets/4d4d8319-ee98-445a-acf0-202f72d759a7)

运行结果：

![image](https://github.com/user-attachments/assets/bde1a000-1208-41e0-bfe0-cf34214ea7d1)

参数获取：

![image](https://github.com/user-attachments/assets/77bc73c8-0671-4a51-8cab-fe2c16c0d19a)

![image](https://github.com/user-attachments/assets/683f1a5b-89f5-48d6-99bc-7bc2a9d4e4b8)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/74595ac7-20ff-40dc-9f9b-256b731c067a)

$*与$@的区别：

- 只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则$* 等价于 “1 2 3”（传递了一个参数），而$@等价于 “1” “2” “3”（传递了三个参数）。

![image](https://github.com/user-attachments/assets/8f7ba0ef-4de4-449f-8cb5-8f906c787e5f)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/cc4fad12-eda8-402d-ab36-93e85730b9f5)
