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
