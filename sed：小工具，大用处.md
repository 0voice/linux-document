原文地址：https://mp.weixin.qq.com/s/9rKG1HcryZTzzgmHeOXQKw





# sed：小工具，大用处



![图片](https://mmbiz.qpic.cn/mmbiz_gif/ibj9nANUc6z74QqKQCcRGEhFTHhfr5A1sViar95KE8EmSobNxbBjW0h8GEsK9mo1Y2IsmpkqGEqBQUCe4mNDc2Dg/640?wx_fmt=gif&tp=wxpic&wxfrom=5&wx_lazy=1)

在学习工作中发现，在Linux中除了ll、ls、less等查看命令，sed与awk是使用最为频繁的文本编辑命令，这两个工具可以使用最简单的方法完成复杂多样的编辑任务，因此接下来将依次为大家介绍这两个工具的使用。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/ibj9nANUc6z74QqKQCcRGEhFTHhfr5A1sWcyAwCULico6r5np4ue18U8Yr4yq3aOC3MShw8IELKcyMcia1XbvtWBw/640?wx_fmt=gif&tp=wxpic&wxfrom=5&wx_lazy=1)



![图片](https://mmbiz.qpic.cn/mmbiz_jpg/ibj9nANUc6z74QqKQCcRGEhFTHhfr5A1sEIafuOrcjSSUxru2xUpc1BCu5A5RUpHiahA1JBxWFPviabibZVnPHRG3Q/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



管道命令sed是一个很好的文本处理工具，主要以行为单位进行处理，可以将数据进行替换、删除、新增、选取等。sed可以处理标准输入内容或者文件，可以输出标准输出或输出到文件。sed的一般使用规则如下：

```
sed -nefri '动作命令' 文件或输入
```

参数设置：

-n：使用安静(silent)模式。在一般sed的用法中，所有来自STDIN的资料一般都会被列出到屏幕上。但如果加上-n参数后，则只有经过sed特殊处理的那一行(或者动作)才会被列出来。

-e：直接在命令行模式上进行sed的动作编辑；

-f：直接将sed的动作命令写在一个档案内，-ffilename则可以执行filename内的sed动作；

-r：sed动作支持的是拓展正规表示法的语法（默认基础正规表示法语法）。

-i：直接修改读取的档案内容，而不是由屏幕输出。

动作命令：

a：新增，a后可以接字串，这些字串会在新一行出现（目前的下一行）；

c：替换，c的后面可以接字串，这些字串可以取代n1、n2之间的行！

d：删除，因为是删除啊，所以d 后面通常不接任何东西；

g：全局，表示动作命令在行内全局执行，也即如果行内有多个关键字，全部删除或替换；

i：新增，i后可以接字串，这些字串会在新一行出现（目前的上一行）；

p：打印，亦即将某个选择的资料印出，通常p会与参数sed-n一起运行；

s：替换，可以直接进行替换的工作，通常s的动作可以搭配正则表达式。

### ⑴新增与删除功能

sed可以以行为单位按照行号进行删除，例如列出文件内容打印行号并删除第2-5行：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGaDwf6y2bQpyt1RQxewq9kQibcvT5t88ia04snuDuMXnMAicmHGK1CFasg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到标准输出的内容少了2-5行，最后一行可以使用“$”代指。这里省略了-e，也即默认就是在命令行模式，还可以根据关键字进行删除，例如删除含有“CHEN”的行：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeG7NBs9zTtwfuEj1eItzhHHo5ymWSbWwiaHKdh8hW64uF5JUmvMWr2ATw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

但是这时文件的内容并没有被更改，如要是删除原文件的内容并保存，可以使用-i参数直接对文件执行命令：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGogup9gtSvMzm9Vtgw0qJktvmdwwNC0aicAsNTPtjPKwkc822Cqs5p2g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

注意这时候虽然前三行被删去，行号仍是第一行开始，因为这里nl处理的是文件而不是标准输出内容。接下来我们新增新行内容，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGY6LuHYgQmSv9FYiacZJNFXv2gQ7KGDwb3RPYUlOIHc7M2aibIq5WnSlg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGy3lX9JXk7ozibANUwTMP4oWqqdyuWiaES7IZ7eOjUCH9mCdBvP0LXfrA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这时很明显的看出两个新增命令a和i的区别。可以使用“\+回车”来增添多行内容，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGqtpasOyliaoMqNXfGp7A0B6tWibiaGlfOWpY5vH9ibnCVmiaeJWqUBe8lmg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

### ⑵替换与显示功能

sed中的动作命令p可以根据行号显示内容，例如选择显示文件中的第5-7行内容：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGHkYPTIECKtia6565Qb2N2peWbbmhkAU5KgvJPpjLox2r7FNibkjmaGQg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

sed中的动作命令c可以进行整行内容替换，例如将文件第2-4行重复内容替换为“reduplicates”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGuEUJAWN2IGERFNCUnicGiaGf25iapshxL6vYFLqibYbaBR9BMMxkLKUicVg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

sed中的动作命令s可以以行为单位查找关键字并进行替换，其中要查找的关键字可以搭配正则表达式进行，例如将文件中所有的“：”替换为“；”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGLTnlm0ebxwODIsePJrUiaLKdQwh0LCvAlibj5BRUyYzmVWFUrtgoPSeA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其中g表示全局，也即每一行进行全部替换，若不加g则只替换找到的第一个关键字：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGrva8XX3L1nERIzP6icFM5DTIWIzEO56kaOg2LKHSz2uZmHOe2GicrIibQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

sed还可以直接处理文件，在多文库数据处理时，遇到重复barcode的情况，常需要进行barcode替换，如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6ibAiapdnGgKzF82a5NjaVeGOLcLvV30yia9V3m5jJswINjG33VENsWnjYw5Dic5uKzqhEeSibibmHibVpA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

上面的例子中第一条表示将替换结果保存为新的文件，而后面两条则进行原文件直接修改。其中“^”表示只替换行首出现的关键字。

