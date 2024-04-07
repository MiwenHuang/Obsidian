## IO多路复用

允许单个进程能够同时处理多个IO事件的机制。

## epoll
先用`epoll_create`创建一个`epoll`对象`epfd`，再通过`epoll_ctl`将需要监视的`socket`添加到`epfd`中，最后调用`epoll_wait`等待数据
```C++
int s = socket(AF_INET, SOCK_STREAM, 0);
bind(s, ...);
listen(s, ...)

int epfd = epoll_create(...);
epoll_ctl(epfd, ...); //将所有需要监听的socket添加到epfd中

while(1) {
    int n = epoll_wait(...);
    for(接收到数据的socket){
        //处理
    }
}
```

epoll通过两个方面实现高并发

1. epoll在内核中使用红黑树来跟踪进程所有待检测的文件描述符，将需要监控的socket通过epoll_ctl函数加入内核中的红黑树里，红黑树是一个高效的数据结构，增删改一般时间复杂度是O(logn)。

2. epoll使用事件驱动机制，内核里维护了一个链表来记录就绪事件，当某个socket有事件发生时，通过回调函数内核会将其加入到这个就绪事件列表中，当用户调用epoll_wait函数时，只会返回有事件发生的文件描述符的个数，不需要像select/poll那样轮询扫描整个socket集合，大大提高了检测效率

![[Pasted image 20240321170251.png]]

## 边缘触发和水平触发

- 使用边缘出发模式的时候，当被监控的Socket描述符有可读写事件时，服务端只会从epoll_wait中苏醒一次，即使进程没有调用read函数从内核读取数据，也依然只塑形一次，因此我们程序要保证一次性将内核缓冲区的数据读完

- 使用水平触发模式时，当被监控的Socket上有可读事件发生时，服务端不断地从epoll_wait中苏醒，直到内核缓冲区被read函数读完才结束，目的是告诉我们有数据需要读取

