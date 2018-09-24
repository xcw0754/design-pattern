# Composite(组合模式)    ---- 结构型模式

回忆一下，Linux的文件系统使得我们可以像操作文件一样来操作目录(当然的，不能cd，这里说的是大部分情况下)，移动、拷贝、删除等等都公共的操作，它有一个特点，那就是目录结构是树形结构。谈到这里组合模式就是这样的东西，用于表示"部分-整体"这样的树形结构非常适合。

什么是组合模式?如下图一样，应该有一个定义了公共接口的基类Component，其应有一至多个叶子节点类Leaf，还有一个分支节点类Composite。这里可以将分支节点类想象作目录，而叶子节点类想象作不同的文件(Linux的文件种类很多)。而且Component通常有Add、Remove、GetChild等操作。


![组合模式UML](https://github.com/xcw0754/PPL/blob/master/UML/uml-composite-20180924.png)



实现
-----

**类的定义**

```
class Component
{
public:
    virtual void Operation()=0;    

    virtual void Add(Component*);
    virtual void Remove(Component*);
    virtual Component* GetChild(int idx);
};

class Leaf: public Component
{
public:
    virtual void Operation();            
};

class Composite: public Component
{
public:
    void Operation();
    void Add(Component*);
    void Remove(Component*);
    Component* GetChild(int index);
private:
    list<Component*> component;
};
```


**逻辑代码**


```
int main()
{
    Composite* node = new Composite();
    node->Add(new Leaf());
    node->Add(new Leaf());

    Composite* root = new Composite();
    root->Add(node);
    root->Add(new Leaf());

    root->operation();
    return 0;
}
```
