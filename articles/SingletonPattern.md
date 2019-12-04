Singleton Pattern
=================

  单例模式(Singleton)，保证一个类仅有一个实例，并提供一个访问它的全局访问点。

  通常我们可以让一个全局变量使得一个对象被访问，但它不能防止你实例化多个对象。一个最好的的办法就是，让类自身负责保存它的唯一实例。这个类可以保证没有其他实例可以被创建，并且它可以提供一个访问该实例的方法。

###适用场景###

  当某个对象只能存在一个实例的情况下使用单例模式；

###优点###
1. 提供了对唯一实例的受控访问。
2. 由于在系统内存中只存在一个对象，因此可以节约系统资源，对于一些需要频繁创建和销毁的对象单例模式无疑可以提高系统的性能。

###缺点###
1. 由于单利模式中没有抽象层，因此单例类的扩展有很大的困难。
2. 单例类的职责过重，在一定程度上违背了“单一职责原则”。

###UML结构图###
![SingletonPattern](https://94275.cn/imgs/post/SingletonPattern.png)

###源码###
SingletonA：饿汉是单例类
```java
/**
 * 单例设计模式中的饿汉式
 *
 * Created by zhenguo on 12/5/14.
 */
public class SingletonA {

    private static SingletonA instance = new SingletonA();

    private SingletonA() {
    }

    public static SingletonA getInstance() {
        return instance;
    }
}
```

SingletonB：懒汉是单例类
```java
/**
 * 单例设计模式中的懒汉式
 *
 * Created by zhenguo on 12/5/14.
 */
public class SingletonB {

    private static SingletonB instance = null;

    private SingletonB() {
    }

    public static synchronized SingletonB getInstance() {
        if (instance == null) {
            instance = new SingletonB();
        }
        return instance;
    }
}
```

Client：客户端调用
```java
/**
 * 单例模式客户端调用
 * 简单说来，单例模式（也叫单件模式）的作用就是保证在整个应用程序的生命周期中，
 * 任何一个时刻，单例类的实例都只存在一个（当然也可以不存在）。
 *
 * Created by zhenguo on 12/5/14.
 */
public class Client {

    public static void main(String[] args) {
        // 饱汉实现方式
        SingletonA singletonA1 = SingletonA.getInstance();
        SingletonA singletonA2 = SingletonA.getInstance();
        if (singletonA1 == singletonA2) {
            System.out.println("singletonA1和singletonA2是一个对象");
        } else {
            System.out.println("singletonA1和singletonA2不是一个对象");
        }

        // 饿汉实现方式
        SingletonB singletonB1 = SingletonB.getInstance();
        SingletonB singletonB2 = SingletonB.getInstance();
        if (singletonB1 == singletonB2) {
            System.out.println("singletonB1和singletonB2是一个对象");
        } else {
            System.out.println("singletonB1和singletonB2不是一个对象");
        }

        // 更方便的实现方式 待续...
    }

}
```
