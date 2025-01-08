原文地址：https://mp.weixin.qq.com/s/RSfrvmk7OF2ytwsmp7fGOw





# Linux系统入门系列之三：初识Bash



![图片](https://mmbiz.qpic.cn/mmbiz_jpg/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRngaj5w9EXFFuIIVEj8icRGXwCDrMeYInjKiaApicZNNhkJ3C4psWzSYBw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR1gZPxrzMK1znuIOPJS74YqywYqOOAia1SzRsk9Pln0TH6w8JnvkyicdQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

事物最外面的一层我们称之为壳（Shell），例如贝壳、地壳。壳是事物与观察者信息交流的媒介，观察者通过壳可以直观地感受、描述事物。计算机同样是如此，普通用户无法直接操作计算机的内核，也需要借助Shell这个媒介来与计算机内核进行交互。不同的操作系统拥有不同的Shell，对于Windows系统，图形界面的Windows即是其shell；而对于Linux系统，其Shell称之为Bash。

——初识Bash

## 1.Bash变量

### ⑴环境变量

Bash内置的用户属性变量多属于环境变量，类似于全局变量，例如PATH、HOME、MAIL等，环境变量只能通过修改用户配置文件（~/.bashrc或~/.bash_profile）来进行修改。环境变量通常以大写字符来表示，可以使用echo$命令来显示变量，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRcaQj6TicpIG5Ugpv94a4BmpcrQd93pNaiczC4QBPSULmdkpLwhwOwbjg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

我们可以使用env命令来查看系统默认的环境变量：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRYoSyOg0xBVAhBXeoYR1eCKFJMVICFSicicH9vMaic5haH6Vhq4TSEqZ5A/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其中有些环境变量比较常用，例如RANDOM变量是常用的随机数生成变量（0~32767），示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRKk4ibWl0Lvx8DMianFc6mtQ3FZc6u8EvYt4jkic7aP6Xib2gBicOjKxpicOg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

此外，环境变量PATH非常有用，可以添加常用软件的绝对路径来方便软件的调用；环境变量？（是的，就是一个问号）为上一个执行的命令所传回的值，一般成功执行，传回0，发生错误，就会回传错误代码。

### ⑵自定义变量

用户可以根据自己需要自定义变量，属于局部变量，使用“=”进行赋值（等号两边不能有空格），变量名由数字和字母组成且以字母开头，赋值内容若包含空格等特殊字符需加双引号，双引号内也可以引用其他变量，特殊字符可以使用反斜杠“\”来转义。可以使用echo命令来显示变量，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRVQFgH1lqib7dvOLFpWns2IoXPDaNsAOIAiacyjP6D8n5XQfFKkq5kHrQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以使用declare来声明变量为数值（-i）类型，例如生成个位数的随机数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRLxPj8c1uamGLIuh0kCBCZI0qB4ZeIJTGNXOXIibhVMDX65L9rrUH9ow/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



如果不事先声明，赋值会默认是字符串：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRe4cQNsJJMtJJoCCRy2f74vKVib5tgdYOrn2GTeDlBw6fHahpV6pTjEQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

取消已经赋值的变量可以使用unset命令，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRXMNt602haDADqQBryZPgU3iaSROKhic6icwwicw2lKD5pBFSwLPRlVSS6g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

一般一个变量只能在一个子程序中运行，export命令可以将变量变为环境变量，从而可以在其它子程序中运行，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRnKyb2oeMOWyEHANmIe1SQECwTXBibCgibuzs0OCCYyicoyRRYVc6ThRTg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

使用set命令可以查看当前环境所有变量（包含环境变量和自定义变量）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRLjKDnaXuzBMNJSuT6Q2FOrU2icicTJ6ANCVntYYmwqjTqwHtsiaic3Ehpg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

如果要实现计算机与用户的交互，让用户用键盘来输入变量内容，可以使用read命令，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRWtoBVyI5u6g4tEeia338Dkf4YNdwH9lbol28z1CrFquTqk3ZiaaJXGzA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

还可以设定提示字符以及限定输入时间：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR0flJcZicJUrh8GUuxIliaK9Zo8w8mjPliaR7cxVpAvLINjgIVsEsexGGQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



### ⑶Bash数组

数组也即向量，可以通过变量名与index的方式赋值，示例如下：



![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRFFq1WU2OJiaSTq1mhq43W9dwj4JYea0ZbwIZGYLORPmjrn3PECkJcrQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

还可以通过“@”作为index提取所有变量：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRKQcJpayW3PfVYgzkbf2dOKLsicQtbkAkhootnwq6a8Ury3hJFOt8frA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

还可以直接通过括号来进行赋值，不同元素间空格隔开：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRHEyEoye0tqz2XFsI9NPiaS1XceMe7BG96OCzGibaMY6ajvVvXb2MV6tg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

注意，默认的index是从0开始的！

### ⑷变量运算

在赋值的时候，可以直接使用“$”或“${}”来引用变量和数组，可以使用“$()”引用命令结果，使用，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRNpxpe4EOMUhAIscniavravBzVgdibZ6MNXvj1cjTykQJNgRV76bPcWqw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

变量可以直接累加：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRGyjSEm7ibB19266u2T8xnrFQK9uwfCCAZpDVUAtkguNlCulic7icSeAOw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以通过“#”来从左到右删除变量内容，通过“%”来从右到左删除变量内容，除标记字符外其他字符可以通过“*”（多个字符）或“?”（单个字符）来指代：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR47mVPpHct4hOxVkUHNjl6BxzkhVu9WPYV4TgwAXXd7SyugqbFdr1sQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以通过“/”将旧字符串替换为新的字符串：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRpREzlIhI9tbECeH4Grk8eUjEZ3O4WABxkSwCKLRiaNs3lDiawGvd7ib8A/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

假如标记字符存在于多处，“#”为删除最短字符，“##”为删除最长字符，同样适用于“%”和“/”，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRtpcxWqibG3ayRpJj0CiaObkXicSJuf8SHRG8N1Jc2A5ibR6fS3ArqbvYTw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

通过shell脚本，也可以引用其他软件和脚本的运行结果来进行变量赋值与运算：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsReA6ibDhbOT85mMp12R0J6u55bkEptkibSCRls1ibJkYNPsGqxz0jSYkSg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRSpxA4sXxnet51uBebHlwz2oaaxg09JOE6hW5W1EA03kxfvYrIgBM4Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

在变量运算的时候，可以通过declare命令声明变量类型，不同类型变量类型例如字符串和数值，其运算规则不同，具体如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRRh6tDGG1F9h1f1Z5qEmBP51PHNlBBFhW6ySCIGXcWDAYD2V2RcyIbw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其他参数选项如下所示：

```
-a：声明为数组；-x：相当于命令export；-r：声明为只读变量。
```

在Bash中，任何命令（包括管道命令）加上反单引号``之后都可以直接作为变量引用，其值为命令运行结果，可以为变量赋值，例如我们列出目录下所有txt文档并将其储存在变量txt里面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRtQJ0pqNW15S3ZjokmOkADlXtOrx8yc64WyiaTa8uLGYViabicebQPxFZw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这一点对于以后的Shell脚本编写非常有用。下面我们可以列出某文件的文件名以及其行数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRoFzmibicVaTTVINBNjEd5CNBZ1n6kNp0tY55ydU2LHyC9er3v2p1ZHEw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

利用这种用法可以很方便的计算序列数目。

## 2.文本编辑

### ⑴基本编辑

Linux平台的大多数文件均是ASCII的纯文本文件，在Linux中Vi/Vim是强大的文本处理工具，Vim可以看成Vi的升级版。Vim有三种模式：一般模式、编辑模式、命令行模式。使用vim创建或打开已有文本文件，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRIic3Piaias8f0DYR0ibxZ3ic6fUjZVoLt26cY5smhwpp5hqZN0PmWPnM2mw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

此时即进入一般模式，这时候可以进行删除、复制等操作（最好不要复制），但是无法输入内容：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRA1ZWHS2VZpwf87ln0EEntI5fn3fSKA1SHKtdG1fcxIseEcqyqtDAng/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

当按键盘上“a”、“i”键，下方显示“INSERT”，开始进入编辑模式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRDAya1Gc4N3huBz4W2ID2kg3nHic3aqyNgTjHs0BgcEpX88RG5XNGU2g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以使用键盘输入，也可以从其它文件（txt、word、excel等）中直接复制粘贴过去：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRo6ULLibrictqIBJghbYd80nSdoicwUicrj0jMN6SfMbEBKbxvJ2gAhEAoA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

编辑完毕后，按“Esc”键退出编辑模式，又进入一般模式。当输入“：”、“/”“？”是便会移动到最下方的命令行进入命令行模式。输入:wq命令按回车键保存并退出。如果保存还未命名的文件，:wq空格后输入文件名（若已命名则是另存为），若是不想保存修改，则输入:q！命令。

### ⑵文本处理

在一般模式里，x/X为向后/前删除一个字符，yy、dd为复制、删除光标所在行，p为将复制内容粘贴到光标下一行。在命令行模式里，Vim有很强大的文本处理功能，可以对文本进行批量处理，具体如下。

输入“/+内容”或者“?+内容”来搜索想查找的内容：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRuPyDzndDQ71iaDV7U9oPFUwHo4uXxC7EEhyfpxcnMVblOOkVsmvqmibw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

按键“n”或者“N”（即Shift+n）可以向下或向上查找内容。在命令行进行查找替换。查找第2行到第4行的第一个is并替换为ia，其命令为:2,4s/is/ia/：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRiaNzZBqOK8TKMkXTicUw6l4hEJKmiaAE4nmx61hiclTZx191lDpfXGYa2Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRW6Quv7hL3DVc7ia1QQ32kbzPdym8K9jzHOQD3xFRZwaAUCxzv5jy88g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其中s为替换的意思，若是第三行全部is替换为ia，则为:2,4s/is/ia/g：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR3vvCH03uXzcT6YlSIQno8WFajTHLM3T8TUo7LdG80t8wyCkb2ia3ECA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRKwWgcRDzwhl9Z4J4AO1DYiczahH784O6hWrVjT66YxyfRheyxKqRdeA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

若是最后一行行号可以用“$”来表示，若是删除，也可以实现：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsR3V34jdaxUsZFnRIG6EC4LrNqlGwrwGbCd2dIyibsnR88yPx6gvODSrA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRvFV0cnMYzGZ5M9BibQz6vDIkPmhaohFhdFvTGhXns2r7QuwAL2lQWgg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

此外，输入:set nu/nonu可以设置显示/不现实行号：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z6Grz1XEGOXXbibR4ktVaEsRua89fdDiaf8lVvORlr3zQqEknckWlSstrkgY4ghrz1IsJOACNsWF37w/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



