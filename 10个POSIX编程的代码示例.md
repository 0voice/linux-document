

# POSIX编程的代码示例



以下是10个Linux POSIX编程的代码示例，涵盖了线程、进程间通信和文件操作等多个方面。每个示例都附带简要说明。

### 1. 创建线程

```
#include <pthread.h>
#include <stdio.h>

void* threadFunction(void* arg) {
    printf("Hello from thread!\n");
    return NULL;
}

int main() {
    pthread_t thread;
    pthread_create(&thread, NULL, threadFunction, NULL);
    pthread_join(thread, NULL);
    return 0;
}
```

### 2. 使用信号量

```
#include <semaphore.h>
#include <pthread.h>
#include <stdio.h>

sem_t semaphore;

void* worker(void* arg) {
    sem_wait(&semaphore);
    printf("In critical section\n");
    sem_post(&semaphore);
    return NULL;
}

int main() {
    pthread_t thread1, thread2;
    sem_init(&semaphore, 0, 1);
    
    pthread_create(&thread1, NULL, worker, NULL);
    pthread_create(&thread2, NULL, worker, NULL);

    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);
    
    sem_destroy(&semaphore);
    
    return 0;
}
```

### 3. 条件变量

```
#include <pthread.h>
#include <stdio.h>

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

void* producer(void* arg) {
   // produce something
   pthread_cond_signal(&cond); 
   return NULL;
}

void* consumer(void* arg) {
   pthread_cond_wait(&cond, &mutex); 
   printf("Consumed an item\n");
   return NULL;
}

int main() {
   pthread_t p_thread, c_thread;

   pthread_create(&p_thread, NULL, producer, NULL);
   pthread_create(&c_thread, NULL, consumer, NULL);

   pthread_join(p_thread, NULL);
   pthread_join(c_thread,NULL);

   return 0;
}
```

### 4. 使用共享内存

```
#include <sys/mman.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int fd = shm_open("/my_shm", O_CREAT | O_RDWR | O_EXCL , S_IRUSR | S_IWUSR);
    
	// Set size of shared memory object
	ftruncate(fd , sizeof(int));

	int *ptr = mmap(0,sizeof(int),PROT_READ | PROT_WRITE , MAP_SHARED , fd , 0 );
	
	*ptr = 42; // Write to shared memory

	munmap(ptr , sizeof(int));
	close(fd);  
	shm_unlink("/my_shm"); // Clean up

	return 0; 
}
```

### 5. 管道示例

```
#include <unistd.h>
#include <stdio.h>

int main() {
     int fd[2];
     pipe(fd);

     if (fork() == 0) { // Child process
         close(fd[1]); // Close writing end in child.
         char buffer[20];
         read(fd[0], buffer , sizeof(buffer)); 
         printf("Child received: %s\n", buffer); 
     } else { // Parent process
         close(fd[0]); // Close reading end in parent.
         const char *msg = "Hello from parent!";
         write(fd[1], msg , strlen(msg)+1); 
     }
     
     return 0;  
}
```

### 6. 文件I/O操作示例

```
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
	int fd = open("example.txt", O_CREAT | O_WRONLY | O_TRUNC , S_IRUSR | S_IWUSR);

	const char *text = "Hello POSIX!";
	write(fd , text , strlen(text)); 

	close(fd);   
	return 0; 
}
```

### 7. 定时器使用示例

```
#define _POSIX_C_SOURCE 199309L

#include <time.h>
#include <signal.h>
#include <stdio.h>

void timer_handler(int signum) {
	printf("Timer expired!\n");
}

int main() {
	struct sigaction sa;
	struct itimerspec timer;

	sa.sa_handler = timer_handler;
	sigaction(SIGRTMIN + 1,&sa,NULL);

	timer.it_value.tv_sec = 2;       // First expiration after two seconds.
	timer.it_value.tv_nsec = 0;
	timer.it_interval.tv_sec = 2;     // Subsequent expiration every two seconds.
	timer.it_interval.tv_nsec = 0;

	timer_settime(timerid , TIMER_ABSOLUTE &timer );

	while(1){ /* Do other work */ }

	return(0); 
}
```

### 8. 消息队列示例（System V）

```
#include<sys/ipc.h>     
#include<sys/msg.h>     
#define MSG_SIZE sizeof(struct msgbuf)-sizeof(long)

struct msgbuf{
	long mtype;      
	char mtext[100];   
};

int main()
{
	int msqid=msgget(IPC_PRIVATE|0666|IPC_CREAT);  
	struct msgbuf message;

	message.mtype=1;     
	strcpy(message.mtext,"hello world");     

	msgsnd(msqid,&message,msg_size(),IPC_NOWAIT);

	msgrcv(msqid,&message,msg_size(),msgtype(1),MSG_NOERROR);


	return(0);   
} 
```

### 9. fork 示例程序：

```
 #include<stdio .h >  
 #include<unistd .h >  

 int main (){  
 pid_t pid=fork();  

 if(pid== -1 ){  
 perror ("Error forking");  
 }else if(pid== 0 ){  
 printf ("Child Process ID: %d \n ",getpid());   
 }else{  
 printf ("Parent Process ID: %d \n ",getpid());   
 wait(NULL ); 
 }   

 return (EXIT_SUCCESS );  
}  
```

### 10. 获取当前进程ID和父进程ID：

```
 #include<stdio .h >

 int main (){  

 pid_t pid=getpid ();    
 pid_t ppid=getppid ();  

 printf ("Current Process ID : %d \n ",pid );   
 printf ("Parent Process ID : %d \n ",ppid );   

return (EXIT_SUCCESS );  
} 
```

以上代码展示了不同的POSIX编程技巧，你可以根据需要进行扩展和修改。确保在适合的环境中测试这些代码，并检查相关头文件及库的依赖。希望这些对你学习POSIX编程有所帮助！

