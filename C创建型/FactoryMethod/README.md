# Factory Method(工厂方法模式)    ---- 对象创建型模式

工厂方法指的是一个专门用于创建对象的接口，方法即接口，"接口"在不同语言里的理解稍微不同，比如(知识面太窄，仅是举例)，C/C++里指的是函数，函数可以单独写，也可以是类中的函数。我认为只要是用于创建对象的功能都能比拟成工厂方法。

工厂方法的好处是很多的，通常用于框架和库中，它隐藏了创建对象的过程及细节，调用工厂方法的时候只知道返回的是个想要的对象，这个对象怎么实现、涉及到哪些类，一般是不清楚的。举个例子，去4S店提车时只知道提到的是辆车，虽然部分车零件是看得见的，但是大部分还是不清楚的，怎么组装的也不知道，我们也不关心，因为我们最终是想开车，而不是修车，细节的事情交给厂家(框架or库)去做。

工厂方法很好理解，但是工厂方法模式就不仅仅是说"用一个接口来创建对象"了，**模式**提供了工厂方法的一般实现模型。为了扩展性，通常具体工厂类都继承自一个抽象工厂类。




典型实现
-----

```
// 工厂抽象类
class Creator
{
public:
    virtual ThingA *CreateThingA();
    virtual ThingB *CreateThingB();
}

// 工厂具体类
class ConreteCreator: public Creator
{
public:
    virtual ThingA *CreateThingA();
    virtual ThingB *CreateThingB();
}
```


这只是很简单的实现，产品类ThingA、ThingB的设计不是关心的点。



注意
-----

1、工厂方法可以有多个吗？

工厂方法可以有多个，一个类中可以编写无数个工厂方法，如果需要的话。


2、一定要用虚函数吗？

工厂方法是个思想，C++一般用虚函数实现，如果你只想写几个工厂方法而不写类，可以的，扩展起来难而已。虚函数是很常用的实现方式。


3、一个工厂可以生产多种不同产品吗？

可以的，建议一个工厂只生产有关联的产品，比如汽车厂就只生产各种汽车配件。


4、一个汽车厂可以同时生产成品车和汽车配件吗？

可以的，这样的设计合理。


5、一个工厂方法可以生产多种产品吗？

可以的，如果产品实在太多了，而且构造起来也比较简单的时候，建议使用。用参数来区别应该返回的产品即可。


6、产品类应该怎么设计？

这和"工厂"无关，但是建议设计合理一点，否则扩展起来就很难，代码难复用。


7、工厂具体类太多了怎么办？

检查一下是不是粒度上的把控有问题，如果工厂的逻辑都是一样的，仅仅是生产的产品不同，那就用模板类，可以避免创建过多的具体类。比如生产果蓝的工厂，都是将水果包装起来卖，包装苹果还是香蕉都是一个逻辑，那就将果蓝工厂做成模板类就行了。


