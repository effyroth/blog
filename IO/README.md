BIO select/poll epoll AIO

概念点：block/nonblock sync/async ready

BIO流程：
  进程等待单个fd读写方法调用返回
  用户态等待内核态
  内核态等待fd ready

select/poll流程：
  进程调用select方法，参数传入fd_set（fd列表），等待返回
  内核态遍历fd_set，返回ready fds
  进程对fds进行读写方法调用

epoll流程：
  进程创建epoll fd
  进程注册读写fds到epoll（内部红黑树结构）
  进程调用epoll_wait等待返回
  返回ready fds events（内部链表结构），或者sleep直到fd ready事件（系统中断）触发epoll callback唤醒或超时返回
  进程对fds进行读写方法调用
  进程注销读写结束的fds

aio流程：
  进程调用参数传入fd和callback函数，不等待返回
  eventloop进程（IOCP）loop fds，调用callback
