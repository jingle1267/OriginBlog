Bridge Pattern
==============

  桥接模式(Bridge)，将抽象部分与它的实现部分分离，使它们都可以独立地变化。优先使用对象的合成/聚合将有助于你保持每个类被封装，并被集中在单个任务上。这样类和类继承层次会保持较小规模，并且不太可能增长为不可控制的庞然大物。

###适用场景###
1. 当一个对象有多个变化因素的时候，通过抽象这些变化因素，将依赖具体实现，修改为依赖抽象。
2. 当某个变化因素在多个对象中共享时。我们可以抽象出这个变化因素，然后实现这些不同的变化因素。
3. 当我们期望一个对象的多个变化因素可以动态的变化，而且不影响客户的程序的使用时。

###优点###
1. 分离抽象和实现部分
2. 更好的扩展性
3. 可动态地切换实现
4. 可减少子类的个数

###缺点###
1. 桥接模式的引入会增加系统的理解与设计难度，由于聚合关联关系建立在抽象层，要求开发者针对抽象进行设计与编程。 
2. 桥接模式要求正确识别出系统中两个独立变化的维度，因此其使用范围具有一定的局限性。

###UML结构图###
![BridgePattern](https://94275.cn/imgs/post/BridgePattern.png)

###源码###
Implementor:实现接口
```java
/**
 * 实现接口
 *
 * Created by zhenguo on 12/8/14.
 */
public interface Implementor {

    public void operation();

}
```

ConcreteImplementorA:实现派生类A
```java
/**
 * 实现派生类A
 *
 * Created by zhenguo on 12/8/14.
 */
public class ConcreteImplementorA implements Implementor {
    @Override
    public void operation() {
        System.out.println("具体实现A的方法执行");
    }
}
```

ConcreteImplementorB:实现派生类B
```java
/**
 * 实现派生类B
 *
 * Created by zhenguo on 12/8/14.
 */
public class ConcreteImplementorB implements Implementor {
    @Override
    public void operation() {
        System.out.println("具体实现B的方法执行");
    }
}
```

Abstraction:抽象类
```java
/**
 * 抽象类
 *
 * Created by zhenguo on 12/8/14.
 */
public abstract class Abstraction {

    protected Implementor implementor;

    public void setImplementor(Implementor implementor) {
        this.implementor = implementor;
    }

    public abstract void operation();

}
```

RefinedAbstraction:抽象实现子类
```java
/**
 * 抽象实现子类
 *
 * Created by zhenguo on 12/8/14.
 */
public class RefinedAbstraction extends Abstraction {
    @Override
    public void operation() {
        if (implementor != null) {
            implementor.operation();
        }
    }
}
```

Client:客户端调用
```java
/**
 * 客户端调用
 * 桥接模式(Bridge)，将抽象部分与它的实现部分分离，使它们都可以独立地变化。
 *
 * Created by zhenguo on 12/8/14.
 */
public class Client {

    public static void main(String[] args) {
        Abstraction abstraction = new RefinedAbstraction();

        abstraction.setImplementor(new ConcreteImplementorA());
        abstraction.operation();

        abstraction.setImplementor(new ConcreteImplementorB());
        abstraction.operation();

    }

}
```
