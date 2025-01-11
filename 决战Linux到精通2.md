
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

![image](https://github.com/user-attachments/assets/cb932a4b-8379-42cf-8798-defb8e9b3c07)

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

![image](https://github.com/user-attachments/assets/451f83d6-daa5-40a3-9c13-5b4397256541)

缩减连续重复的字符成指定的单个字符：

![image](https://github.com/user-attachments/assets/23b5a452-4f09-46cd-83cd-16ff063a3598)

删除指定的字符：

![image](https://github.com/user-attachments/assets/0bc931a2-d94c-4199-bd0b-41303549c73f)

### join - 文件按行连接
将两个文件中指定栏位相同的行连接起来。即按照两个文件中共同拥有的某一列，将对应的行拼接成一行。

注意：在使用join之前所处理的文件要事先经过排序。

![image](https://github.com/user-attachments/assets/fa0ecd18-9c4d-4e78-a73b-39309c1e4855)

使用join命令，将两个文件连接：

![image](https://github.com/user-attachments/assets/76388ce1-d482-4d2e-90ee-ab925b2150f1)

两个文件互换，输出结果的变化：

![image](https://github.com/user-attachments/assets/e1281a47-42c1-4fcc-9dd0-883aee9fb0ba)

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

![image](https://github.com/user-attachments/assets/337146ab-972f-4dd5-b415-b57b34ce6ddb)

参数：

- -d<间隔字符>或–delimiters=<间隔字符> 　用指定的间隔字符取代跳格字符。
- -s或–serial 　串列进行而非平行处理。
- [文件…] 指定操作的文件路径

使用paste指令将文件"file"、“testfile”、"testfile1"进行合并，输入如下命令：

![image](https://github.com/user-attachments/assets/cc773dbc-e509-4e63-9f04-12080d9520f9)

参数"-s"可以将一个文件中的多行数据合并为一行进行显示：

![image](https://github.com/user-attachments/assets/f788b6fb-b4f8-4f99-ba0f-50505a8019d1)

如果将文件位置改为-，表示接收标准输入：

![image](https://github.com/user-attachments/assets/4c81b2e5-15f3-499f-9db2-76c0f3680d63)

### split - 文件切割
split命令用于将一个文件分割成数个。

该指令将大文件分割成较小的文件，在默认情况下将按照每1000行切割成一个小文件。

语法：

![image](https://github.com/user-attachments/assets/b29f031d-8d39-4bfa-9e11-e5eea1325dc1)

参数说明：

- -<行数> : 指定每多少行切成一个小文件
- -b<字节> : 指定每多少字节切成一个小文件
- -C<字节> : 与参数"-b"相似，但是在切 割时将尽量维持每行的完整性
- [输出文件名] : 设置切割后文件的前置文件名， split会自动在前置文件名后再加上编号

使用指令"split"将文件"README"每6行切割成一个文件，输入如下命令：

![image](https://github.com/user-attachments/assets/bc23b7d0-d33e-431a-b16e-77a19d02fbdb)

以上命令执行后，指令"split"会将原来的大文件"README"切割成多个以"x"开头的小文件。而在这些小文件中，每个文件都只有6行内容。

以大小切割：

![image](https://github.com/user-attachments/assets/640c407c-4a7f-4d19-9491-58c0dedc781d)

### xargs - 参数代换
不是所有的命令都支持管道，如ls，对于不支持管道的命令，可以通过xargs让其有管道命令的效果，如下所示：

![image](https://github.com/user-attachments/assets/6d5d99b1-d300-443d-bab4-241e1b165c23)

如果没有xargs，ls -l的结果将不是前面find的标准输出，因为ls不支持管道命令。

xargs 用作替换工具，读取输入数据重新格式化后输出。

定义一个测试文件，内有多行文本数据：

![image](https://github.com/user-attachments/assets/83f38859-bf7c-4d57-8320-8eead6e53f29)

多行输入单行输出：

![image](https://github.com/user-attachments/assets/f63a15de-d001-4e45-aedc-ac8b50596070)

-n 选项多行输出：

![image](https://github.com/user-attachments/assets/01ecac0b-2238-4707-987d-e8509e04cf82)

-d 选项可以自定义一个定界符：

![image](https://github.com/user-attachments/assets/b71feb0a-5593-4945-800f-9304980de8cc)

结合 -n 选项使用：

![image](https://github.com/user-attachments/assets/3192fde6-07de-4094-8344-85301d1a6ec0)

读取 stdin，将格式化后的参数传递给命令:

![image](https://github.com/user-attachments/assets/8e02252f-9344-4165-a58b-04c458267386)

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

# Shell基本运算符
Shell 和其他编程语言一样，支持多种运算符，包括：

- 算数运算符
- 关系运算符
- 布尔运算符
- 字符串运算符
- 文件测试运算符

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

![image](https://github.com/user-attachments/assets/237d0eab-c676-47ae-87fc-33ee2165a564)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/9c1d8f71-5522-4660-845f-014ce6448d88)

两点注意：

- 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2。
- 完整的表达式要被 ` ` 包含，这个字符是反引号在 Esc 键下边。

## 算术运算符
下表列出了常用的算术运算符，假定变量 a 为 10，变量 b 为 20：

![image](https://github.com/user-attachments/assets/74eb0aa4-9ee4-4ee8-918d-d7a9342f4b04)

算术运算符实例如下：

![image](https://github.com/user-attachments/assets/acb95f5b-283c-4271-b4c1-36558c7bd204)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/66cb7402-a5f9-4780-973a-0e258c36b7a6)

**注意：**

- 乘号(*)前边必须加反斜杠\才能实现乘法运算；
- if…then…fi 是条件语句，后续将会讲解。
- 在 MAC 中 shell 的 expr 语法是：$((表达式))，此处表达式中的 “*” 不需要转义符号 \ 。

![image](https://github.com/user-attachments/assets/44d0d7a7-eb2d-4df4-8886-68bf3fd08f9f)

## 关系运算符
关系运算符只支持数字，不支持字符串，除非字符串的值是数字。

下表列出了常用的关系运算符，假定变量 a 为 10，变量 b 为 20：

![image](https://github.com/user-attachments/assets/fde7d101-4faa-4fca-8e9f-a606969635c6)

关系运算符实例如下：

![image](https://github.com/user-attachments/assets/1d427592-dee9-48ee-816f-db626e1f1451)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/213b7276-5f37-441a-80fe-59c8e9ed9071)

## 布尔运算符
下表列出了常用的布尔运算符，假定变量 a 为 10，变量 b 为 20：

![image](https://github.com/user-attachments/assets/d367c150-47b5-4aa2-9940-c939918304b0)

布尔运算符实例如下：

![image](https://github.com/user-attachments/assets/3d362469-88d5-496c-b747-32e709b24dae)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/03f1dd98-709d-4854-bd18-04c7794d1a87)

## 逻辑运算符
以下介绍 Shell 的逻辑运算符，假定变量 a 为 10，变量 b 为 20:

![image](https://github.com/user-attachments/assets/43161ba3-1475-4baf-a919-d6d22e328958)

逻辑运算符实例如下：

![image](https://github.com/user-attachments/assets/1f0d73c1-4002-42ed-935e-1f7aede58216)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/7783648b-1e93-49c1-b251-93def9cfbdea)

## 字符串运算符
下表列出了常用的字符串运算符，假定变量 a 为 “abc”，变量 b 为 “efg”：

![image](https://github.com/user-attachments/assets/8a4239e2-9050-4f8e-9d89-276b375a6478)

字符串运算符实例如下：

![image](https://github.com/user-attachments/assets/07fd1e06-3421-4f5c-82e6-b2b491df3281)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/fcfc4eef-3922-44fc-823c-36283f5086de)

## 文件测试运算符
文件测试运算符用于检测 Unix 文件的各种属性。

属性检测描述如下：

![image](https://github.com/user-attachments/assets/4965edd7-a069-4409-97bc-443de068d0d5)

其他检查符：

- **-S**: 判断某文件是否 socket。
- **-L**: 检测文件是否存在并且是一个符号链接。

变量 file 表示文件 /var/www/runoob/test.sh，它的大小为 100 字节，具有 rwx 权限。下面的代码，将检测该文件的各种属性：

![image](https://github.com/user-attachments/assets/f1bb488d-eda8-44df-8563-fad09677c824)

执行脚本，输出结果如下所示：

![image](https://github.com/user-attachments/assets/4e37c79e-1dcd-4173-b409-9d31916e2607)

# test命令
Shell中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。

## 数值测试

![image](https://github.com/user-attachments/assets/788eeddd-2dd8-4f93-8b48-eddfaaccf539)

实例演示：

![image](https://github.com/user-attachments/assets/998506b5-93df-48a4-8ba4-6712fd4f4367)

输出结果：

![image](https://github.com/user-attachments/assets/f0324e96-f6f1-4915-aa48-91c5f3fc3120)

代码中的 [] 执行基本的算数运算，如：

![image](https://github.com/user-attachments/assets/f7349aff-8811-4f49-9fa9-dec5a82bd352)

结果为:

![image](https://github.com/user-attachments/assets/d9cc3574-8e6c-4f4b-abc5-beb049de71fb)

## 字符串测试

![image](https://github.com/user-attachments/assets/806e4871-e53f-48f1-84b8-dbb8d925bbb1)

实例演示：

![image](https://github.com/user-attachments/assets/84bfd596-bdcf-4ac5-a5fe-f76a14375429)

输出结果：

![image](https://github.com/user-attachments/assets/dc2dc0fc-0ace-440d-a432-35db672418c6)

## 文件测试

![image](https://github.com/user-attachments/assets/713c06dd-d6d5-4629-a163-8902b2085abd)

实例演示：

![image](https://github.com/user-attachments/assets/848fd99c-4343-4830-84f1-b76710db6469)

输出结果：

![image](https://github.com/user-attachments/assets/39e4f5f1-71c1-4154-ae67-75e9d70c8ec6)

另外，Shell还提供了与( -a )、或( -o )、非( ! )三个逻辑操作符用于将测试条件连接起来，其优先级为："!“最高，”-a"次之，"-o"最低。例如：

![image](https://github.com/user-attachments/assets/10c8ebe8-4e84-4f9f-93cc-514d6dc9bb93)

输出结果：

![image](https://github.com/user-attachments/assets/159949da-9423-4847-8654-4cebd5fc2846)

# Shell 流程控制
## if else判断语句
if 语句语法格式：

![image](https://github.com/user-attachments/assets/b078a4e2-68df-4874-bede-1df81db7bdd6)

写成一行（适用于终端命令提示符）：

![image](https://github.com/user-attachments/assets/402d05de-b3d3-4973-9af0-86ad301a9427)

if else 语法格式：

![image](https://github.com/user-attachments/assets/b81df188-e857-4e96-9bf4-629563e69495)

if else-if else 语法格式：

![image](https://github.com/user-attachments/assets/aafd94e5-ec47-4cba-abc3-114779fd65ba)

以下实例判断两个变量是否相等：

![image](https://github.com/user-attachments/assets/b933420b-bab6-4f89-8e7b-e84ec10bb98f)

输出结果：

![image](https://github.com/user-attachments/assets/3e4c2396-8314-49dc-bc03-2f33428f26e9)

if else语句经常与test命令结合使用，如下所示：

![image](https://github.com/user-attachments/assets/aca6548f-a7e8-4e71-bc48-b9eaf5cbb2fc)

输出结果：

![image](https://github.com/user-attachments/assets/2e01368c-c7fe-49df-b3d6-9d0b6003a698)


## for循环
for循环一般格式为：

![image](https://github.com/user-attachments/assets/52a21c07-a421-427c-b3bc-076354fd748b)

写成一行：

![image](https://github.com/user-attachments/assets/0dcda478-4ffb-4145-95e9-2588e2403702)

例如，顺序输出当前列表中的数字：

![image](https://github.com/user-attachments/assets/28b58508-209a-4104-9b7f-cf7d62c076f3)

输出结果：

![image](https://github.com/user-attachments/assets/51879653-4867-47f7-83ac-c84f7a771ea1)

顺序输出字符串中的字符：

![image](https://github.com/user-attachments/assets/1dd8ec6f-9784-4ece-8040-4065580ec503)

输出结果：

![image](https://github.com/user-attachments/assets/92b23fc3-8ebf-4537-af3c-eb888f8b3fb0)

## while循环
while循环格式为：

![image](https://github.com/user-attachments/assets/b8c9cfdf-7d37-4625-8f89-e608de935183)

示例：

![image](https://github.com/user-attachments/assets/8fd57587-97bd-42c6-a511-5e0861f38bd3)

运行脚本，输出：

![image](https://github.com/user-attachments/assets/7c3a60d5-e8b1-40dd-b8ae-152264a85c76)

while循环可用于读取键盘信息。下面的例子中，输入信息被设置为变量FILM，按Ctrl-D结束循环。

![image](https://github.com/user-attachments/assets/78e07e7c-0ddb-4bb1-a424-98ec88ce9441)

运行脚本，输出类似下面：

![image](https://github.com/user-attachments/assets/e5540163-03d8-4dd1-af2f-946dd5f62327)


## 无限循环
无限循环语法格式：

![image](https://github.com/user-attachments/assets/0357e9ff-1113-4b63-af65-6d2737acb7e4)

或者

![image](https://github.com/user-attachments/assets/e4a189fe-7498-4fb6-b271-e3b77ef6ec8b)

或者

![image](https://github.com/user-attachments/assets/b0764b9e-2afc-4652-92bd-45fd56f897b0)


## until 循环
until 循环执行一系列命令直至条件为 true 时停止。

until 循环与 while 循环在处理方式上刚好相反。

一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用。

until 语法格式:

![image](https://github.com/user-attachments/assets/e528cf98-ba18-43b6-b53b-d2fd85961a6a)

condition 一般为条件表达式，如果返回值为 false，则继续执行循环体内的语句，否则跳出循环。

以下实例我们使用 until 命令来输出 0 ~ 9 的数字：

![image](https://github.com/user-attachments/assets/cfd63bf3-a27d-461c-a030-1021bbf53d12)

运行结果：

输出结果为：

![image](https://github.com/user-attachments/assets/3010aecc-eea4-4294-a9e5-229831b1b5fc)


## case
Shell case语句为多选择语句。可以用case语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。case语句格式如下：

![image](https://github.com/user-attachments/assets/6e3c85b7-54ee-4054-be52-7bec014b2449)

下面的脚本提示输入1到4，与每一种模式进行匹配：

![image](https://github.com/user-attachments/assets/e5d75d36-6169-4c1a-83e5-5807ee8f5a56)

输入不同的内容，会有不同的结果，例如：

![image](https://github.com/user-attachments/assets/b5c7d6d7-6078-43f8-925a-b4cddc909beb)


## 跳出循环
在循环过程中，有时候需要在未达到循环结束条件时强制跳出循环，Shell使用两个命令来实现该功能：break和continue。

break命令允许跳出所有循环（终止执行后面的所有循环）。

下面的例子中，脚本进入死循环直至用户输入数字大于5。要跳出这个循环，返回到shell提示符下，需要使用break命令。

![image](https://github.com/user-attachments/assets/c4c26f3b-3f4c-4ed3-b67b-5e6c0eb97dd0)

执行以上代码，输出结果为：

![image](https://github.com/user-attachments/assets/da4d0ae9-b06a-4943-8ce9-f529a7ff9838)

continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。



# Shell输入/输出重定向
重定向命令列表如下：

![image](https://github.com/user-attachments/assets/b270c372-e21c-4732-9011-2a90eb2b3f4d)

## 输出重定向
重定向一般通过在命令间插入特定的符号来实现。特别的，这些符号的语法如下所示:

![image](https://github.com/user-attachments/assets/ff839005-68fe-4e36-83b9-03516a8a01a1)

上面这个命令执行command1然后将输出的内容存入file1。

注意任何file1内的已经存在的内容将被新内容替代。如果要将新内容添加在文件末尾，请使用>>操作符。

输出重定向会覆盖文件内容：

![image](https://github.com/user-attachments/assets/d5b5ff19-19c4-49a2-90f5-27e1cda6ae3b)

如果不希望文件内容被覆盖，可以使用 >> 追加到文件末尾，例如：

![image](https://github.com/user-attachments/assets/7c8c5afb-8db4-497f-b499-913d8cc8e41a)

## 输入重定向
和输出重定向一样，Unix 命令也可以从文件获取输入，语法为：

![image](https://github.com/user-attachments/assets/b064eb6c-7ab6-40e8-9d73-ce469b9f8eea)

这样，本来需要从键盘获取输入的命令会转移到文件读取内容。

注意：输出重定向是大于号(>)，输入重定向是小于号(<)。

统计 users 文件的行数,执行以下命令：

![image](https://github.com/user-attachments/assets/5d76ad6c-4003-4a5c-b801-58d4c72487fc)

也可以将输入重定向到 users 文件：

![image](https://github.com/user-attachments/assets/7fda8d1f-b68b-44c9-84c3-6c811f2cc25b)

注意：上面两个例子的结果不同：第一个例子，会输出文件名；第二个不会，因为它仅仅知道从标准输入读取内容。

同时替换输入和输出，执行command1，从文件infile读取内容，然后将输出写入到outfile中:

![image](https://github.com/user-attachments/assets/19dda201-7e82-4ca9-87f7-36fea3d32e2a)

## 重定向深入讲解
一般情况下，每个 Unix/Linux 命令运行时都会打开三个文件：

- 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。
- 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。
- 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。

默认情况下，command > file 将 stdout 重定向到 file，command < file 将stdin 重定向到 file。

如果希望 stderr 重定向到 file，可以这样写：

![image](https://github.com/user-attachments/assets/9b651344-e035-49b9-ad71-5d8ba01b549b)

如果希望 stderr 追加到 file 文件末尾，可以这样写：

![image](https://github.com/user-attachments/assets/ecae25eb-af4c-4d36-b99d-3b7ba611a0e8)

2 表示标准错误文件(stderr)。

如果希望将 stdout 和 stderr 合并后重定向到 file，可以这样写：

![image](https://github.com/user-attachments/assets/01230bfa-8ad3-47df-8cee-66a32b10cee2)

如果希望对 stdin 和 stdout 都重定向，可以这样写：

![image](https://github.com/user-attachments/assets/f2ad9eac-65fe-44fe-9946-1b2652c2024d)

command 命令将 stdin 重定向到 file1，将 stdout 重定向到 file2。

## Here Document
Here Document 是 Shell 中的一种特殊的重定向方式，用来将输入重定向到一个交互式 Shell 脚本或程序。

它的基本的形式如下：

![image](https://github.com/user-attachments/assets/31b1163f-f233-4c76-994a-c83a04b05383)

它的作用是将两个 delimiter 之间的内容(document) 作为输入传递给 command。

注意：结尾的delimiter 一定要顶格写，前面不能有任何字符，后面也不能有任何字符，包括空格和 tab 缩进。

在命令行中通过 wc -l 命令计算 Here Document 的行数：

![image](https://github.com/user-attachments/assets/9163dd47-677e-4907-82a2-bcbecc9c8c61)

## /dev/null 文件
如果希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null：

![image](https://github.com/user-attachments/assets/a41dce72-4ae4-4d01-ad37-2bcec954d0be)

/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果。

如果希望屏蔽 stdout 和 stderr，可以这样写：

![image](https://github.com/user-attachments/assets/32f23d16-cc93-49d8-9243-64d29d4c4d16)

0 是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。

# 实例
## 杨辉三角：

![image](https://github.com/user-attachments/assets/2e4779e9-8ae7-4af5-8695-bc9f71157b7b)

## sum()&max():

![image](https://github.com/user-attachments/assets/261df432-da4f-4fcb-bb16-07e3128c188e)

## 99乘法表：

![image](https://github.com/user-attachments/assets/4aea8236-423b-4a63-ac77-6ff930836b5c)

# 文本编辑命令
## cut命令

![image](https://github.com/user-attachments/assets/0de2c92a-aac1-45ed-8db1-a21b43c5b3e9)

cut以行为单位，根据分隔符把行分成若干列，这样就可以指定选取哪些列了。

![image](https://github.com/user-attachments/assets/13fe483b-116f-4377-86af-02e33d728732)

只显示/etc/passwd的用户和shell：

![image](https://github.com/user-attachments/assets/e9591d00-28ad-48d0-97bf-0cf4d322cf60)

## sed命令
sed 可依照脚本的指令来处理、编辑文本文件。

Sed 主要用来自动编辑一个或多个文件、简化对文件的反复操作、编写转换程序等。

语法:

![image](https://github.com/user-attachments/assets/1d2cea08-eabf-4771-94d5-62988b779c93)

**参数说明：**

- -e <script>以指定的script来处理输入的文本文件。
- -f<script文件>以指定的script文件来处理输入的文本文件。
- -n仅显示script处理后的结果，一般跟p动作搭配使用。
- -i使用处理后的结果修改文件。

**动作说明：**

- a：在指定行后面插入内容
- i：在指定行前面插入内容
- d：删除指定行
- c ：替换指定行
- p ：打印指定行的数据，通常需要跟-n选项搭配使用
- s ：替换指定字符，兼容vim的替换语法，例如 1,20s/old/new/g

## 元字符集
sed支持一般的正则表达式，下面是支持的正则语法：

![image](https://github.com/user-attachments/assets/8df55229-8298-4ea1-bd65-dfeae9f68608)

## a|i:在指定行位置添加行

![image](https://github.com/user-attachments/assets/51cee3f5-0592-4754-b4b1-74c890a472c2)

## d:删除指定行

![image](https://github.com/user-attachments/assets/89fb87ae-3a70-4fe6-bbd3-dc0c7dbbdc19)

## c:替换指定行

![image](https://github.com/user-attachments/assets/6f62167b-8899-4b9e-af21-92aca53ddf0c)

## p:仅显示指定行
不加-n选项时，除了输出匹配行，还同时会输出所有行，所以需要加-n选项。

仅列出 /etc/passwd 文件内的第 5-7 行：

![image](https://github.com/user-attachments/assets/0ba9c11c-06e3-43eb-b91b-38d306501bf7)

## s:字符串替换
语法：

![image](https://github.com/user-attachments/assets/d1def1d3-a294-4d36-84f3-b369d90a43e3)

## y:单字符替换
跟s一样也用于替换，不过s替换的是整体，y替换的是每一字母对应的单个字母

把data中的第一行至第三行中的a替换成A，b替换成B，c替换成C：

![image](https://github.com/user-attachments/assets/476a60eb-9c38-4e6d-b0e9-51511509e68a)

示例：

![image](https://github.com/user-attachments/assets/f635abda-a65f-4325-a86a-6616c438ab6b)

## hHgG模式空间&保持空间
h命令是将当前模式空间中内容覆盖至保持空间，H命令是将当前模式空间中的内容追加至保持空间

g命令是将当前保持空间中内容覆盖至模式空间，G命令是将当前保持空间中的内容追加至模式空间

模拟tac命令：

![image](https://github.com/user-attachments/assets/82db10ad-7ba0-4833-839d-79b4c75d59c4)

1!G第1行不 执行“G”命令，从第2行开始执行。

$!d，最后一行不删除（保留最后1行）

下图P表示模式空间，H代表保持空间：

![image](https://github.com/user-attachments/assets/ffa6a11b-46a2-4dad-8517-99bc0a1db067)

递增序列：

![image](https://github.com/user-attachments/assets/b02dc351-5cf4-4e4c-b969-bc5d6d9f6884)

## 多次指定-e选项进行多点编辑
删除/etc/passwd第三行到末尾的数据，并把bash替换为blueshell：

![image](https://github.com/user-attachments/assets/72060851-b831-4c72-9b09-593d4b8dcacd)

删除一个文件以#开头的行和空行：

![image](https://github.com/user-attachments/assets/1b50f7dc-9c7c-4741-b313-2547c5a39db3)

也可以通过;实现

![image](https://github.com/user-attachments/assets/b818ac1a-7cb4-4014-b5f5-f22f31daaa6f)

## 选项-i直接修改文件内容
默认情况下sed命令仅仅只是将处理结果显示在控制台，加-i选项则会修改文件内容。

将 regular_express.txt 内每一行结尾若为 . 则换成 !

![image](https://github.com/user-attachments/assets/d75de402-fbdb-4a7a-a726-f6ea90ad9111)


# awk命令
AWK是一种处理文本文件的语言，是一个强大的文本分析工具。

之所以叫AWK是因为其取了三位创始人 Alfred Aho，Peter Weinberger, 和 Brian Kernighan 的 Family Name 的首字符。

语法：


![image](https://github.com/user-attachments/assets/8266a330-dcf2-4866-9f4e-e908717a6ba4)

**选项参数说明：**

- -F fs or --field-separator fs 指定输入文件折分隔符，fs是一个字符串或者是一个正则表达式，如-F:。
- -v var=value or --asign var=value 赋值一个用户定义变量。
- -f scripfile or --file scriptfile 从脚本文件中读取awk命令。


## 基本用法

![image](https://github.com/user-attachments/assets/d17f20ba-bb7d-4721-9466-cd48bc8eaecd)

每行按空格或TAB分割，输出文本中的1、4列：

![image](https://github.com/user-attachments/assets/fd0e53fc-321a-4369-a272-86e31bd1ecf9)

格式化输出：

![image](https://github.com/user-attachments/assets/9bce1a5c-366b-4e31-a1bd-b764575961de)

### -F指定分割字符

![image](https://github.com/user-attachments/assets/317b641e-4e64-44cc-9c4b-6b2e5817b0ec)

使用:分割,取/etc/passwd文件每个用户对应shell：

![image](https://github.com/user-attachments/assets/421818e5-7938-48c3-b778-f1112174280c)

同时使用:和/l两个分隔符分割/etc/passwd文件

![image](https://github.com/user-attachments/assets/9de26665-f992-47f7-a05f-3db545feb7bb)

### -v设置变量

![image](https://github.com/user-attachments/assets/9b9fc489-85a2-4c95-8380-aed5c46b6c86)

例子：

![image](https://github.com/user-attachments/assets/bbf9e55b-2b8e-497b-bb6f-9a0dacd38aa6)

### -f指定awk脚本

![image](https://github.com/user-attachments/assets/c7bfeca9-a7c7-4149-b9a6-56b563f15663)

脚本模块：

- BEGIN{ 这里面放的是执行前的语句 }
- END {这里面放的是处理完所有的行后要执行的语句 }
- {这里面放的是处理每一行时要执行的语句}

假设有这么一个文件（学生成绩表）：

![image](https://github.com/user-attachments/assets/91e1bfc6-8d1f-4d68-a6ec-23daafae72d0)

awk脚本如下：

![image](https://github.com/user-attachments/assets/a3649333-2c03-4afe-a202-eb831dc00b00)

我们来看一下执行结果：

![image](https://github.com/user-attachments/assets/80bf68f7-c70f-48e3-9a32-1ae1608c46a9)

## AWK工作原理
AWK 工作流程可分为三个部分：

- 读输入文件之前执行的代码段（由BEGIN关键字标识）。
- 主循环执行输入文件的代码段。
- 读输入文件之后的代码段（由END关键字标识）。

命令结构:

![image](https://github.com/user-attachments/assets/413653ff-0186-4a43-a821-053e86ab1271)

下面的流程图描述出了 AWK 的工作流程：

![image](https://github.com/user-attachments/assets/0fc95774-098f-4bfe-84d4-74a372f7ff21)

- 1、通过关键字 BEGIN 执行 BEGIN 块的内容，即 BEGIN 后花括号 {} 的内容。
- 2、完成 BEGIN 块的执行，开始执行body块。
- 3、读入有 \n 换行符分割的记录。
- 4、将记录按指定的域分隔符划分域，填充域，$0 则表示所有域(即一行内容)，1 ∗ ∗ 表 示 第 一 个 域 ， ∗ ∗ 1** 表示第一个域，**1∗∗表示第一个域，∗∗n 表示第 n 个域。
- 5、依次执行各 BODY 块，pattern 部分匹配该行内容成功后，才会执行 awk-commands 的内容。
- 6、循环读取并执行各行直到文件结束，完成body块执行。
- 7、开始 END 块执行，END 块可以输出最终结果。

### 运算符

![image](https://github.com/user-attachments/assets/7908a9cf-9d1c-4760-b114-9583ebfa714e)

#### 过滤第一列大于2的行

![image](https://github.com/user-attachments/assets/2df412ea-e751-4721-accf-07fa974f1458)

#### 过滤第一列等于2的行

![image](https://github.com/user-attachments/assets/708a105f-6c80-4834-8222-91a0f3a68170)

#### 过滤第一列大于2并且第二列等于’Are’的行

![image](https://github.com/user-attachments/assets/a22083a4-d1b4-416a-a564-ad292f2449fd)

#### 内建变量

![image](https://github.com/user-attachments/assets/40e1705d-1e40-451c-bbea-dbda78ded917)

格式化变量说明：

- %s 输出字符串
- %i 输出整数
- %f 输出浮点数

%-5s 格式为左对齐且宽度为5的字符串代替（-表示左对齐），不使用则是又对齐。

%-4.2f 格式为左对齐宽度为4，保留两位小数。

```txt
python@ubuntu:~/test$ awk 'BEGIN{printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n","FILENAME","ARGC","FNR","FS","NF","NR","OFS","ORS","RS";printf "---------------------------------------------\n"} {printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n",FILENAME,ARGC,FNR,FS,NF,NR,OFS,ORS,RS}'  log.txt
FILENAME ARGC  FNR   FS   NF   NR  OFS  ORS   RS
---------------------------------------------
log.txt    2    1         5    1         
log.txt    2    2         5    2         
log.txt    2    3         3    3          
log.txt    2    4         4    4         

python@ubuntu:~/test$ awk -F: 'BEGIN{printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n","FILENAME","ARGC","FNR","FS","NF","NR","OFS","ORS","RS";printf "---------------------------------------------\n"} {printf "%4s %4s %4s %4s %4s %4s %4s %4s %4s\n",FILENAME,ARGC,FNR,FS,NF,NR,OFS,ORS,RS}'  log.txt
FILENAME ARGC  FNR   FS   NF   NR  OFS  ORS   RS
---------------------------------------------
log.txt    2    1    :    1    1         
log.txt    2    2    :    1    2         
log.txt    2    3    :    1    3         
log.txt    2    4    :    1    4    
```

#### 输出顺序号 NR, 匹配文本行号

![image](https://github.com/user-attachments/assets/00a3ea9f-a0c3-4392-9980-6f7dc6dffb2b)

#### 指定输出分割符

![image](https://github.com/user-attachments/assets/f816f0a3-da1c-4bad-bd90-e278a53e66e7)

#### 忽略大小写

![image](https://github.com/user-attachments/assets/a4b277e1-9857-40b4-bd72-f3324680ade6)

## 正则字符串匹配
#### ~ 表示模式开始。// 中是模式。

输出第二列包含 “th”，并打印第二列与第四列：

![image](https://github.com/user-attachments/assets/5f2a62bf-3288-420c-bf35-703dc6dc8164)

输出包含"re"的行：

![image](https://github.com/user-attachments/assets/047ef2ec-7428-4dc9-b218-8c05104c231b)

**!表示取反**

输出第二列不包含 “th”，并打印第二列与第四列：

![image](https://github.com/user-attachments/assets/56e79daf-31cb-4a63-9ef7-fb93186e906d)

输出不包含"re"的行：

![image](https://github.com/user-attachments/assets/7286b335-e1da-4d0c-8d5f-67c9965e70f0)


## 一些实例
#### 计算文件大小

![image](https://github.com/user-attachments/assets/c8777d7a-6faf-45e2-9bb8-63782ca5dbf7)

#### 从文件中找出长度大于80的行

![image](https://github.com/user-attachments/assets/58c2fe38-2251-4457-bae7-dd6bd044d86b)

#### 打印九九乘法表

![image](https://github.com/user-attachments/assets/33e11241-62a6-4bba-9492-598f1cce3a0f)

#### 访问日志分析

日志格式

```txt
python@ubuntu:~/test$ head access.log -n1
42.236.10.75 "changtou.xiaoxiaoming.xyz" [14/Oct/2019:12:47:18 +0800] "GET /logo/8@3x.png HTTP/1.1" 200 26053 "https://changtou.xiaoxiaoming.xyz/" "Mozilla/5.0 (Linux; U; Android 8.1.0; zh-CN; EML-AL00 Build/HUAWEIEML-AL00) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/57.0.2987.108 baidu.sogo.uc.UCBrowser/11.9.4.974 UWS/2.13.1.48 Mobile Safari/537.36 AliApp(DingTalk/4.5.11) com.alibaba.android.rimet/10487439 Channel/227200 language/zh-CN" "42.236.10.75" rt="0.000" uct="-" uht="-" urt="-"
```

示例：

![image](https://github.com/user-attachments/assets/132fb03e-aeb8-481f-a9e9-55e1fb2b2ce7)


# awk编程
## 条件语句IF&ELSE
IF 条件语句语法格式如下：

![image](https://github.com/user-attachments/assets/e1d1682c-9888-4965-95ab-2d8e4ba042f3)

也可以使用花括号来执行一组操作：

![image](https://github.com/user-attachments/assets/d365bf7f-0f0c-4e0f-972f-b3ae3dc4f122)

判断数字是奇数还是偶数：

![image](https://github.com/user-attachments/assets/9f5dc8d6-0b93-4324-a5e9-885691c8617e)

IF - ELSE 条件语句语法格式如下：

![image](https://github.com/user-attachments/assets/329e9baa-0059-4c71-ba41-630bbd850bdf)

在条件语句 condition 为 true 时只需 action-1，否则执行 action-2。

```txt
python@ubuntu:~/test$ awk 'BEGIN {
>     num = 11; 
>     if (num % 2 == 0) printf "%d 是偶数\n", num; 
>     else printf "%d 是奇数\n", num 
> }'
11 是奇数
python@ubuntu:~/test$ awk 'BEGIN {num = 11; if (num % 2 == 0) printf "%d 是偶数\n", num; else printf "%d 是奇数\n", num }'
11 是奇数
```

可以创建多个 IF - ELSE 格式的判断语句来实现多个条件的判断：

![image](https://github.com/user-attachments/assets/3bc68297-83dc-49c1-b782-b55ef8c1eb8d)

输出结果：

![image](https://github.com/user-attachments/assets/7b19e21a-f3b5-4521-9cee-78835a087144)

## 循环语句For&While
For 循环的语法如下：

![image](https://github.com/user-attachments/assets/1d16e22b-a6ee-4998-9009-26a5439d8253)

下面的例子使用 For 循环输出数字 1 至 5：

![image](https://github.com/user-attachments/assets/359a5694-2eaf-490a-be3c-3d5d402298d3)

While 循环的语法如下：

![image](https://github.com/user-attachments/assets/13950dab-d9db-4c64-a3f1-2959bdac9152)

下面是使用 While 循环输出数字 1 到 5 的例子：

![image](https://github.com/user-attachments/assets/f3aa9469-bcfc-4e28-84c8-1db61e4d76a8)

在下面的示例子中，当计算的和大于 50 的时候使用 break 结束循环：

![image](https://github.com/user-attachments/assets/c1a685f9-10b7-4e33-89ba-c1b038b415bd)

输出结果为：

![image](https://github.com/user-attachments/assets/4126a99c-d5aa-4ea7-9767-f0382f70adc1)

Continue 语句用于在循环体内部结束本次循环，从而直接进入下一次循环迭代。

下面的例子输出 1 到 20 之间的偶数：

![image](https://github.com/user-attachments/assets/4d5ae24b-1f8b-482a-96b9-3ede669e8d62)

Exit 用于结束脚本程序的执行。

该函数接受一个整数作为参数表示 AWK 进程结束状态。 如果没有提供该参数，其默认状态为 0。

下面例子中当和大于 50 时结束 AWK 程序。

![image](https://github.com/user-attachments/assets/6620ac86-0823-4ff6-adc4-de11e6b89a90)

输出结果为：

![image](https://github.com/user-attachments/assets/f2e245f4-b95a-4c8a-b276-20ef464717e3)

## awk数组
AWK的数组底层数据结构是散列表，索引可以是数字或字符串。

数组使用的语法格式：

![image](https://github.com/user-attachments/assets/61e434e9-615b-47fd-8dca-544e936a7c0d)

创建数组并访问数组元素：

![image](https://github.com/user-attachments/assets/ac96fda4-a6a7-4b82-8e18-b671a537742d)

删除数组元素语法格式：

![image](https://github.com/user-attachments/assets/49f1bccf-3c69-423e-81cb-9acf280ddbce)

下面的例子中，数组中的 google 元素被删除（删除命令没有输出）：

![image](https://github.com/user-attachments/assets/eafd3cbf-75d8-4512-a85b-c58108ebc668)

AWK 本身不支持多维数组，不过我们可以很容易地使用一维数组模拟实现多维数组。

如下示例为一个 3x3 的三维数组：

![image](https://github.com/user-attachments/assets/bcade7ed-f51f-46f3-a19a-6b6f034c15dc)

以上实例中，array[0][0] 存储 100，array[0][1] 存储 200 ，依次类推。为了在 array[0][0] 处存储 100, 可以使用字符串0,0 作为索引： array[“0,0”] = 100。

下面是模拟二维数组的例子：

![image](https://github.com/user-attachments/assets/944dd71d-e52c-472c-9321-49ac63782cc9)

执行上面的命令可以得到如下结果：

![image](https://github.com/user-attachments/assets/24065000-038d-448e-ba7b-724a496d08c3)

在数组上可以执行很多操作，比如，使用 asort 完成数组元素的排序，或者使用 asorti 实现数组索引的排序等等。

## AWK 用户自定义函数
自定义函数的语法格式为：

![image](https://github.com/user-attachments/assets/1622b929-843c-46c6-8fd4-b07a3f7150f2)

以下实例实现了两个简单函数，它们分别返回两个数值中的最小值和最大值。

文件 functions.awk 代码如下：

![image](https://github.com/user-attachments/assets/9aa3fc92-f586-4495-86dc-4af4934d8f20)

执行 functions.awk 文件，可以得到如下的结果：

![image](https://github.com/user-attachments/assets/72c79d7f-b401-407a-8265-e78f7e94e77d)

## AWK 内置函数
AWK 内置函数主要有以下几种：

- 算数函数
- 字符串函数
- 时间函数
- 位操作函数
- 其它函数

## 算数函数

![image](https://github.com/user-attachments/assets/0eeaf24b-b3b8-4408-bf6c-7e6ec15d1d5f)

## 字符串函数

![image](https://github.com/user-attachments/assets/906e9c56-1a2c-4d6c-a10a-8fa0d630470c)

**注：**Ere 部分可以是正则表达式。

#### 1、gsub、sub 使用

![image](https://github.com/user-attachments/assets/14d8c156-d933-40c7-867c-7ba3c0d940cb)

#### 2、查找字符串（index 使用）

使用了三元运算符: **表达式 ? 动作1 : 动作2**

![image](https://github.com/user-attachments/assets/5144215e-5ebf-45b8-8f5c-5def9b9ae598)

#### 3、正则表达式匹配查找(match 使用）

![image](https://github.com/user-attachments/assets/c06f16db-f676-4166-9e33-b63ab15a853c)

#### 4、截取字符串(substr使用）

从第 4 个 字符开始，截取 10 个长度字符串。

![image](https://github.com/user-attachments/assets/274ab448-9719-4007-af59-63dfa31b1b65)

#### 5、字符串分割（split使用）

![image](https://github.com/user-attachments/assets/20089ff7-07d6-40bd-b561-7b6f9cf0ba98)

分割 info，将 info 字符串使用空格切分为动态数组 tA。注意 awk for …in 循环，是一个无序的循环。 并不是从数组下标 1…n ，因此使用时候需要特别注意。

## 时间函数

![image](https://github.com/user-attachments/assets/8279e54f-5c9c-4eb8-b484-d8e97d1f2c52)

strftime 日期和时间格式说明符:

![image](https://github.com/user-attachments/assets/fcb3e3f5-7c99-480a-ba00-d399b66e1513)

## 位操作函数

![image](https://github.com/user-attachments/assets/3f36316d-44df-4dbb-9d13-bffbacd68c2f)

## 其他函数

![image](https://github.com/user-attachments/assets/013f4b71-59e6-4d2d-beeb-ee7935d3562b)


# vim全套笔记
## VIM快速复习
### 什么是 vim？
Vim是从 vi 发展出来的一个文本编辑器。代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。vim 的官方网站 (http://www.vim.org)

vim 键盘图：

![image](https://github.com/user-attachments/assets/b31821ca-cfec-4e15-b24d-4e18face99d3)

基本上vi可以分为三种状态：

- 命令模式（command mode)
- 插入模式（Insert mode)
- 底行模式（last line mode)

## 按:冒号即可进入last line mode

![image](https://github.com/user-attachments/assets/d77e1061-9253-4ec3-9180-4af3606b26d0)

## 从command mode进入Insert mode
按i在当前位置编辑

按a在当前位置的下一个字符编辑

按o插入新行，从行首开始编辑

按R(Replace mode)：R会一直取代光标所在的文字，直到按下 ESC为止；(常用)

## 按ESC键退回command mode
h←j↓k↑l→前面加数字移动指定的行数或字符数

1、翻页bu上下整页，ud上下半页

![image](https://github.com/user-attachments/assets/6ce7a6ad-b42c-4d0b-aa77-913cb0c92918)

2、行定位

![image](https://github.com/user-attachments/assets/158a4680-d69a-4184-96ba-b8276edf6ef9)

3、当前行定位

![image](https://github.com/user-attachments/assets/0b893dab-9cc8-415b-aac9-8d212a83ade6)

4、编辑

![image](https://github.com/user-attachments/assets/ed35568e-c5a4-43c8-ae24-fb047d81141f)

## 多行编辑，vim支持，vi不支持
按ctrl+V进入块模式，上下键选中快，按大写G选择到末尾，上下左右键移动选择位置

按大写I进去编辑模式，输入要插入的字符，编辑完成按ESC退出

选中要替换的字符后，按c键全部会删除，然后输入要插入的字符，编辑完成按ESC退出

选中要替删除的字符后，按delete键，则会全部删除

按shift+V可进入行模式，对指定行操作


## vim练习
1、创建目录/tmp/test，将/etc/man.config复制到该目录下

![image](https://github.com/user-attachments/assets/ed480a6a-9867-43f1-942e-8ceeaa8fea80)

2、用vim编辑man.config文件：

![image](https://github.com/user-attachments/assets/29b99bd3-a86f-44c3-881d-2bb272adab71)

3、设置显示行号； 移动到第58行，向右移动40个字符，查看双引号内的是什么目录；

![image](https://github.com/user-attachments/assets/a4f53d74-8a36-4493-90d7-3f98c81a0d02)

4、移动到第一行，并向下查找“bzip2”这个字符串，它在第几行；

![image](https://github.com/user-attachments/assets/05ef77cc-13d7-4711-bcc1-a25265a396aa)

5、将50行到100行之间的man更改为MAN，并且 逐个挑选 是否需要修改；

![image](https://github.com/user-attachments/assets/9531ea83-de3f-4a63-9bcd-8c60ff76c684)

6、修改完后，突然反悔了，要全部复原，有哪些方法？

![image](https://github.com/user-attachments/assets/abe4ca8a-2c20-48e3-bc8c-cfb2fad63f11)

7、复制65到73这9行的内容（含有MANPATH_MAP），并且粘贴到最后一行之后；

![image](https://github.com/user-attachments/assets/d7c53d7f-3a04-4f94-9ad7-64b96bbb33e9)

8、21行到42行之间开头为#符号的批注数据不要了，如何删除；

![image](https://github.com/user-attachments/assets/2b06eb64-3758-4930-8f0d-ae6500ec884c)

9、将这个文件另存为man.test.config的文件

![image](https://github.com/user-attachments/assets/4a302383-da01-40e8-a89c-c5b25909f47c)

10、到第27行，并且删除15个字符，结果出现的第一个字符是什么？

![image](https://github.com/user-attachments/assets/78330195-2dc8-4b52-bfbe-2e01adb50dae)

11、在第一行新增一行，在该行内输入“I am a student ”

![image](https://github.com/user-attachments/assets/71b26636-7ebb-476f-b4f8-a16472163234)

12、保存并退出

![image](https://github.com/user-attachments/assets/a3daf209-dd57-4d02-87e3-e14b66abaf1e)

## vi/vim的三种模式
vi/vim主要分为三种模式，分别是**命令模式（Command mode），输入模式（Insert mode）和底线命令模式（Last line mode）。**

![image](https://github.com/user-attachments/assets/acecafd0-0aa0-421c-8114-52c5efa44290)

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

![image](https://github.com/user-attachments/assets/ac70fb16-8807-4bc3-8b1b-c02fbdaad683)

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

![image](https://github.com/user-attachments/assets/4e42c2a6-defb-489d-8a0b-159b1de13bae)

### 删除操作

![image](https://github.com/user-attachments/assets/4e0ce449-374b-40ed-b87b-a7811dc8a7ed)

### 撤销&复原&重复

![image](https://github.com/user-attachments/assets/aa823548-5aae-4e8c-ada8-83c15c6589e6)

### 复制&粘贴

![image](https://github.com/user-attachments/assets/477dc1b5-c811-4730-bd64-621715641732)

### 合成行
- J: 将光标所在行与下一行的数据结合成同一行

### 搜索

![image](https://github.com/user-attachments/assets/a8a1829d-c0bc-48b3-9d49-86f0e1f9a0cc)

### 替换

![image](https://github.com/user-attachments/assets/3424f1f9-ee3a-4fd1-9ac6-d132d7b4cde2)

## 底行命令模式的常用操作

![image](https://github.com/user-attachments/assets/4236dd7b-54df-43c9-9fb8-4123f3aca908)

示例：

![image](https://github.com/user-attachments/assets/06489d4d-ec71-457f-badd-9f79dd1349a0)

## 可视模式
v 进入字符可视化模式： 文本选择是以字符为单位的。

V 进入行可视化模式： 文本选择是以行为单位的。

Ctrl+v 进入块可视化模式 ： 选择一个矩形内的文本。

可视模式下可进行如下操作：

![image](https://github.com/user-attachments/assets/e3e96f25-787e-48fa-bcf7-fa5be341a5a5)

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

![image](https://github.com/user-attachments/assets/2d7a0c0a-2fd8-49e7-a3f1-7accef8a6e7f)


## 启动初始化进程init
内核文件加载以后，就开始运行第一个程序 /sbin/init，它的作用是初始化系统环境。

init程序首先是需要读取配置文件/etc/inittab。

![image](https://github.com/user-attachments/assets/a5e3c788-6794-4d08-a640-be1bdb37f93c)

![image](https://github.com/user-attachments/assets/562926fe-466f-4cbf-a41c-eeea4e588b87)

由于init是第一个运行的程序，它的进程编号（pid）就是1。其他所有进程都从它衍生，都是它的子进程。

## 确定运行级别
许多程序需要开机启动。它们在Windows叫做"服务"（service），在Linux就叫做"守护进程"（daemon）。

init进程的一大任务，就是去运行这些开机启动的程序。

但是，不同的场合需要启动不同的程序，比如用作服务器时，需要启动Apache，用作桌面就不需要。

Linux允许为不同的场合，分配不同的开机启动程序，这就叫做"运行级别"（runlevel）。也就是说，启动时根据"运行级别"，确定要运行哪些程序。

![image](https://github.com/user-attachments/assets/64ca0d95-eda3-40af-a7c7-3216aeecf95c)

Linux系统有7个运行级别(runlevel)：

- 运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动
- 运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登陆
- 运行级别2：多用户状态(没有NFS)
- 运行级别3：完全的多用户状态(有NFS)，登陆后进入控制台命令行模式
- 运行级别4：系统未使用，保留
- 运行级别5：X11控制台，登陆后进入图形GUI模式
- 运行级别6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动

可以使用运行级别执行关机或重启：

![image](https://github.com/user-attachments/assets/62d13274-8fd1-4cde-b53f-7146225f9ffa)

## 加载开机启动程序
在init的配置文件中有这么一行： si::sysinit:/etc/rc.d/rc.sysinit它调用执行了/etc/rc.d/rc.sysinit，而rc.sysinit是一个bash shell的脚本，它主要是完成一些系统初始化的工作，rc.sysinit是每一个运行级别都要首先运行的重要脚本。

它主要完成的工作有：激活交换分区，检查磁盘，加载硬件模块以及其它一些需要优先执行任务。

![image](https://github.com/user-attachments/assets/d87d8a64-c283-46bf-b196-7aa350537157)

这一行表示以5为参数运行/etc/rc.d/rc，/etc/rc.d/rc是一个Shell脚本，它接受5作为参数，去执行/etc/rc.d/rc5.d/目录下的所有的rc启动脚本，/etc/rc.d/rc5.d/目录中的这些启动脚本实际上都是一些连接文件，而不是真正的rc启动脚本，真正的rc启动脚本实际上都是放在/etc/rc.d/init.d/目录下。

而这些rc启动脚本有着类似的用法，它们一般能接受start、stop、restart、status等参数。

/etc/rc.d/rc5.d/中的rc启动脚本通常是K或S开头的连接文件，对于以 S 开头的启动脚本，将以start参数来运行。

而如果发现存在相应的脚本也存在K打头的连接，而且已经处于运行态了(以/var/lock/subsys/下的文件作为标志)，则将首先以stop为参数停止这些已经启动了的守护进程，然后再重新运行。

这样做是为了保证是当init改变运行级别时，所有相关的守护进程都将重启。

至于在每个运行级中将运行哪些守护进程，用户可以通过chkconfig或setup中的"System Services"来自行设定。

![image](https://github.com/user-attachments/assets/9ce76cdc-5c57-4750-8a2a-89c58818ae0b)

## 用户登录
一般来说，用户的登录方式有三种：

- （1）命令行登录
- （2）ssh登录
- （3）图形界面登录

![image](https://github.com/user-attachments/assets/3ae0ba6b-1a6e-4c4c-bbef-ed8b7665fe18)

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

![image](https://github.com/user-attachments/assets/3499397a-c708-4ad8-9139-1e82e6116f8e)

shell，简单说就是命令行界面，让用户可以直接与操作系统对话。用户登录时打开的shell，就叫做login shell。

（1）命令行登录：首先读入 /etc/profile，这是对所有用户都有效的配置；然后依次寻找下面三个文件，这是针对当前用户的配置。

![image](https://github.com/user-attachments/assets/be9338bf-2167-4a3c-a89a-32b782770aa2)

需要注意的是，这三个文件只要有一个存在，就不再读入后面的文件了。比如，要是 ~/.bash_profile 存在，就不会再读入后面两个文件了。

（2）ssh登录：与第一种情况完全相同。

（3）图形界面登录：只加载 /etc/profile 和 /.profile。也就是说，/.bash_profile 不管有没有，都不会运行。

## Linux关机

![image](https://github.com/user-attachments/assets/748da12c-5ac5-40ac-8e50-8992cfafdae8)

最后总结一下，不管是重启系统还是关闭系统，首先要运行**sync**命令，把内存中的数据写到磁盘中。

关机的命令有 **shutdown –h now halt poweroff 和 init 0** , 重启系统的命令有 **shutdown –r now reboot init 6。**

# 计算机启动的流程

![image](https://github.com/user-attachments/assets/13692316-a2b5-4acd-a1fe-b280b2fd83c6)

boot是bootstrap（鞋带）的缩写，它来自一句谚语：

![image](https://github.com/user-attachments/assets/2e58a020-bc74-4675-8634-64326d7b330b)

字面意思是"拽着鞋带把自己拉起来"，这当然是不可能的事情。最早的时候，工程师们用它来比喻，计算机启动是一个很矛盾的过程：必须先运行程序，然后计算机才能启动，但是计算机不启动就无法运行程序！

早期真的是这样，必须想尽各种办法，把一小段程序装进内存，然后计算机才能正常运行。所以，工程师们把这个过程叫做"拉鞋带"，久而久之就简称为boot了。

计算机的整个启动过程分成四个阶段。
