# Proxy(代理模式)    ---- 结构型模式

代理的概念很容易被理解，像Http代理、Socks代理、Nginx代理的思想一样，就是完成被代理者做该做的事之外还要实现一些额外的功能，例如权限控制。

拿Nginx来说，它可以只是web服务器的一个代理软件，它本身不实现任何业务逻辑，但是它有个功能，那就是权限限制，它规定了哪些资源不允许访问，哪些资源可以访问。为什么要有Nginx的诞生呢？如果没有Nginx这个角色的话，我觉得web服务器也可能会因为权限问题而一团糟，任何开放的端口都要先检查一堆权限然后才开始执行业务逻辑，而且还很难维护。有了Nginx之后，web服务器就只需要专心完成业务逻辑，不用去管什么权限问题，来访者必定是有权限的，没权限的早就被Nginx档掉了。


代理模式的一个简单例子如下图

![代理模式UML](https://github.com/xcw0754/PPL/blob/master/UML/uml-proxu-20180924.jpg)



```
public Image
{
public:
    virtual void display();
}

public RealImage: public Image
{
public:
    virtual void display();
    void loadFromDist();
private:
    string filename;
}

public ProxyImage: public Image
{
public:
    virtual void display();
private:
    RealImage realimage;
    String filename;
}
```


这里的ProxyImage类和RealImage类一样，都继承自Image类，但是业务逻辑代码(即main函数)不应该直接使用RealImage类，而应该使用ProxyImage类。ProxyImage的接口实现就可以在RealImage类的基础上包装一些控制逻辑了，这样设计能让控制逻辑分离出来，随时可以撤掉而不会对现有业务逻辑产生大影响。
