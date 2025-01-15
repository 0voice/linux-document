原文地址：https://mp.weixin.qq.com/s/kTHAS_DpRxInODju_JOdVw



# Linux系统安装详细教程



## **下载Vmware**

去官网直接下载

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCibt1oU79TEic1jktGWnU8QU0XM36YNvnX0cHJACKiaCBaDQofJ3gicycRw/640?wx_fmt=jpeg&wxfrom=13&tp=wxpic)



**安装激活Vmware**



VMware Workstation Pro 15永久许可证激活密钥（任选其一）



YG5H2-ANZ0H-M8ERY-TXZZZ-YKRV8
UG5J2-0ME12-M89WY-NPWXX-WQH88
UA5DR-2ZD4H-089FY-6YQ5T-YPRX6
GA590-86Y05-4806Y-X4PEE-ZV8E0
ZF582-0NW5N-H8D2P-0XZEE-Z22VA
YA18K-0WY8P-H85DY-L4NZG-X7RADD



VMware 15官方完整版，安装后采用上面的VMware许可证密钥激活即可，功能完整无缺，适合追求完美的用户使用。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC3ARXVt8Se7rtY7IOWicsRaHZk25h2kSHsbn2y82b4O5k349FtmxECXQ/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





## **下载Liunx（推荐使用Ubuntu18.04.5）**

去官网直接下载

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCkMib51dbThfPR3aMrjsNYrXC25l7opABQicXE90cnbvE8LudRm8ETjOQ/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCchAUYptOK6L45ls14PXpsjv8J9BF2X24hStOdABOG5hLmOwCeF6Tuw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





## 开始创建



首先打开第一步下载好的WMwaer

点击创建新的虚拟机

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCAqAwqbAZhD5nDS8OiaY4vPicibJjNSIEETc7N9wohC2epfoibmxyib97NPg/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





点击推荐的“典型”配置

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC5gtft5L3FwCI0abCFlicKIYphmokrxz7MJJIRUhwfMB5SrgkJicXOxuQ/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





稍后安装操作系统

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCjfXh4bKIJRibku3jXJsbdN006M01IdicmticaKlyH0MuIfW5tbpDdKqjA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



选择Linux

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC9jolyP8g3ePm8DgBYenGkG5uCTpic00l8KDYYHJbo796An7Zyr9SPOA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



然后就是起一个用户名字，选择要安装的位置



虚拟机处理器数量及内核都选择2，对于开发来说够用了。即使不够用的话，这个参数也是可以修改的。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCI3wPHg1CXbLMIaufcVk0exXsibFbezRr33I4F6VddVx0m7tiasbA0Ddw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





内存选择2048M，也就是2G，最好选择1G，2G，4G，8G，不要选择3G这样的。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCptsgfAiaY9Lyj3PIxfoLu9KPaO6vMcJPniaOJuB15MmvYBE2iazYiaf4sA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





后面这几步都可以直接“下一步”即可

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuChWGtibJ2cAprzzz89NTPfTpibJVpaibYMOylLZfXhbAXYADxUibFV4iaGbA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





虚拟机所产生的文件特别大，所以选择位置所在的磁盘最好剩余空间大一些。建议设置为20，如果磁盘空间不够可以选择40，这个空间不是实时占用。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCVmxeUCj4Bcv2ia8Qz7l0OUIIdxx4n0dtXqzQHiabHY0qIu9KpcSlp4Rw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





点击自定义硬件

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC4fdClTjFaqlgdcpuPMf1g4k7o5jqricHmc7j7RGrjNEFgmpWA2Zt3nw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





点击CD/DVD，右侧选择使用ISO映像文件，选择你第二步下载好的Linux系统文件

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCdFNEz3EwC4lZqXBIYyZNGt5QUxhS0v48XSXqIuroTeHDqEzlHVa4SA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





创建完成后开机![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCib5SAOjgy3QELuKtufbmHZticdcQgC81lePvRwuSVTXvibSSiaSg1GBUZA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



建议使用English英语

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCMeQyYjMicCRMBicGGQIGo074jurVtGj5Hs0DYibsicmU1unjvf1nuloAibg/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





这一步直接选择默认

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCpNdiblau8peAcusVVphuoiabooBp0bKt1dNUr1ric9HdvCjnqaKxeLRnQ/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)





这里也是选择默认，然后点击 “Install Now”，之后的弹出窗口里点击 “continue”

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC480kKAhiaCOTPYHPy56Gxozv270wErlk5jycrdJ2K01kdJwBRLiaViaTg/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

- 

- 在Where Are You?里面，地图里点击中国，然后点击 “continue”

- ![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCuZ4PoCGyXUQyQe2FvAQVsC7zWjcl1sl5yQ2A6UM3h6JOSJNLibyw0fA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

  

填写好个人信息，接下来就进入了下载安装的过程，整个过程大概需要20分钟。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCgHibsYmXM6bibb1lichSWHhGa8MZSR9jqBQInXItp5lU4zP2CBRk13iaLg/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



安装完毕之后选择 “restart now”，重启虚拟机。至此，虚拟机及Linux系统均已经安装完成。



![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCHkKZzAIptOSbicjAW0AUEJlVrsnlcTqVLLOohYFnQgNV3bWcqaSaibBg/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



Ubuntu刚安装完毕之后，还无法进行开发，因为有些环境还未设置好，比如：升级vi到vim，源的更换，等等。



在对Ubuntu进行配置时，命令行窗口（Shell）是必须的，但Ubuntu默认未将这个命令行窗口放在左边任务栏里，因此我们要先把它调出来。



调出来的方法也很简单，首先点击任务栏下方的九个点的那个图标，然后往下滚一屏，就可以找到termical（终端）那个图标的。或者在上方的搜索栏里直接输入 “terminal”也可以找到它。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC0E3YvmusEG4CAq8ySarWXia2aUicCXpW5DTqt4HcOZEvfnpJszq4Snxw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



因为我们对命令行窗口非常常用，所以我们可以将它固定在任务栏里。在Ubuntu 18.04里，只需将终端的图标从任务栏下面拖拽到上面即可自动固定在任务栏里，其它版本的Ubuntu可能需要右击，然后选择 “Add to Favorites”

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC2CuUZ14jM7ic1qhfy8MdXNYGSS0YboWAibFfw56jX3j4icnueJhhW2Hzg/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)







**安装VMware tools**



VMware tools可以更方便的管理虚拟机，比如共享剪贴板，也就是在虚拟机里复制文字可以直接粘贴到Window主机里，反之亦可。

###  

### 安装过程： 

- 点击“虚拟机” 然后 “安装VMwareTools(T)”，如有弹出窗口“CD-ROM门锁定”，则点击“是”

- ![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC87TSONNI1C2LsGELdAcAWscAFWbZD23kujibono8523m3KtB3s9ve1g/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

  

  打开命令行窗口，输入代码将安装包拷备至当前目录



输入cp /media/liangxu/VMware\ Tools/VMwareTools-10.2.0-7259539.tar.gz .

回车



此处的“liangxu”应替换为你的用户名，具体可以在桌面点击“文件图标”，将鼠标放在左边目录的倒数第二个即可显现路径，同理，“VMwareTools-10.2.0-7259539.tar.gz”也要替换为你下载的安装包名，这里是以我的文件名举例子。



将“VMwareTools-10.2.0-7259539.tar.gz”替换为你下载的安装包名



输入tar zxf VMwareTools-10.2.0-7259539.tar.gz

回车



进到vmware-tools-distrib，安装VMware tools。安装过程第一次询问的时候，输入 “yes” ，之后一路回车即可。



输入cd VMware-tools-distrib/

回车



最后输入sudo ./VMware-install.pl

回车

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCOZ9CtrcOwq7eWbzDX0oWwviao1S1yMqblaAWpmu9balqvFLk1pBMZLw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



安装完毕之后，将安装包删除即可。其实如果把安装包拷备到/tmp目录下的话，这一步不用做。



VMware Tools安装完毕之后，需要重启虚拟机，相应的功能才会启用，比如：共享剪贴板。

## 更改软件源

打来soft文件

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuCIOicXvAhcISIGzM9baX7xCqtyXLFFZKprEibb0OscwMSHT2oDqt76xHA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



选择Download from后面的网址

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC1tl1ZzDaJuibdqaapHQXEc6Lf9z78ha891e4110uom95CA34gicQicrcA/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

更换为阿里云的“mirrors.aliyun.com”

这样服务器就设置成国内服务器了，当然也可以更改成其他国内服务器。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/1tI5UfdTBic7MhlicibzicVO9d1gJXB0lGuC9DDPUPkRy85rHlHoa2h32IBGBr374dBxrEiczq243TjcRBqadHwm0xQ/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这样Linux就能正常使用了。



