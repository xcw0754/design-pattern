# BUILDER(生成器模式)    ---- 对象创建型模式

假设有一些库可以用，我们主要写如下CreateMaze函数就可以创建一个迷宫。这种代码在安卓开发中比较常见，比如点击一下"新建"按钮就可以创建一个迷宫。迷宫的组合是千变万化的，但是基本的组成部分是比较固定的，比如房间、门等等。

```
Maze* CreateMazeA(MazeBuilder& builder)
{
    // 随意组合，最后的目的是创建一个Maze
    builder.BuildRoom(1);
    builder.BuildRoom(2);
    builder.BuildDoor(1, 2);

    return builder.GetMaze();
}

Maze* CreateMazeB(MazeBuilder& builder)
{
    // 随意组合，最后的目的是创建一个Maze
    builder.BuildRoom(1);
    builder.BuildRoom(2);
    builder.BuildRoom(3);
    builder.BuildRoom(4);
    builder.BuildRoom(5);

    return builder.GetMaze();
}
```


上面的builder就是生成器，用于生成一个迷宫。但是迷宫是什么样子的，这需要我们来设计，这部分代码最经常变动，通常就是把不经常变动的逻辑抽出来，作为builder。


注意
-----

1、想要增加迷宫的部件(如墙)该怎么做？

在MazeBuilder类中新增墙这种元素(元素可以是个类、数组、字符串，随便发挥)，写个CreateMazeC就行了。


2、MazeBuilder应该怎样设计？

这不是生成器模式所关心的点，MazeBuilder可以用工厂方法等思想实现，各种高端技术一顿乱操作，随意发挥，能生产迷宫部件就行。


3、为什么CreateMazeX只是个函数？

将所有的CreateMazeX函数设计成一个类也是可以的，这不是生成器模式所关心的点。如果将所有的CreateMazeX函数设计成一个类，那这个类也可以称为工厂类了，里面的CreateMazeX函数都是工厂方法。
