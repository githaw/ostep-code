第27章：线程api
-------------


**永远不要在线程函数里面返回一个指针。**

原因在于，线程函数中的指代存放在线程的栈中，当执行该函数的return时，该线程的栈会被释放

不过现在的编译器会把这些问题识别出来，标志为error
```
thread_create_with_return_args_danger.c: In function ‘mythread’:
thread_create_with_return_args_danger.c:29:12: error: function returns address of local variable [-Werror=return-local-addr]
     return (void *)&r;
            ^~~~~~~~~~
cc1: all warnings being treated as errors
```
------------

