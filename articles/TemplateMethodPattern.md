TemplateMethodPattern
=====================

  模板方法模式（TemplateMethod），定义一个操作中的算法骨架，而将一些步骤延迟到子类中。模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。

###适用环境###
  当我们要完成在某一细节层次一致的一个过程或一系列步骤，但其个别步骤在更详细的层次上的实现可能不同时，我们通常考虑用模板方法模式来处理。
  
###优点###
1. 模板方法模式在一个类中形式化地定义算法，而由它的子类实现细节的处理。
2. 模板方法是一种代码复用的基本技术。它们在类库中尤为重要，它们提取了类库中的公共行为。
3. 模板方法模式导致一种反向的控制结构，这种结构有时被称为“好莱坞法则”，即“别找我们，,我们找你”通过一个父类调用其子类的操作(而不是相反的子类调用父类)，通过对子类的扩展增加新的行为，符合“开闭原则”

###缺点###
  每个不同的实现都需要定义一个子类，这会导致类的个数增加，系统更加庞大，设计也更加抽象，但是更加符合“单一职责原则”，使得类的内聚性得以提高。
  
###UML结构图###
![TemplateMethodPattern](https://github.com/jingle1267/octopress/raw/master/source/imgs/post/TemplateMethodPattern.png)

###源码###
AbstractClass:抽象模板
```java
/**
 * 抽象模板
 *
 * Created by zhenguo on 11/24/14.
 */
public abstract class AbstractClass {

    public abstract void start();

    public abstract void end();

    /**
     * 模板方法 实现算法骨架
     */
    public void run() {
        System.out.println("模板方法：");
        start();
        end();
    }

}
```

ConcreteClassA:实现抽象模板类A
```java
/**
 * 实现抽象模板类A
 *
 * Created by zhenguo on 11/24/14.
 */
public class ConcreteClassA extends AbstractClass {
    @Override
    public void start() {
        System.out.println("ConcreteClassA start()");
    }

    @Override
    public void end() {
        System.out.println("ConcreteClassA end()");
    }
}
```

ConcreteClassB:实现抽象模板类B
```java
/**
 * 实现抽象模板类B
 *
 * Created by zhenguo on 11/24/14.
 */
public class ConcreteClassB extends AbstractClass {
    @Override
    public void start() {
        System.out.println("ConcreteClassB start()");
    }

    @Override
    public void end() {
        System.out.println("ConcreteClassB end()");
    }
}
```

Client:客户端调用
```java
/**
 * 客户端调用
 *
 * Created by zhenguo on 11/24/14.
 */
public class Client {

    public static void main(String[] args) {
        AbstractClass cls;

        cls = new ConcreteClassA();
        cls.run();

        cls = new ConcreteClassB();
        cls.run();

    }

}
```


