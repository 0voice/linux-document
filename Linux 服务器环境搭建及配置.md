原文地址：https://cloud.tencent.com/developer/article/2055948?areaSource=102001.20&traceId=-8Bh7LTxkNRsIeWZa1ivO





# Linux 服务器环境搭建及配置[通俗易懂]



### 环境搭建（源码）

#### 1、配置 JDK 1.8 运行环境

（1）、新建文件夹。

```
mkdir /opt/java
```

（2）、进入安装 jdk 的位置。

```
cd /opt/java/
```

（3）、利用 WinSCP 工具，将下载的压缩包上传到目录下。

（4）、然后进行解压命令，将压缩包进行解压，解压完成之后，执行删除命令删除压缩包。

A)、解压命令：`tar zxvf 压缩包名称`

```
tar zxvf jdk-8u221-linux-x64.tar.gz
```

B)、删除命令：`rm -f 压缩包名称`

```
rm -f jdk-8u221-linux-x64.tar.gz
```

（5）、配置运行环境：

1)、编辑 /etc/profile：

```
vi /etc/profile
```

2)、添加如下配置：

代码语言：javascript

复制

```javascript
export JAVA_HOME=/opt/java/jdk1.8.0_221
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin
```

（6）、使配置文件修改生效。

```
source /etc/profile
```

（7）、验证是否配置成功。

```
java -version
```

#### 2、配置 Tomcat 服务器

（1）、新建文件夹。

```
mkdir /opt/tomcat
```

（2）、进入安装 tomcat 的位置。

```
cd /opt/tomcat/
```

（3）、利用 WinSCP 工具，将下载的压缩包上传到目录下。

（4）、然后进行解压命令，将压缩包进行解压，解压完成之后，执行删除命令删除压缩包。

A)、解压命令：`tar zxvf 压缩包名称`

```
tar zxvf apache-tomcat-8.5.43.tar.gz
```

B)、删除命令：`rm -f 压缩包名称`

```
rm -f apache-tomcat-8.5.43.tar.gz
```

（5）、修改 tomcat 运行权限。

1)、进入文件夹。

```
cd /opt/tomcat/apache-tomcat-8.5.43/bin
```

2)、修改权限。

```
chmod -R 777 startup.sh shutdown.sh catalina.sh
```

ps：此处我们是将 `startup.sh`、`shutdown.sh`、`catalina.sh` 三个文件的权限设置低，其中 `startup.sh`为开始运行，`shutdown.sh` 为结束运行，`catalina.sh` 为运行过程。

（6）、运行 tomcat。

a)、进入文件夹。

```
cd /opt/tomcat/apache-tomcat-8.5.43/bin
```

b)、tomcat 运行命令：

```
./startup.sh
```

c)、tomcat 停止命令：

```
./shutdown.sh
```

d)、tomcat 调试命令：

```
./catalina.sh run
```

e)、查看进程：

```
ps -ef |grep tomcat
```

f)、杀死进程：

```
kill -9 进程号
```

（7）、实时查看 tomcat 运行日志。

a)、先切换到日志文件夹目录：

```
cd /opt/tomcat/logs
```

b)、查看：

```
tail -f catalina.out
```

c)、退出tail命令：

```
Ctrl + c
```

#### 3、配置 Nginx 反向代理服务器

（1）、安装 gcc，gcc 是用来编译下载下来的 nginx 源码。

```
yum install gcc-c++
```

（2）、安装 pcre 和 pcre-devel

PCRE(Perl Compatible Regular Expressions) 是一个 Perl 库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，pcre-devel 是使用 pcre 开发的一个二次开发库。

```
yum install -y pcre pcre-devel
```

（3）、安装 zlib，zlib 提供了很多压缩和解方式，nginx 需要 zlib 对 http 进行 gzip。

```
yum install -y zlib zlib-devel
```

（4）、安装 openssl，openssl 是一个安全套接字层密码库，nginx 要支持 https，需要使用 openssl。

```
yum install -y openssl openssl-devel
```

（5）、新建文件夹。

```
mkdir /opt/nginx
```

（6）、进入安装 nginx 的位置。

```
cd /opt/nginx/
```

（7）、利用 WinSCP 工具，将下载的压缩包上传到目录下。

（8）、然后进行解压命令，将压缩包进行解压，解压完成之后，执行删除命令删除压缩包。

A)、解压命令：`tar zxvf 压缩包名称`

```
tar zxvf nginx-1.14.2.tar.gz
```

B)、删除命令：`rm -f 压缩包名称`

```
rm -f nginx-1.14.2.tar.gz
```

（9）、打开文件路径。

```
cd /opt/nginx/nginx-1.14.2
```

（10）、编译。

```
./configure
```

（11）、安装。

```
make && make install
```

（12）、打开 `/usr/local/nginx/conf` 下的 `nginx.conf` （可忽略）

```
cd /usr/local/nginx/conf/nginx.conf
```

（13）、配置端口，防止端口冲突（可忽略）

（14）、打开 `/usr/local/nginx/sbin` 目录。

```
cd /usr/local/nginx/sbin
```

代码语言：javascript

复制

```javascript
...
    server {
            listen       80;
            server_name  localhost;

            #charset koi8-r;

            #access_log  logs/host.access.log  main;

            location / {
                root   html;
                index  index.html index.htm;
            }
...
```

（15）、启动。

```
./nginx
```

（16）、测试是否安装成功。

使用浏览器打开：127.0.0.1:80

（17）、nginx 重启。

方法一：进入 nginx 可执行目录 sbin 下，输入命令：

```
cd /usr/local/nginx/sbin
./nginx -s reload
```

![img](https://ask.qcloudimg.com/http-save/yehe-8223537/9b44a682ded79b3b4b83471d9ce3fd2a.png)

 方法二：查找当前 nginx 进程号，然后输入命令：

```
netstat -apn|grep nginx
kill -HUP 进程号
cd /usr/local/nginx/sbin
./nginx
```

![img](https://ask.qcloudimg.com/http-save/yehe-8223537/3619322eb0c12a6e4ba0f24d64af7689.png)

Q：

1）、如果出现 [emerg] getpwnam(“nginx”) failed 错误。

```
useradd -s /sbin/nologin -M nginx id nginx
```

2）、如果出现 [emerg] mkdir() “/var/temp/nginx/client” failed (2: No such file or directory) 错误。

```
mkdir -p /var/tem/nginx/client
```

3）、如果您正在运行防火墙，请运行以下命令以允许 HTTP 和 HTTPS 通信。

a)、`firewall-cmd --permanent --zone=public --add-service=http`

b)、`firewall-cmd --permanent --zone=public --add-service=https`

c)、`firewall-cmd --reload`

**nginx.conf 文件说明（修改版）**

代码语言：javascript

复制

```javascript
#user  nobody;
# 工作进程：数目。根据硬件调整，通常等于cpu数量或者2倍cpu数量。
worker_processes  1; 
 
# 错误日志存放路径
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

# nginx进程pid存放路径
#pid        logs/nginx.pid; 
 
events {
    # 工作进程的最大连接数量
    worker_connections  1024;
}
 
http {
    # 指定mime类型，由mime.type来定义
    include       mime.types; 
    default_type  application/octet-stream;
 
    # 日志格式设置
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';
 
    # 用log_format指令设置日志格式后，需要用access_log来指定日志文件存放路径
    #access_log  logs/access.log  main; 

	  # 指定nginx是否调用sendfile函数来输出文件，对于普通应用，必须设置on。如果用来进行下载等应用磁盘io重负载应用，可设着off，以平衡磁盘与网络io处理速度，降低系统uptime。
    sendfile        on; 
    # 此选项允许或禁止使用socket的TCP_CORK的选项，此选项仅在sendfile的时候使用
    #tcp_nopush     on; 
 
 	# keepalive超时时间
    #keepalive_timeout  0;  
    keepalive_timeout  65;
 
    # 开启gzip压缩服务
    #gzip  on; 
 		
 		# 负载均衡配置（四种策略：轮询（默认）、weight、ip_hash、fair）
 		upstream myserver {
 			# 每个请求按访问ip的hash结果决定，这样每个访客固定访问一个后端服务器，可以解决session问题。
 			ip_hash 
 			# weight代表权重默认是1，权重越大表示分配的客户端越多。
 			server	127.0.0.1:8080 weight=5; 
 			server  127.0.0.1:8081 weight=10;
 			# 根据响应时间决定。
 			fair;	
 		}
 		
    # 虚拟主机
    server {
        # 配置监听端口号
        listen       80;  
        # 配置访问域名，域名可以有多个，用空格隔开
        server_name  127.0.0.1; 
 
 		# 字符集设置
        #charset koi8-r; 
 
        #access_log  logs/host.access.log  main;
 
 		# 请求转发
        #location / {
        #    root   html;
        #    proxy_pass	http://myserver; 
        #    index  index.html index.htm;
        #}
        
        # 动静分离
        location /www/ {
            root   /data/;
            index  index.html index.htm;
        }
        
        location /images/ {
            root   /data/;
            autoindex on;
        }
        
        # 错误跳转页
        #error_page  404              /404.html; 
 
        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
 
        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}
 
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        # 请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
        #location ~ \.php$ { 
        # 根目录
        #    root           html; 
        # 请求转向定义的服务器列表
        #    fastcgi_pass   127.0.0.1:9000; 
        # 如果请求的Fastcgi_index URI是以 / 结束的， 该指令设置的文件会被附加到URI的后面
        并保存在变量$fastcig_script_name中
        #    fastcgi_index  index.php; 
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}
 
        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
 
 
    # another virtual host using mix of IP-， name-， and port-based configuration
    
    # 另配一个虚拟主机
    server {
        listen       9000;
        server_name  127.0.0.1;
 
        location ~ /admin/ {
            root   html;
            proxy_pass	http://127.0.0.1:9001; 
            index  index.html index.htm;
        }
        
        location ~ /user/ {
            root   html;
            proxy_pass	http://127.0.0.1:9002; 
            index  index.html index.htm;
        }
    }
 
    # HTTPS server
    #
    #server {
    # 监听端口
    #    listen       443 ssl;  
    # 域名
    #    server_name  localhost; 
 
 	# 证书位置
    #    ssl_certificate      cert.pem; 
    # 私钥位置
    #    ssl_certificate_key  cert.key; 
 
    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m; 
 
	# 密码加密方式
    #    ssl_ciphers  HIGH:!aNULL:!MD5; 
    #    ssl_prefer_server_ciphers  on; # ssl_prefer_server_ciphers  on; #
 
 
    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
 
}
```

#### 4、配置 MySQL 数据库

（1）、新建文件夹。

```
mkdir /opt/mysql
```

（2）、进入安装 mysql 的位置。

```
cd /opt/mysql/
```

（3）、下载并安装 MySQL。

```
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
```

`yum -y install mysql-community-serve`r

（4）、首先启动 MySQL。

```
systemctl start mysqld.service
```

（5）、查看 MySQL 运行状态。

```
systemctl status mysqld.service
```

（6）、在日志文件中找出密码。

```
grep "password" /var/log/mysqld.log
```

（7）、进入数据库。

```
mysql -uroot -p
```

（8）、输入初始密码，此时不能做任何事情，因为 MySQL 默认必须修改密码之后才能操作数据库。

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
```

（9）、退出 MySQL。

```
exit;
```

（10）、开放外网访问端口。

1)、查看服务器的端口3306是否存在。

```
netstat -an|grep 3306
```

2)、修改配置文件。

```
vi /etc/my.cnf
```

添加如下配置：

代码语言：javascript

复制

```javascript
[mysqld]
port=3306
bind-address=0.0.0.0
```

 3)、重启。

mysql service mysql restart # 尝试访问，不成功的话继续操作。

4)、数据库设置修改。

登录 mysql。

```
mysql -u root -p
```

选择 [mysql 数据库](https://cloud.tencent.com/product/cdb?from_column=20065&from=20065)。

```
use mysql;
```

查看用户表信息。

```
select user,host from user;
```

假定 root 用户外网访问，更新 root 用户的 host 为 %，上面如果存在不需要更新。

```
update user set host='%' where user='root';
```

授权处理。

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root用户的密码' WITH GRANT OPTION;
flush privileges;
```

5)、重启 msql 尝试连接，如果不行的话，可能是防火墙的问题，继续操作。

防火墙设置 iptables为例

service iptable status // 查看防火墙状态

iptables -L -n –line-number |grep 3306 // –line-number 可以显示规则序号，在删除的时候比较方便

iptables -D INPUT 3 // 删除 input 的第3条规则

不存在3306的端口的话，开放3306

iptables -A INPUT -p tcp -m tcp –dport 3306 -j ACCEPT

再次查看3306端口.此时应该可以看到

iptables -L -n

service iptables save // 保存规则

service iptables restart // 重启

#### 5、配置 Redis 服务

（1）、新建文件夹。

```
mkdir /opt/redis
```

（2）、进入安装 redis 的位置。

```
cd /opt/redis/
```

（3）、利用 WinSCP 工具，将下载的压缩包上传到目录下。

（4）、然后进行解压命令，将压缩包进行解压，解压完成之后，执行删除命令删除压缩包。

A)、解压命令：`tar zxvf 压缩包名称`

```
tar zxvf redis-5.0.8.tar.gz
```

B)、删除命令：`rm -f 压缩包名称`

```
rm -f redis-5.0.8.tar.gz
```

（5）、打开文件路径。

```
cd /opt/redis/redis-5.0.8
```

（6）、编译。

```
yum -y install gcc gcc-c++ kernel-devel
make
```

（7）、启动。

```
./redis-server /opt/redis/redis-5.0.8/redis.conf
```

（8）、开启外网访问。

1)、配置 `redis.conf`。

```
vi /opt/redis/redis-5.0.8/redis.conf
```

将 bind 127.0.0.1 使用#注释掉，改为# bind 127.0.0.1（bind 配置的是允许连接的 ip，默认只允许本机连接；若远程连接需注释掉，或改为 0.0.0.0）

将 protected-mode yes 改为 protected-mode no（3.2之后加入的新特性，目的是禁止公网访问redis cache，增强 redis 的安全性）

将 requirepass foobared 注释去掉，foobared 为密码，也可修改为别的值（可选，建议设置）

2)、设置 iptables 规则，允许外部访问6379端口

```
iptables -I INPUT 1 -p tcp -m state --state NEW -m tcp --dport 6379 -j ACCEPT
```

（9）、添加开机启动服务。

```
vim /etc/systemd/system/redis-server.service
```

添加如下配置：

代码语言：javascript

复制

```javascript
[Unit]
Description=The redis-server Process Manager
After=syslog.target network.target

[Service]
Type=simple
PIDFile=/var/run/redis_6379.pid
ExecStart=/opt/redis/redis-5.0.8/src/redis-server /opt/redis/redis-5.0.8/redis.conf
ExecReload=/bin/kill -USR2 $MAINPID
ExecStop=/bin/kill -SIGINT $MAINPID

[Install]
WantedBy=multi-user.target
```

（10）、设置开机启动。

```
systemctl daemon-reload
systemctl start redis-server.service
systemctl enable redis-server.service
```

#### 6、配置 RabbitMQ 服务

（1）、下载 erlang 和 rabbitmq-server 的 rpm 文件。

http://www.rabbitmq.com/releases/erlang/erlang-19.0.4-1.el7.centos.x86_64.rpm

http://www.rabbitmq.com/releases/rabbitmq-server/v3.6.6/rabbitmq-server-3.6.6-1.el7.noarch.rpm

（2）、新建文件夹。

```
mkdir /opt/rabbitmq
```

（3）、进入安装 rabbitmq 的位置。

```
cd /opt/rabbitmq/
```

（4）、利用 WinSCP 工具，将下载的压缩包上传到目录下。

（5）、安装 erlang。

```
rpm -ivh erlang-19.0.4-1.el7.centos.x86_64.rpm
```

测试是否安装成功：

```
erl
```

（6）、安装 rabbitmq 依赖 socat。

```
yum install socat
```

（7）、安装 rabbitmq。

```
rpm -ivh rabbitmq-server-3.6.6-1.el7.noarch.rpm
```

（8）、启动和关闭。

service rabbitmq-server stop # 关闭

service rabbitmq-server start # 启动

service rabbitmq-server status # 状态

（9）、打开/sbin目录。

```
cd /usr/sbin
./rabbitmq-plugins list
./rabbitmqctl status
```

（10）、添加用户。

1)、运行如下的命令，增加用户admin，密码admin

```
./rabbitmqctl add_user 账号 密码
```

e：`./rabbitmqctl add_user admin admin`

2)、分配用户标签(admin为要赋予administrator权限的刚创建的那个账号的名字)

```
./rabbitmqctl set_user_tags admin administrator
```

3)、设置权限<即开启远程访问>(如果需要远程连接，例如java项目中需要调用mq,则一定要配置，否则无法连接到mq,admin为要赋予远程访问权限的刚创建的那个账号的名字，必须运行着rabbitmq此命令才能执行)

```
./rabbitmqctl set_permissions -p "/" admin ".*" ".*" ".*"
```

4)、开启Web管理插件。

```
./rabbitmq-plugins enable rabbitmq_management
```

（11）、测试是否安装成功。

使用浏览器打开：127.0.0.1:15672

登录用户名密码验证账户权限。

