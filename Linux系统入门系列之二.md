原文地址：https://mp.weixin.qq.com/s/lHzsdtpjYiGm2diy33gC6g



# Linux系统入门系列之二



### 3命令管理

#### 3.1命令连接符

当需要一次执行多个命令的时候，可以同时输入，不同命令之间可以使用分号“；”隔开，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2ibLGz9Kicaxib4axXebx32yDye5T9z80FicLWNRIRbuWjblX9Iric4e4CZg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

上面的多命令之间是独立的，按照先后顺序执行，多个相互依赖的命令之间还可以通过逻辑连接符“&&”和“||”来连接，具体如下：

cmd1&& cmd2：若cmd1执行正确则开始执行cmd2，否则不执行；

cmd1|| cmd2：若cmd1执行正确则不执行cmd2，否则执行。

具体示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2c1JVJ5DfVUgOiajjl8PMCev9e5hr59ap9I0eJdU0kfbpTBhXoqGnePg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



#### 3.2管道命令

管道命令（pipe）是由多个命令组成的定向处理流程，但与命令的连续执行或判断执行不同，后续命令仅能处理前面命令传来的正确信息，不同命令间使用“|”界定。

例如，我们列出etc下的所有文件，并将结果进行分页展示，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2bp9kZcFbBAzb97LlN1oVNyvuWaMQpiaOdyTvYbib18Mx8CJxkhJSDPQw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

查询服务器用户登录信息，并将“tengwk”用户的信息选取出来，并剪取用户名和登录时间：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2rrw7EicdOtokT43FxGficlwar5YDyhdoCLUOrTmPZSrbzlHlcuXlEtkg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

命令：xargs

该命令可以使不支持管道命令的指令引用标准输入内容，使用示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2TDJ9pdYffvhZdVELuGF6yblic0ictnjjSS3nWSLBvkXicE69tmFgXLqsw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

命令ls -l只能作用于文件和路径，并不能处理标准输入的内容，也即不支持管道命令，因此会将所有文件列出。然而xargs可以将标准输入的内容转换为指令的作用对象。该命令还可以产生命令的参数，例如-p可以提醒后面命令的意义，用户可以输入y（yes）或n（no）来选择是否执行：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2UdNTepF4iaNicywOm3DibIMVYIN5IpsrKlbCzUJ3TuGe24kMq2pFJeunA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

xargs具体参数如下：

-n后面加次数，表示命令在执行的时候一次用的argument的个数，默认是用所有的；

-P修改最大的进程数（也即一次提交的最大任务数），默认是1；

-i或者是-I，将xargs的参数的每项名称，一般是一行一行赋值给{}，可以用{}代替，例如：ls *.out | xargs -i mv {} {}.txt。

 

#### 3.3软件脚本

在Linux中，可以使用命令充分调用各种软件（脚本）来完成分析任务，也可以将Linux命令整合为shell脚本，这样便于管理与修改。

命令：perl

在Linux中调用perl脚本并输出结果，示例如下：

perl perl02.pl

命令：Rscript

在Linux中调用perl脚本并输出结果，示例如下：

Rscript r01.R

命令：sh

执行多命令整合成shell脚本，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic23wwFgTvCAwsUrN9tL5D7suBX5mS8dAUODcJvqFQ2ylghxqzrAiaGGiag/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

对于安装的软件，调用时则需要完整的绝对路径，例如Mothur，需要输入/sdd/userLogin/zhengjw/softwares/mothur/mothur然后回车来输入命令，或者直接输入命令，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2yWjwMFSwz13IAHAfJt9O7I80yrtdiaAibVeibicibwkrWBjib4aL20kGpjcA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

对于经常用到的软件，我们可以将其路径添加到环境变量PATH，则可以直接调用，首先我们需要修改用户主目录下的配置文件，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2phVKlIsSwmHUCeJ6ClVYjAdibjFMu7J1RrJdEPbAo804myk5icJUVKSg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

最后执行source激活环境变量：

source ~/.bashrc

这时候便可以直接调用mothur：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2WQkZoONW52aUz3PvhaVoV7faEOe4ZvYw1OfE0pG2HYl3zKoeSMmFaQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

 

#### 3.4任务管理

命令：nohup……&

表示命令无间断的后台运行，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2dicMZ55h5BnnQBhg4I1eV1jyYOicW8q4jGXXEPWyFbR1qicngLAy5U3JQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1) 

命令：jobs

查看当前用户当前窗口正在运行的脚本程序，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2s7J2RpGtbbNxIibmNpukiazheNPM9GP77DxOSdNxb3iaXyc3RZW3GPUOQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

命令：ps

列出当前用户正在运行的程序，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2UebDkCgiaeznaFRaIXL2dxRz6mPJ1TN1t25MdcXM13jRHRzibSvym4Eg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

列出正在运行的程序及其完整路径：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2CBIvG4PoCoRX61ia5xWw81BMBf56pZyyYXT1LUXHLKZxkq4jROxnG8A/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

参数选项含义如下：

u：与当前用户相关的进程；

x：通常与a参数一起使用，可列出较完整信息（包括程序执行路径）；

f：按照程序运行时间进行排序。

注意这个命令参数选项前不需要加“-”。

命令：kill

结束当前正在运行的某个程序，示例如下：

kill PID

kill %程序编号

其中%后面跟的是jobs查看的程序编号，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2ic90EY0aIobZ4ZKRmrWyFk1zfNviaSVAcrvCOvYlssibjB4cu5RHlAkUQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1) 

命令：top

动态显示显示当前系统正在执行的进程的相关信息，包括进程ID、内存占用率、CPU占用率等，示例如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibj9nANUc6z7k0nSXE0LSvTiciaWpWc41ic2wXAsOmPiak080xKxzTBsj0vvOvVzdia5gW3TTzI4he5LUCN13hxwl0fw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



