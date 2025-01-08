原文地址：https://mp.weixin.qq.com/s/nq4wK0uXnDY7rhYxqCqK9Q





# Linux系统入门系列之四：工具命令



![图片](https://mmbiz.qpic.cn/mmbiz_jpg/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRngaj5w9EXFFuIIVEj8icRGXwCDrMeYInjKiaApicZNNhkJ3C4psWzSYBw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR1gZPxrzMK1znuIOPJS74YqywYqOOAia1SzRsk9Pln0TH6w8JnvkyicdQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

在上一篇文章[Linux系统入门系列之三：初识Bash](https://mp.weixin.qq.com/s?__biz=Mzg3MzEwMzIwOA==&mid=2247483985&idx=1&sn=968cc499d2aa29c3f46bf4a0e9db6eda&scene=21#wechat_redirect)中，我带大家初步认识了Bash这个Linux系统中的Shell，并学习了使用vim编辑、处理文本信息。事实上Bash拥有非常多的工具命令，并且很多工具命令已经集成化，可以完成多种多样的任务，就像Windows系统中的Office软件一样。接下来将带大家认识更多的工具命令以及数据的输入与输出，从而便以后各种生物信息数据的处理。

——走进Bash

## 3.工具命令

虽然Vim很强大，但是批量处理一些文本文档尤其是很大的文件（例如高通量测序数据），一些逐行处理的工具命令非常实用。

### ⑴选取命令：cut，grep

选取命令可以基于关键字按行搜索，将含有关键字的行选取出来。一般来说cut为剪取（注意不是剪去）标准输出的内容（可以理解为屏幕显示内容，可以来自cat/more/less），而grep除了处理标准输出的内容还可以处理文件，使用规则如下：

```
cut -d ‘分割字符’ -f ‘范围’cut -c ‘字符范围’grep -acinvw --color=auto ‘要选取的内容’ ‘文件名称’
```

其中grep参数-i忽略大小写，-v反向选取，-n输出行号，-w匹配整个单词。**注意，有时候工具命令里的单引号和双引号不能相互替代！**使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR2ZEKQB3ic3BLiaoggCwq5s0tCI7ricCLw23cut6thbsSrNZUncx1w5zTA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

--color=auto将关键字使用其他颜色标识：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRAuwV1E5RlGtCZw2gtianMN5cZkHiaLUKib7LDUOm4VhFrqXImLy68JGeg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



### ⑵排序命令：sort，uniq，wc

sort可以依据数据类型来进行排序，uniq可以合并相同数据类型并计算数目，wc可以计算文件的字符数、行数等信息，使用规则如下：

```
sort -bfMnrtuk ‘文件或标准输出’
```

其中-f忽略大小写，-b忽略最前面空格，-M按月份排序，-n纯数字排序，-r反向排序，-u相同数据拍在同一行，-t分隔符类型，默认为空格（若是tab需要转义：-t $'\t'），-k作为排序标准的区间，默认以行首排序。

```
uniq -ic
```

其中-i为忽略大小写，-c为对相同数据进行计数。

```
wc -lwm ‘文件或标准输出’
```

其中-l列出行数，-w列出字数，-m列出字符数，排序计数的具体使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRexokJue623pWBWcMDNFrgsuomDkI4CYZVd5AMnu3Q6BYVTxkUorWLg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

计算文件的整体数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRBXL7HF6iaiaaQCFTnIEfRP1wl8YuFfibzdJGsfjHt2eYR6SwWxhIDnEDg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

需要注意的是，不同语系下排序顺序不同，例如在en_US.UTF-8中，字母无论大小写均按照字母表顺序排序，而C语言中大写字母排在小写字母之前：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRzUTB0494aNict01ppSl1jKasT6lnR6tTKmmItAgzQIO54icfmBLIaxxA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRLLibhUs9dicBFtictqRQq2WXjwwvehO3ykN7uxUojpkqU0HnKiaNUcHZ1w/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

计算当前路径下文件数目：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRciaR1LbahPmrHWs48s7xaI9icHX6Xmmfice1F4qFT9Y1fLA3Rr5b6VXyw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



### ⑶字符转换命令：tr，col，expand

命令tr可以删除或替换文字信息，col和expand可以将tab键转换为空格键，使用规则如下：

```
tr -ds ‘要删除的内容’ ‘要替换的内容’
```

命令tr可以处理来自标准输出的内容，其中-d为删除，-s为替换，例如将“：”替换为“；”方法示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsREtbNric8VHakkUGuDRVLv5dnPVfp0PN7b7RCGYFGLAVSZf1O4po9bzA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

将所有的小写字母替换为大写字母并保存：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR4JZJxshU0oYMiamabnl65f8iabVVfQGrodtFzR5qXxDpyUCREYVgKiafQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



```
col -x
```

命令col可以处理标准输出的内容，其中-x将tab键转换为对等的空格键。使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRKMymI26tU0yRGD3iaicH5LlkMQPBu0zxPL9Oicia48KyDVgu6ZGqsSVqibw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



```
expand -t
```

命令expand可以处理标准输出内容，其中-t后面跟数字，一般一个tab键可以用8个空格键替换。使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRW1GNKR6aeeMzf6HK8yQEuibHOeGGfNbh1BcymgiaPia2VzA4HJAZN4rEg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



### ⑷整合切割命令：join，paste，split

命令join可以将具有相同数据的两个文件整合到一起，命令paste将两个文件的行并列并以tab分隔，命令split可以将大文件根据大小或行数切割成小文件以便于复制。使用规则如下：

```
join -ti12 file1 file2
```

命令join可以处理文件内容并转换为标准输出，其中-t后面跟分隔符，默认是空格或tab，-i忽略大小写，-1后面跟数字，也即第一个文件以一行的第几个字段为关键字，默认为行首，-2也即第二个文件以一行的第几个字段为关键字。使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRicuicXo852smmRydvpG47hEVuoSzd6fsXY1AEzc31uachYuKFn60UhAw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



```
paste -d file1 file2
```

命令paste可以按行将两个文件整合为一个文件，而不需要按照关键字。其中-d后面为分隔符，默认为tab。使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRyfOGlkdeaxaVIyQme6d6iaB3Faf5ibDAp2s3jCeFzclew93r5FuuoibLw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



```
split -bl file sfile
```

命令split可以直接切割文件数据，其中-b后面加要切割成的文件大小，可以直接写字节数或者加k、m单位，-l后面加要切割成的文件行数，sfile为小文件前导名，命令会自动加后缀区分，使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRibPWIhu8f8bbLqJUYwHNg2TOLQ2ZCSI2pRSB9D8pS8Jhia7icgSvLWa5Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

