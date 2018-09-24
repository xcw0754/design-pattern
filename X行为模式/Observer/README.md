# Observer(观察者模式)    ---- 行为型模式

观察者模式用于解决一对多的场景，即一个对象的状态改变时，其他感兴趣的对象能收到通知，有点像订阅博客。观察者模式的思想很多地方都有用到，经典场景就是注册感兴趣的事件，然后通过回调来告知。这种模式确实很方便很好用，不过还是得了解一下基本的设计方法。

注册回调，一般还要提供优先级，这样才能解决逻辑先后顺序的问题，实现方式很多样也比较简单。还有一个是防止死循环，设想一下，在事件A触发时，其中一个回调中执行了一个很久的循环，然后还dispatch一个其他事件B，然后监听事件B的回调中又dispatch一个事件A，这样就开始无限的循环了。防止死循环的设计方式可以定个规则，延迟dispatch直到到空闲时才开始执行，这样就能保证当前的事件回调都能执行完，还可以记录嵌套的深度，在超过一定量时强制退出，记录下来供日后分析CPU持续飙高的原因。

常见的观察者模式都是设计成单线程的，规模控制起来简单。如果有意深入了解，可以拿libev的源码看一看。下面的逻辑代码就用的libev框架。



```
void stdin_readable_cb(struct ev_loop *loop, ev_io *w, int revents)
{
    char buf[64] = {0};
    read(w->fd, buf, sizeof(buf) - 1);
    printf("%s\n", buf);
}

int main()
{
    struct ev_loop *loop = EV_DEFAULT;
    ev_io stdin_readable;

    ev_io_init(&stdin_readable, stdin_readable_cb, STDIN_FILENO, EV_READ);
    // 注册回调，监听标准输入事件
    ev_io_start(loop, &stdin_readable);

    ev_run(loop, 0);
    return 0;
}
```
