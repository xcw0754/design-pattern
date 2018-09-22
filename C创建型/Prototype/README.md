# Prototype(原型模式)    ---- 对象创建型模式

原型指的是一个类实例，也就是对象，它的各项属性都是默认的，一般不会对它进行太多变动。通过克隆原型来创建对象就是原型模式的思想。

试想一下，一个比较庞大的类，在创建它的时候需要很多行代码，它的属性有上百个，但是常用的只有其中的十来个，这个时候，通过new来创建对象就繁琐了点。如果有一个默认的对象，通过clone来创建对象就方便了，clone完之后修改一下其中少部分属性就能用了。代码复杂度就可以降下来了。

使用场景其实挺多的，比如英雄联盟的一场王者峡谷比赛用一个对象来表示，地图是一样的，地图上的河蟹、大小龙、小兵都是一样的，只是10只英雄可能不同，这时候可以程序运行起来就创建一场默认比赛，随便塞10个英雄，每次新局就clone这个对象，做微量修改就能用了。

原型模式讲的是一种思想，至于怎么clone见仁见智，选择合适的方式来clone就好了。要实现clone就得考虑的多了，深拷贝或是浅拷贝？全局函数还是成员函数？什么情况允许拷贝？用完后对象怎么销毁？



典型实现
-----

```
class Prototype
{
public:
    virtual Prototype *clone() = 0;
};
 
class ConcretePrototype: public Prototype
{
public:
    virtual Prototype *clone();
};
 
ConcretePrototype *Default = new ConcretePrototype();

int main()
{
    for (int i = 0; i < 10; i++) {
        ConcretePrototype *newone = Default.clone();
        modify newone;
        use newone;
    }
    return 0;
}
```


类Protype是抽象类，继承它的类必须实现clone。
