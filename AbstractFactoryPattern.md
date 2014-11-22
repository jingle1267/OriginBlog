抽象工厂
========

###设计原则###
1. 开闭原则：对扩展开放，对修改关闭。
2. 里氏替换：主张使用“抽象(Abstraction)”和“多态(Polymorphism)”将设计中的静态结构改为动态结构，维持设计的封闭性。

###适用场景###
  抽象工厂模式特别适合于这样的一种产品结构：产品分为几个系列，在每个系列中，产品的布局都是要同的，在一个系列中某个位置的产品，在另一个系列中一定有一个对应的产品。这样的产品结构是存在的，这几个系列中同一位置的产品可能是互斥的，它们是针对不同客户的解决方案，每个客户都只择其一。

###优点###
  抽象工厂模式除了具有工厂方法模式的优点外，最主要的优点就是可以在类的内部对产品族进行约束。所谓的产品族，一般或多或少的都存在一定的关联，抽象工厂模式就可以在类内部对产品族的关联关系进行定义和描述，而不必专门引入一个新的类来进行管理。

###缺点###
  产品族的扩展将是一件十分费力的事情，假如产品族中需要增加一个新的产品，则几乎所有的工厂类都需要进行修改。所以使用抽象工厂模式时，对产品等级结构的划分是非常重要的。

###UML结构图###
![AbstractFactoryPattern](/imgs/post/AbstractFactoryPattern.png)

###源码###
IFactory:抽象工厂类
```java
/**
 * 抽象工厂
 *
 * Created by zhenguo on 11/22/14.
 */
public interface IFactory {

    /**
     * 创建产品A
     *
     * @return
     */
    public IProductA createProductA();

    /**
     * 创建产品B
     *
     * @return
     */
    public IProductB createProductB();

}
```

Factory1:工厂1
```java
/**
 * 工厂1
 *
 * Created by zhenguo on 11/22/14.
 */
public class Factory1 implements IFactory {
    @Override
    public IProductA createProductA() {
        return new ProductA1();
    }

    @Override
    public IProductB createProductB() {
        return new ProductB1();
    }
}
```

Factory2:工厂2
```java
/**
 * 工厂2
 *
 * Created by zhenguo on 11/22/14.
 */
public class Factory2 implements IFactory {
    @Override
    public IProductA createProductA() {
        return new ProductA2();
    }

    @Override
    public IProductB createProductB() {
        return new ProductB2();
    }
}
```

IProductA:抽象产品A
```java
/**
 * 抽象产品A
 *
 * Created by zhenguo on 11/22/14.
 */
public interface IProductA {

    /**
     * 产品A的方法
     */
    public void run();

}
```

ProductA1:产品A1
```java
/**
 * Created by zhenguo on 11/22/14.
 */
public class ProductA1 implements IProductA {
    @Override
    public void run() {
        System.out.println(getClass().getSimpleName());
    }
}
```

ProductA2:产品A2
```java
/**
 * Created by zhenguo on 11/22/14.
 */
public class ProductA2 implements IProductA {
    @Override
    public void run() {
        System.out.println(getClass().getSimpleName());
    }
}
```

IProductB:抽象产品B
```java
/**
 * 抽象产品B
 *
 * Created by zhenguo on 11/22/14.
 */
public interface IProductB {

    /**
     * 产品B的方法
     */
    public void run();

}
```

ProductB1:产品B1
```java
/**
 * Created by zhenguo on 11/22/14.
 */
public class ProductB1 implements IProductB {
    @Override
    public void run() {
        System.out.println(getClass().getSimpleName());
    }
}
```

ProductB2:产品B2
```java
/**
 * Created by zhenguo on 11/22/14.
 */
public class ProductB2 implements IProductB {
    @Override
    public void run() {
        System.out.println(getClass().getSimpleName());
    }
}
```

Client:客户端调用类
```java
/**
 * 抽象工厂(Abstract Factory)，提供一个创建一系列相关或相互依赖对象的接口，而无需指定他们具体的类。
 *
 * Created by zhenguo on 11/22/14.
 */
public class Client {

    public static void main(String[] args) {
        IFactory factory;
        IProductA productA;
        IProductB productB;

        factory = new Factory1();
        productA = factory.createProductA();
        productB = factory.createProductB();
        productA.run();
        productB.run();

        factory = new Factory2();
        productA = factory.createProductA();
        productB = factory.createProductB();
        productA.run();
        productB.run();

    }

}
```




