Builder Pattern
===============

  建造者模式(Builder),将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。
  
###适用场景###
  建造者模式主要用于创建一些复杂的对象，这些对象内部的构建的建造顺序通常是稳定的，但对象内部的构造通常面临着复杂的变化。建造者模式是在当创建复杂对象的算法应该独立于改对象的组成部分以及它们的装配方式时适用的模式。
  
###优点###
1. 如果我们用了建造者模式，那么用户就只需要指定需要创建的类型就可以得到它们，而具体建造的过程和细节就不需要知道了。
2. 建造者模式的好处就是使得建造代码与表示代码分离，由于建造者隐藏了该产品是如何组装的，所有若需要改变一个产品的内部表示，只需要再定义一个具体的建造者就可以了。
  
###缺点###
1. 建造者模式所创建的产品一般具有较多的共同点，其组成部分相似，如果产品之间的差异性很大，则不适合使用建造者模式，因此其使用范围受到一定的限制。
2. 如果产品的内部变化复杂，可能会导致需要定义很多具体建造者类来实现这种变化，导致系统变得很庞大。

###UML结构图###
![BuilderPattern](https://94275.cn/imgs/post/BuilderPattern.png)

###源码###
Builder:抽象建造者类
```java
/**
 * 抽象建造者类
 *
 * Created by zhenguo on 11/27/14.
 */
public abstract class Builder {

    public abstract void buildPartA();

    public abstract void buildPartB();

    public abstract Product getResult();

}
```
Product:产品类
```java
/**
 * 产品类
 *
 * Created by zhenguo on 11/27/14.
 */
public class Product {

    private ArrayList<String> parts = new ArrayList<String>();

    public void add(String part) {
        parts.add(part);
    }

    public void show() {
        System.out.println("产品创建:");
        for (String part : parts) {
            System.out.println("--- " + part);
        }
    }

}
```
Director:指挥者类
```java
/**
 * 指挥者类
 *
 * Created by zhenguo on 11/27/14.
 */
public class Director {

    public void construct(Builder builder) {
        builder.buildPartA();
        builder.buildPartB();
    }

}
```
ConcreteBuilder1:具体建造者类1
```java
/**
 * 具体建造者类1
 *
 * Created by zhenguo on 11/27/14.
 */
public class ConcreteBuilder1 extends Builder {
    private Product product = new Product();

    @Override
    public void buildPartA() {
        product.add("部件A");
    }

    @Override
    public void buildPartB() {
        product.add("部件B");
    }

    @Override
    public Product getResult() {
        return product;
    }
}
```
ConcreteBuilder2:具体建造者类2
```java
/**
 * 具体建造者类2
 *
 * Created by zhenguo on 11/27/14.
 */
public class ConcreteBuilder2 extends Builder {
    private Product product = new Product();

    @Override
    public void buildPartA() {
        product.add("部件X");
    }

    @Override
    public void buildPartB() {
        product.add("部件Y");
    }

    @Override
    public Product getResult() {
        return product;
    }
}
```
Client:客户端调用
```java
/**
 * 客户端调用
 *
 * 建造者模式(Builder)，将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。
 * Created by zhenguo on 11/27/14.
 */
public class Client {

    public static void main(String[] args) {
        Director director = new Director();
        Builder b1 = new ConcreteBuilder1();
        Builder b2 = new ConcreteBuilder2();

        director.construct(b1);
        Product p1 = b1.getResult();
        p1.show();

        director.construct(b2);
        Product p2 = b2.getResult();
        p2.show();
    }

}
```

  
