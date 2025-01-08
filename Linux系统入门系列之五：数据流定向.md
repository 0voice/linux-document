原文地址：https://mp.weixin.qq.com/s/swRLSabylfS4jwQn_ao0rA





# Linux系统入门系列之五：数据流定向





Linux具有强大的文件信息处理系统，基于Linux系统的数据流定向、正则表达式可以方便的在服务器中处理大数据文本。接下来将带大家深入了解Linux系统文件处理规则，从而便以后各种生物信息数据的处理。

——走进Bash

## 1.数据流定向

一般命令的执行来自于标准输入（例如键盘输入，来自文件的命令也要转换为标准输入），执行完毕后将数据（处理结果或错误信息）传输到屏幕上，也即标准输出，但是这样导致屏幕十分杂乱，也不利于结果的保存查看。我们可以采用数据流定向手段将结果和错误信息传输到文件，定向方法如下：

标准输入（stdin）：代码为0，使用<或<<；

标准输出（stdout）：代码为1，使用>或>>；

标准错误输出（stderr）：代码为2，使用2>或2>>。

具体用法如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBofzJibAOAXhxXtk0OsibUZcWvh5aa07hmrhp8dZKnwqPicqp3CJQjJ8EQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

例如我们要运行显示时间和日期的shell脚本，并将结果保存在cal_date.txt里面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBWaFyPFFaiaia7amHzk0j2Fr6a7NWRp9vAXT5MRQribxnJQWKJYobrFyQg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

接下来我们运行显示生日的脚本，将结果追加在cal_date.txt中：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgB1265a82aLYJLTT13EdYeHlGukicGc6Ur4TdaPb5o0X1CXHUqrfCSOibA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

注意这里使用的是>>，若是>则内容会替代而不是累加。接下来我们修改shell脚本使cal参数错误，然后运行并输出错误信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBhRNsWF7xwBs0KxRoheqLjLM6jP0eKdpjOBfVD4CfibMG4J4XC5Jg9PA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

也可以将正确结果与错误信息同时输出到两个文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBN0bKsrFlXVCT2L8xpaKQibVSD0cIibRvJoXuzCYBeZW14JiaYIwFEeiaXg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

假如我们不希望在屏幕上看到错误信息，也不希望保存，直接将报错丢掉，可以使用垃圾桶/dev/null，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBJGscvWgKyU30iaHQD1icbCBibZSlbJOYH8xewkdxeFyNKzzJ1o2w4v7gA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

将正确结果和错误信息输出到同一个文件，可以灵活使用&符号：



![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBjlAYeicKg0krK7eekRQ3wHJw97rpYYibA6Et7qTmqQHJicic4GRxxt4xUQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

命令cat可以将文件内容转换为标准输出显示到屏幕上，同时也可以将键盘输入到屏幕上的内容写入新的文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBaA6UZZINFfUF3GVR2icBBQiagsyrFApKNqmg4ibH1b1fvUiaWDaJlsK1bQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

其中<<后面跟的是结束输入的关键词。采用<我们还可以使用文件来代替标准输入，例如将friends1.sh的内容作为标准输入写入一个新的文件friends2.sh，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBULITYicLia9wa7ApKzTSMXTXjS0OgusomoGTYCsJOicIRiaNhJ454YjYJQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



命令：tee

命令tee可以起到数据流分流的作用，例如我们将数据同时显示到屏幕上（以便下一步处理）并保存到一个文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z545g34I2Roy0OiauYdohOgBFArzcpSpKmLR3tMiaTPeiauBoBDntaSiaiazOiasbuK2xZlHAc8mNWiahPHw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



