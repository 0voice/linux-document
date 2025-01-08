原文地址：https://mp.weixin.qq.com/s/3ox5JSC80_2eOMV60Hxtfw





# awk：强大的文本分析工具



![图片](https://mmbiz.qpic.cn/mmbiz_gif/ibj9nANUc6z74QqKQCcRGEhFTHhfr5A1sViar95KE8EmSobNxbBjW0h8GEsK9mo1Y2IsmpkqGEqBQUCe4mNDc2Dg/640?wx_fmt=gif&tp=wxpic&wxfrom=5&wx_lazy=1)



awk是一个强大的文本分析工具，相对于grep的查找，sed的编辑，awk在其对数据分析并生成报告时，显得尤为强大。简单来说awk就是把文件逐行的读入，以空格或tab为默认分隔符将每行切片，切开的部分再进行各种分析处理。awk可以处理文件数据，或者来自前个命令的标准输入内容，awk的一般使用规则如下：

```
awk -Ffv 'BEGIN{} //条件{动作1;动作2} END {}' 文件或标准输入
```

大参数：参数-F指定分隔符，-f调用脚本，-v定义变量；

BEGIN 初始化代码块，在对每一行进行处理之前，初始化代码，主要是引用全局变量，设置FS分隔符

// 匹配代模块，可以是字符串或正则表达式

{} 命令代模块，包含一条或多条命令

； 多条命令使用分号分隔

END 结尾代码块，在对每一行进行处理之后再执行的代码块，主要是进行最终计算或输出结尾摘要信息

### 01数据内容选取





我们可以使用匹配模块搭配正则表达式选取行：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNEeGCgf1O4iaUzmAg7bfUxo5jAIv9yv1icZUBXR1F1lLHxk8Wl1pRzgrw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其中匹配内容里面可以使用bash变量，但是必须用加单引号，如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNzphEYAKu87aBQCvuaO3vuwu6PZiaHtJ8ODNpia6ibNmiboib6Omz1rOSib0g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

我们也可以根据分隔符选取字段，例如使用last列出最后五行登陆者信息，并使用awk中print命令选取账户名及其IP信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNVm2lWrSu9DIpb13dnE2xso8fS7x43XXwn7Bwfldkvia9icS7eQViaMVEw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其中“\t”表示分隔符为tab，注意这里是打印内容的分隔符，而不是划分域的分隔符，可以换成其他符号甚至是任意字符串（包括数据）均可：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNWiaOfdhJC5QN4yJyQYpPCoSuibwdvVuhTBSjZfPPy6afAJpbXAvT1qyA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

最后一行是时间信息，中间隔着一行空行，如要是进一步只选取账户和IP可以使用sed命令：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNPxOcRsQs2aRWzfHOCLDKRP2SEqEzqm4BPLB0SNncnBJwTaa9gb8JGw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

由以上例子可以看出awk工作流程：读入有'\n'换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域，$0则表示所有域，$1表示第一个域，$n表示第n个域。默认域分隔符是空格键或[tab]键，所以$1表示登录用户，$3表示登录用户IP，也即awk是以行为一次处理单位，域（字段）为最小的处理单元。

可以使用-F强制制定其他划分域的分隔符，多个分隔符使用[]括起来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNGcCJqfv2QvLAvXMmBwfgKh4PFNgknZXVibdbnzbiaYxw66saSgHhFfcA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这里需要注意"/:"和"[/:]"的不同。这个功能在处理物种分类信息的时候非常有用，例如多样性分析中otutable的物种注释信息各个水平堆叠在一起，不利于作图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNEkHLeMr2XhaLoJfOQPrYdT8PjfKsiaPAueNYjPGsR3Mr6ne47oqiaj5Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

我们可以从中选取科水平的注释结果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LN1HxwolKuck0PLzI3I1MKkrD797nakRIsXia2uDSlymyuicLyvMZpria5Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

提取的结果可以保存到文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNoL7l5SuATpghYLuGa2ebIywf0pq1FtluQqJjkZLSHMPggIpM5XLLEQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

保存的文件可以安行和原来的otu table进行合并（使用paste命令）。

### 02内置变量




awk有许多内置变量用来设置环境信息，这些变量可以被改变，下面给出了最常用的一些变量：

ENVIRON 支持队列中系统环境变量的使用

FILENAME awk浏览的文件名，对于批量处理文件很有用

FNR 浏览文件的次数，一般与NR相同，**大于****NR****处理多个文件**

FS 设置输入域分隔符，等价于命令行-F选项

NF 浏览记录的域的个数

NR  已读的记录数，**可以指定处理某一行**

OFS 输出域分隔符

ORS 输出记录分隔符

RS 控制记录分隔符

下面我们利用内置变量来处理数据信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LN25ibgsATp4mgHavicptD1pBtQ56iav68Hibbc92kL3leZjdafFuxu6k45Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

在上面例子中，我们使用内置变量显示了行号以及每一行的字段数目。

### 03条件运算符



awk的命令间也可以使用条件运算符设置条件类型，使得命令选择性执行，常见的有大于>、小于<、大于等于>=、小于等于<=、等于==、不等于!=、匹配~、不匹配!~。下面我们以/etc/passwd文件为例，这个文件每一行字段之间以“：”分割，如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LN0WK8Fz7EUkMdkBWich7icdYfNQYDlqMkEtbT1p4MarOXNjbjX8Dsg5kg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

接下来我们选取第三个字段也即UID大于500小于600的数据行，并且列出每行第一字段账号和第三字段UID：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNAXkiafHNNuIA5TN20r7kCKldWxRYo2B6Ut0zcBic19zvY4UMGvtLxEqQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以发现，条件类型里还可以使用逻辑连接符。awk的这种数据筛选功能也非常有用，例如可以用来筛选高丰度的物种或者基因。

### 04AWK编程





awk的条件类型决定着动作命令的执行，其条件语句可以通过变量以及判断语句进行编程实现，还可以搭配正则表达式。

除了awk自定义的变量，用户可以根据需要自定义变量，例如我们可以通过自定义变量计算文件的行数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNxwicRKCex3EnDbDo8lBksmbl3flicmvH5dTfpZXSKcP8vviaAk0DgPczQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

在这里count=count+1可以简写为count+=1，或者count++，同理每次加2则表示为count+=2。上面命令的另一种写法为：

```
awk 'BEGIN{count=0} {count=count+1} END{print "user count is ", count}' /etc/passwd
```



awk同样可使用if控制结构，例如前面计算序列总数的命令使用if结构如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LNgBQgKcia1Sf95qCe5Jxx0sibibJHoYhxxHd0ZcDyNumiaChTCuFeD0VnVg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

要注意if() {} else {}是一个完整的结构，要放在一个花括号内。

awk同样可以引入数组以及for结构。awk中的数组下标**可以是数字和字母**，数组的下标通常被称为关键字(key)。下面通过两个例子比较说明：

```
①awk -F ':' 'BEGIN{count=1} {name[count]=$1;count++} END{for (i=1; i<=NR; i++) print i, name[i]}' /etc/passwd②last -n 100 | sed -n '1,100p' | awk '{a[$1]++} END{for (i in a) print i,"\t", a[i]}'
```

第一个例子中，定义了name[count]数组，for为迭代循环，因为数组的下标是从1开始的整数，通过迭代打印出对应的下标以及数组内容。第二个例子中定义了关联数组a[$1]（参照Perl语言中的哈希），其下标是key（既可能是数字也可能是字母，没有规则）不需要定义初值，通过for循环结构打印出结果。a[$1]++实质为计算$1中字符串的出现的次数，也即统计重复字符数，这里为统计最近100次登录里每个账号的登陆次数。需要注意的是，awk是通过一行行不断浏览文件的方法来执行命令，因此NR也是不断变化的，但是END后面的模块中NR为最后一次浏览完的数据。运行结果如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LN1vWEuBFG6hHicmXjKTmPICUxxcicPSkGfFRFxTGKe4Pibb5v9gy4OXIQA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z5Bia0Hlzg5x7yNHU8vye3LN2MYRSZqnlb8licTZrZdT0qAun2geNW4IicIHCibVjib0g1uTbf59COhWIA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

