Flyweight Pattern
=================

  享元模式(Flyweight)，运用共享技术有效地支持大量细粒度的对象。

###适用场景###

1. 如果一个系统中存在大量的相同或者相似的对象，由于这类对象的大量使用，会造成系统内存的耗费，可以使用享元模式来减少系统中对象的数量。
2. 对象的大部分状态都可以外部化，可以将这些外部状态传入对象中。

###优点###

1. 享元模式的优点在于它能够极大的减少系统中对象的个数
2. 享元模式由于使用了外部状态，外部状态相对独立，不会影响到内部状态，所以享元模式使得享元对象能够在不同的环境被共享

###缺点###

1. 由于享元模式需要区分外部状态和内部状态，使得应用程序在某种程度上来说更加复杂化了
2. 为了使对象可以共享，享元模式需要将享元对象的状态外部化，而读取外部状态使得运行时间变长

###UML结构图###

![Flyweight Pattern](http://ihongqiqu.com/imgs/post/FlyweightPattern.png)

###源码###

享元类的接口

```java
public interface Flyweight {

    public void operation(int id);

}
```

具体共享类

```java
public class ConcreteFlyweight implements Flyweight {

    @Override
    public void operation(int id) {
        System.out.println("具体Flyweight : " + id);
    }

}
```

不需要共享的享元具体实现类

```java
public class UnsharedConcreteFlyweight implements Flyweight {

    @Override
    public void operation(int id) {
        System.out.println("不共享的具体Flyweight : " + id);
    }

}
```

享元工厂，用来创建并管理Flyweight对象。

```java
public class FlyweightFactory {

    private HashMap<String, Flyweight> flyweights = new HashMap<String, Flyweight>();

    public FlyweightFactory() {
        flyweights.put("X", new ConcreteFlyweight());
        flyweights.put("Y", new ConcreteFlyweight());
        flyweights.put("Z", new ConcreteFlyweight());
    }

    public Flyweight getFlyweight(String key) {
        return flyweights.get(key);
    }
}
```

客户端调用

```java
public class Client {

    public static void main(String[] args) {
        int id = 20;

        FlyweightFactory flyweightFactory = new FlyweightFactory();

        Flyweight fx = flyweightFactory.getFlyweight("X");
        fx.operation(--id);

        Flyweight fy = flyweightFactory.getFlyweight("Y");
        fy.operation(--id);

        Flyweight fz = flyweightFactory.getFlyweight("Z");
        fz.operation(--id);

        UnsharedConcreteFlyweight unsharedConcreteFlyweight = new UnsharedConcreteFlyweight();
        unsharedConcreteFlyweight.operation(--id);

    }

}
```

