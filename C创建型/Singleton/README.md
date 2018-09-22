# Singleton(单例模式)    ---- 对象创建型模式

单例是指唯一存在的一个实例，比如一个类只能实例化一个对象，系统中只能有一个init进程。单例模式比较好理解，使用频率也很高。

单例进程非常常见，服务器进程通常需要监听一些端口，处理一些服务，单例进程可以保证不会有奇奇怪怪的事出现，比如避免文件的读写乱序等。

单例模式的重点在于实现，毕竟优雅的实现方式不多，我们的目的是禁止创建多个对象，不是说写个注释就算了，是要从技术上去限制它。看看下面这个比较优雅实现。



典型实现
-----

**对象单例**

```
class Singleton
{ 
public:
    static Singleton &getInstance()
    {       
        static Singleton instance;
        return instance;
    }
private:
    Singleton() {} 	//构造函数
    Singleton(const Singleton &);	//拷贝构造函数
    void operator=(Singleton const &);	//重载赋值运算符
};

int main()
{
    Singleton &obj = Singleton::getInstance();
    return 0;
}
```


- 构造函数，拷贝构造函数都声明为私有，这样就创建多余的S实例。
- getInstance()接口被声明为static，因此无需实例化即可调用它，如S &a = S::getInstance()。
- 通过getInstance()得到的S实例均是同一个，因为instance被声明为static了。
- 拷贝构造函数和重载赋值运算符这两个函数仅声明，不要实现！
- 这种写法在C++11标准中是线程安全的(GCC4.3支持)，在之前的标准中就不一定了,自己加锁去！



**进程单例**

```
int lockfile(int fd) 
{
    struct flock flk;

    flk.l_type = F_WRLCK;
    flk.l_start = 0;
    flk.l_whence = SEEK_SET;
    flk.l_len = 0;
    return fcntl(fd, F_SETLK, &flk);
}

int main()
{
    int fd = open("/var/run/test.pid", O_RDWR | O_CREAT, 0644);
    if (lockfile(fd) < 0) {
        if (errno == EACCES || errno == EAGAIN) {
            // 已经有进程在运行了
        } else {
            // 其他错误，请检查
        }
    }
    // 成功上锁
    // 逻辑代码
    return 0;
}
```

进程单例也是很见的，通常是通过对某个文件进行加锁，这样后来的进程就没法进行加锁，自然就运行不了。这个锁会在进程死亡之后释放，所以不用担心进程异常退出问题。

