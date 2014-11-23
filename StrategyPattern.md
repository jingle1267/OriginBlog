Strategy Pattern
================
  策略模式(Strategy)是一种定义一系列算法的方法，从概念上来看，所有这些算法完成的都是相同的工作，只是实现不同，它可以以相同的方式调用所有的算法，减少了各种算法类与使用算法类之间的耦合。

###设计原则###
  策略模式遵循开闭原则，对扩展开放，对修改关闭。

###适用原则###
1. 策略模式都是用来封装算法的，但在实践中，我们发现可以用它来封装几乎任何类型的规则，只要在分析过程中听到需要在不同时间应用不同的业务规则，就可以考虑使用策略模式处理这种变化的可能性。
2. 对客户隐藏具体策略(算法)的实现细节，彼此完全独立。

###优点###
1. 策略模式的有优点是简化了单元测试，因为每个算法都有自己的类，可以通过自己的接口单独测试。
2. 策略模式提供了可以替换继承关系的办法。继承
3. 使用策略模式可以避免使用多重条件转移语句。
4. 策略模式提供了管理相关的算法族的办法。

###缺点###
1. 客户端必须知道所有的策略类，并自行决定使用哪一个策略类。
2. 策略模式造成很多的策略类，每个具体策略类都会产生一个新类。

###UML结构图###
![StrategyPattern](https://github.com/jingle1267/octopress/raw/master/source/imgs/post/StrategyPattern.png)

###源码###
IStrategy:抽象算法类
```java
/**
 * 抽象算法类
 *
 * Created by zhenguo on 11/22/14.
 */
public interface IStrategy {

    /**
     * 抽象方法
     */
    public void algorithm();

}
```

StrategyA:算法A
```java
/**
 * 具体算法A
 *
 * Created by zhenguo on 11/22/14.
 */
public class StrategyA implements IStrategy {
    @Override
    public void algorithm() {
        System.out.println("算法A实现");
    }
}
```

StrategyB:算法B
```java
/**
 * 具体算法B
 *
 * Created by zhenguo on 11/22/14.
 */
public class StrategyB implements IStrategy {
    @Override
    public void algorithm() {
        System.out.println("算法B实现");
    }
}
```

Context:上下文
```java
/**
 * 上下文
 *
 * Created by zhenguo on 11/22/14.
 */
public class Context {

    private IStrategy strategy;

    public Context(IStrategy strategy) {
        this.strategy = strategy;
    }

    /**
     * 上下文接口
     */
    public void contextInterface() {
        this.strategy.algorithm();
    }

}
```

Client:客户端调用
```java
/**
 * 策略模式(Strategy)是一种定义一系列算法的方法，从概念上来看，所有这些算法完成的都是相同的工作，
 * 只是实现不同，它可以以相同的方式调用所有的算法，减少了各种算法类与使用算法类之间的耦合。
 *
 * Created by zhenguo on 11/22/14.
 */
public class Client {

    public static void main(String[] args) {
        Context context;

        context = new Context(new StrategyA());
        context.contextInterface();

        context = new Context(new StrategyB());
        context.contextInterface();
    }

}
```




