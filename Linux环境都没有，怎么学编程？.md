原文地址：https://mp.weixin.qq.com/s/WeZLtfrMdnISpX3v5WpJfA



# Linux环境都没有，怎么学编程？





------

# 憋说了，整一套吧！

本文准备从0开始，一步步搭建一套属于自己的**多节点Linux系统环境**，这将是后续**学Linux**、**用Linux**、**Linux环境编程**、**应用和项目部署**、**工具实验**等一系列学习和实践的基石，希望对小伙伴们有帮助。

提前备好Linux编程实验环境非常重要，建议人手一套，这样以后每当学完一个理论知识需要实践时，立马就可以拿到上面去练手了。

因此本文先把环境给搭建起来！

------

# 软件准备

- `VMware`虚拟机软件：本文使用的是`VMware Fusion 10.1.0`版本
- `CentOS`操作系统`ISO`镜像：`CentOS 7.4 64位`
- SSH终端软件：`SecureCRT`
- SFTP文件传输工具：`Transmit`
- 物理宿主机系统：`macOS Catalina 10.15.4`

------

# 安装Linux操作系统

**1、创建新的虚拟机**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCprPG1YeWKnc7kzicGh2m5qNKoIlcib0vYEU0O9x8y0Tdv2kl6ibnMibjiaw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**2、选择固件类型**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCubFMnTY9ViciaC40r9scKnBWWhe8t2oPAlAHfVeMnuGbRUP0HYO6v7yw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

默认即可

**3、选择自定义设置**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCgGTfqdoibI2ACjpg8pmOQSkawHYjqAcsuNBQjUqcNk2yNkYaen7CNqA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**4、进入自定义设置**

我们初步需要自定义的主要也就是**处理器**、**内存**、**硬盘**，可以根据宿主机性能按需分配。

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCgs7VxE93iaF1sEyhyRp1PrlxTC8XUNhdtKnThOCeFcKZicVq0mtKgOmg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCicR41LE7NA342wraR6f5tf5aj86AKqYh2l4pATF1eNEYxA50slq4DKQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCAiaX8LV7o1ib1GmvN59jXCNq62jPtuXTOwJRzTSwGT06Kf0EyiaqOkGuw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**5、启动虚拟机**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCsLyzv0UntbZPS03ibLILg8Hf5TJbuTd4w8O7hBsClibRpfs00bll28Zg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

如果有权限提示，记得打开权限允许，否则可能会报错

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCeiawypoktrUUO23iak4Ju9gua7GFHCU9pPIxejZR9UwWXOKLGicq09j8g/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

正式点击启动键，过程中各种提示权限的允许动作，建议都通过一下。

**6、进入系统安装界面**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCtAjxnib2wKoSicSWvxe4WONTaGHJL3q8ibFaHnjvx2nwIHooNic3fiaSfeA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCfaGQV6iczj7kCSJFt6oicV4yelqCWJ3uMyiccx4bLkBPh7XRNbgP40tWg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**7、选择安装语言**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCWlbatRcNkdrxauAVgjiaBwnj9s0NEG7vUd1cbAK9uVCuaAEKcx55aLA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**8、选择预安装的软件**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wC7XeBomk7WrNyaXFzf9IVVjLGDyyXrziau49v3PibaiaZB1JZhcAdxG0ibg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCebZPc0f8cSpcib2CQ3TlmvFd3JlsL4dpPzoIQU00OJAibkOP5uLRdfjw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**9、配置分区**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCUEu9gzjUibpjicB7qfHYlOLdUxfubTyzCm9nro4XnBPoO661J5pYYhYQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCY8dscYmmFCmP28dw4Z7H4PyjbkmlzV3agyiaHHncd5TKGgZfEP5qH6Q/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

没有特别需求可以选择自动分区，大家如果有需要可以自定义分区。

**10、进入正式安装过程**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCDmFYia7k3Zx0zr149Tao6v5Cl2h9IBrLeXo0ZzKD4icWgm6bJQIlqwJA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wC6V72h9fwibiaEaTgJ0avyOkWQvpQvTibBDvKkjpKiaBz9HIX3L8Hic78euw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**11、安装完成并重启**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCcUAxHSooP9uWPm4bKibKhazia0Kh0iaFjjGjMPibUwCRYWiaFBvnFMM6nsQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**12、进入新系统**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCUw0r7icshS5GCL84B4YKu9zX4mV3ECoMtShIgdXOFzUd7fKfGWZmhXw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wC6w5nTrMbSy14WU1JtPTfB1OvgY8Jyqp4DsyZicmm7qEMHp4EMRehpxg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

------

# 系统是装好了，但还有几个问题

**问题一：** 虚拟机内Linux系统与外网无法连通

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCga8EywiahCVL2HDOMzpHrClxQJiao6gVhgLuzH1pngnNHol4fXiaLFXkA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**问题二：** 虚拟机内Linux系统与外部宿主机无法连通

比如我这里的物理宿主机的IP地址为：`192.168.31.35`

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCegH5cicEvVSH46ncIPECRo9v8U1RJOvV9yP7RzF0b3KjuQ9Sk3IvssQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**问题三：** 虚拟机内Linux系统节点与节点之间无法连通（如果装了多个Linux节点的话）

------

# 网络配置（极其重要！）

**1、首先尝试查看虚拟机系统的IP地址**

使用命令`ifconfig`进行查看。我们会发现装好的系统并没有为它设置IP地址。

**2、设置虚拟机与物理宿主机的网络连接**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wC6l23n8D39kiah3GJtw0HhlZC8S7oYzGpVHFZ212ibR3Jf7PvXwxlmrMA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

首先选择**桥接模式**，另外由于我的物理主机是通过WiFi的方式连接到路由器最终访问外网，所以此处我选择的是`Wi-Fi`这一项

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCxBxqNweKTlrs4QqwqHN0EMmA04f2cGASMVl6XoUNphynxlNficjwfsw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

小伙伴们可以按实际情况进行选择。

**3、为虚拟机配置固定静态IP**

首先使用`dhclient`工具为本机分配一个网络内可用的IP地址：

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCrH6sHBCfSfjDuWgC9E2BvG10FCmPFzpS0aiabib7Aciat3D7388ic4JJqA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

接下来编辑虚拟机系统网卡配置，将上面分配所得的IP地址配置进去：

使用命令编辑：`vim /etc/sysconfig/network-scripts/ifcfg-ens33`

修改配置如下：

```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=824ec4bd-a9ae-4410-8346-17ce7f3dd111
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.31.110
NETMASK=255.255.255.0
GATEWAY=192.168.31.1
DNS1=119.29.29.29
```

尤其注意下图红色标记部分的配置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCHJn749TSGKh18zn3GAquuOq55NowMm5XKWmsFSqLMmtGFVEtpXqGUg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

编辑完成，重启网络设置即可

```
systemctl restart network.service
```

------

## **检查安装配置结果**

**1、首先检查IP配置结果**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCkEU1KU4LOPF9oBTib2lqHOLLHufAAoXT4QibQ0LicaQYS5d4lu2VlFnBA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**2、检验虚拟机系统网络和外界的连通性**

包括检查和外网的连通、和物理宿主机的连通、以及和兄弟节点（前提是你安装了多个虚拟机系统节点的话）之间的连接

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCNegicxiak7E4QhwRfCnsK7gYZlB7r0u8mb9BDGqChtgvGwxprKTzEVOA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

3、反向检查物理宿主机和虚拟机系统网络的连接性

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCnQicY8yfV55eg6w6WazztlL49uQDBCFxWyYf6cJLQ1nUiamUIGAIlicRQ/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

至此，大功告成！

------

# SSH远程连接

在宿主机通过SSH终端连接虚拟机内Linux系统，成功！

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCzUFUPXIFLFPS9icibpUbpzjz1ep5BMLt2l9qachrvVawygXmanWLNVQw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

------

# SFTP文件传输

在宿主机通过SFTP工具即可访问虚拟机内Linux节点，从而可以实现本地和服务器的文件互传

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCOufDIW8SPrevhMnP3m2d8as9STWy7KMMELSh37Wv9MxicOXERE6kXrg/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这样一来，一个可用的Linux节点就打造完成了！

------

# 何不再多弄几个节点？

可以完全重复以上步骤再打造出多个Linux节点，当然**更简单的方式**则是直接通过上面已经装好了的虚拟机节点**直接克隆**，来快速生成其他节点。

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wC8kzk6p04yDRh4GeYv93PzNDxRgS4RlibjBzLBmT1NWDzQAC3vHBNRwA/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzq8IHr5xUXxKsKO2UwFm8wCoDDNR5dY6eiaatJoWKgYvuxxdRz76JiaaZv43yXiacHPGC6auKJyxClOw/640?wx_fmt=png&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

克隆完成之后，只需要再配置一下新节点的网络即可。

------

# 后记

好啦，现在**多节点的Linux环境**终于搭建完成了，后续不管是 **学Linux**、**用Linux**，还是**Linux环境编程**、**应用和项目部署**、**工具实验**，都有可以动手实践的地方了。

------

