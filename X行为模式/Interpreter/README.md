# Interpreter(解释器模式)    ---- 行为型模式

解释器模式适合解析简单的表达式，比如逻辑表达式。解释器模式的原理就是利用类来解析表达式，可以创建一个表达式基类，然后有一个共有的操作interpret()来求表达式的值，子类用于解释各种指定的表达式。所需角色如下图:


![解释器模式UML](https://github.com/xcw0754/PPL/blob/master/UML/uml-interpreter-20180926.png)


假设我们要求如下的逻辑表达式的值。

`(true and x) or (y and (not x))`


再假设类都已经设计好了，有BooleanExp、Context、VariableExp、OrExp、AndExp、Constant、NotExp，则可以像下面这样来求表达式的值。
```
BooleanExp *exp;
Context context;

VariableExp *x = new VariableExp("X")
VariableExp *y = new VariableExp("Y")

exp = new OrExp(
        new AndExp(new Constant(true), x), 
        new AndExp(y, new NotExp(x))
        );

context.Assign(x, false);
context.Assign(y, true);

bool result = exp->Evaluate(context);
```

感觉这几行代码很神奇，这类设计的很漂亮才能这样。解释器模式不适合复杂的表达式，否则类的设计非常复杂，稍有不慎就坑人了。也不适合需求经常变化的表达式，否则类会越来越多。
