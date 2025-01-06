原文地址：https://cloud.tencent.com/developer/article/1457096





# Posix多线程编程



**一、线程与多线程的定义**

线程存在于进程当中，是操作系统调度执行的最小单位。说通俗点线程就是干活，多线程也就是同时可以干不同的活而且还不会互相打扰，线程并没有自己的独立空间。

**二、进程与线程的区别与联系**

 如果说进程是一个资源管家，负责从主人那里要资源的话，那么线程就是干活的苦力。

一个管家必须完成一项工作，就需要最少一个苦力，也就是说，一个进程最少包含一个线程，也可以包含多个线程。苦力要干活，就需要依托于管家，所以说一个线程，必须属于某一个进程。进程有自己的地址空间，线程使用进程的地址空间，也就是说，进程里的资源，线程都是有权访问的，比如说堆啊，栈啊，静态存储区什么的。

线程就是个无产阶级，但无产阶级干活，总得有自己的劳动工具吧，这个劳动工具就是栈，线程有自己的栈，这个栈仍然是使用进程的地址空间，只是这块空间被线程标记为了栈。每个线程都会有自己私有的栈，这个栈是不可以被其他线程所访问的。

从上面我们知道了进程和线程区别，使用多线程首先是要和进程相对比，它是一种非常便捷的多任务操作方式；我们知道，在Linux系统下，启动一个新的进程必须分配给它独立的地址空间，建立众多的数据表来维护它的代码段、堆栈段和数据段，这是一种"昂贵"的多任务工作方式。而运行于一个进程中的多个线程，它们彼此之间使用相同的地址空间，共享大部分数据，启动一个线程所花费的空间远远小于启动一个进程所花费的空间，而且，线程间彼此切换所需的时间也远远小于进程间切换所需要的时间。据统计，总的说来，一个进程的开销大约是一个线程开销的30倍左右，当然，在具体的系统上，这个数据可能会有较大的区别。对不同进程来说，它们具有独立的数据空间，要进行数据的传递只能通过通信的方式进行，这种方式不仅费时，而且很不方便。线程则不然，由于同一进程下的线程之间共享数据空间，所以一个线程的数据可以直接为其它线程所用，这不仅快捷，而且方便。当然，数据的共享也带来其他一些问题，有的变量不能同时被两个线程所修改，有的子程序中声明为static的数据更有可能给多线程程序带来灾难性的打击，这些正是编写多线程程序时最需要注意的地方。

线程操作相关的函数：

**(1)线程创建函数**

代码语言：javascript

复制

```javascript
1int pthread_create(pthread_t *tid, const pthread_attr_t *attr, void *(*func) (void *), void *arg);
```

参数说明：

pthread_create用于创建一个线程，成功返回0，否则返回Exxx（为正数）。

pthread_t *tid：线程id的类型为pthread_t，通常为无符号整型，当调用pthread_create成功时，通过*tid指针返回。

const pthread_attr_t *attr：指定创建线程的属性，如线程优先级、初始栈大小、是否为守护进程等。可以使用NULL来使用默认值，通常情况下我们都是使用默认值。

void *(*func) (void *)：函数指针func，指定当新的线程创建之后，将执行的函数。

void *arg：线程将执行的函数的参数。如果想传递多个参数，请将它们封装在一个结构体中。

**(2)线程等待的函数**

代码语言：javascript

复制

```javascript
1int pthread_join (pthread_t tid, void ** status);
```

参数说明：

pthread_join用于等待某个线程退出，成功返回0，否则返回Exxx（为正数）。

pthread_t tid：指定要等待的线程ID。

void ** status：如果不为NULL，那么线程的返回值存储在status指向的空间中（这就是为什么status是二级指针的原因！这种才参数也称为“值-结果”参数）。

**(3)获得线程自身的ID的函数**

代码语言：javascript

复制

```javascript
1pthread_t pthread_self (void);
```

pthread_self用于返回当前线程的ID。

**(4)线程分离的函数**

代码语言：javascript

复制

```javascript
1int pthread_detach (pthread_t tid);
```

pthread_detach用于是指定线程变为分离状态，就像进程脱离终端而变为后台进程类似。成功返回0，否则返回Exxx（为正数）。变为分离状态的线程，如果线程退出，它的所有资源将全部释放。而如果不是分离状态，线程必须保留它的线程ID，退出状态直到其它线程对它调用了pthread_join。

**(5)退出线程(终止线程)的函数**

代码语言：javascript

复制

```javascript
1void pthread_exit (void *status);
```

pthread_exit用于终止线程，可以指定返回值，以便其他线程通过pthread_join函数获取该线程的返回值。

参数说明：

void *status：指针线程终止的返回值。

Linux内核只提供了轻量进程的支持，限制了更高效的线程模型的实现，但Linux着重优化了进程的调度开销，一定程度上弥补了这一缺陷。目前最为流行的线程机制LinuxThreads所采用的就是线程-进程“一对一”模型，调度交给核心，而在用户级实现一个包括信号处理在内的线程管理机制。

**线程编程实例：pthread.c**

代码语言：javascript

复制

```javascript
 1#include <stdio.h>
 2#include <string.h>
 3#include <stdlib.h>
 4#include <unistd.h>
 5#include <pthread.h>
 6void *thread_1(void *arg)
 7{
 8    printf("thread one\n");
 9}
10void *thread_2(void *arg)
11{
12    printf("thread two\n");
13}
14int main()
15{
16    int ret = 0;
17    pthread_t pid = 0;
18pthread_t pid1 = 0;
19    //创建线程1
20    ret = pthread_create(&pid, NULL, thread_1, NULL);
21    if(ret < 0)
22    {
23        perror("pthread_create");
24        exit(EXIT_FAILURE);
25    }
26    //创建线程2
27    ret = pthread_create(&pid1, NULL, thread_2, NULL);
28    if(ret < 0)
29    {
30        perror("pthread_create");
31        exit(EXIT_FAILURE);
32    }
33    //等待线程退出
34    pthread_join(pid, NULL);
35    pthread_join(pid1, NULL);
36    return 0;
37}
```

注意，在gcc中，默认是不包含线程相关的库的，所以在编译这个程序操作如下是会产生错误的，如图4-3-25所示。

![img](https://ask.qcloudimg.com/http-save/yehe-5745070/534b9xbd91.jpeg)

​        图4-3-25 gcc编译中没有包含线程库的验证结果

 正确的编译方式是下面这样，要加上-lpthread这个库，确保编译的时候链接上。如图4-3-26所示。

![img](https://ask.qcloudimg.com/http-save/yehe-5745070/kqj96c2jk9.png)

 图4-3-26 创建线程

运行结果，如图4-3-27所示。

![img](https://ask.qcloudimg.com/http-save/yehe-5745070/cacazwclbg.png)

 图4-3-27 创建线程的实验结果

pthread.c创建了2个线程，并在线程中实现打印功能，最终调用pthread_join等待子线程运行结束，一并退出。

通过上面的一个例程会发现一个问题，当我们去操作一个文件的时候会出现一个问题，就是不知道该听谁的，这时候我们就需要一个互斥锁，让线程一个个来，a执行完之后在执行b。

**互斥锁例程：pthread2.c**

代码语言：javascript

复制

```javascript
 1#include <stdio.h>
 2#include <string.h>
 3#include <stdlib.h>
 4#include <unistd.h>
 5#include <pthread.h>
 6//定义一个互斥锁变量
 7pthread_mutex_t m;
 8void *thread_1(void *arg)
 9{
10    //互斥锁加锁
11    pthread_mutex_lock(&m);
12    printf("thread one\n");
13    //互斥锁解锁
14    pthread_mutex_unlock(&m);
15}
16void *thread_2(void *arg)
17{
18    pthread_mutex_lock(&m);
19    printf("thread two\n");
20    pthread_mutex_unlock(&m);
21}
22int main()
23{
24    int ret = 0;
25    //以动态方式创建互斥锁
26    ret = pthread_mutex_init(&m, NULL);
27    if(ret < 0)
28    {
29        perror("pthread_mutex_init");
30        exit(EXIT_FAILURE);
31    }
32    pthread_t pid = 0;
33    pthread_t pid1 = 0;
34    ret = pthread_create(&pid, NULL, thread_1, NULL);
35    if(ret < 0)
36    {
37        perror("pthread_create");
38        exit(EXIT_FAILURE);
39    }
40    ret = pthread_create(&pid1, NULL, thread_2, NULL);
41    if(ret < 0)
42    {
43        perror("pthread_create");
44        exit(EXIT_FAILURE);
45    }
46    pthread_join(pid, NULL);
47    pthread_join(pid1, NULL);
48    return 0;
49}
```

一样的，同样执行编译加上-lpthread参数保证编译时链接线程库，然后运行，如图4-3-28所示。

![img](https://ask.qcloudimg.com/http-save/yehe-5745070/4cctmwpxrl.png)

 图4-3-28 添加互斥锁测试

线程安全就是多线程访问时，采用了加锁机制，当一个线程访问该函数的某个数据时，进行保护，其它线程不能进行访问直到该线程读取完成，其它线程才可以使用。不会出现数据不一致或者数据污染。
