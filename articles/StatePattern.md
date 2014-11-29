State Pattern
=============

  状态模式(StatePattern)，当一个对象的内在状态改变时允许改变其行为，这个对象看起来像是改变了其类。
  
###适用原则###
  状态模式主要解决的是当控制一个对象状态转换的条件表达式过于复杂是的情况。把状态的判断逻辑转移到表示不同状态的一系列类当中，可以把复杂的判断逻辑简化。当一个对象的行为取决于它的状态，并且它必须在运行时刻根据状态改变它的行为是，就可以考虑使用状态模式。

###优点###
1. 状态模式的好处是将与特定状态相关的行为局部化，并且将不同状态的行为分割开来。程序中也也就是消除庞大的条件分支语句。
2. 状态模式通过把各种状态转移逻辑分布到State的子类之间，来减少相互间的依赖。

###缺点###
  导致较多的ConcreteState子类。
  
###UML结构图###
![StatePattern](https://github.com/jingle1267/octopress/raw/master/source/imgs/post/StatePattern.png)

###源码###
IState:抽象状态类，定义一个接口以封装与Context的一个特定状态相关的行为
```java
/**
 * 抽象状态类，定义一个接口以封装与Context的一个特定状态相关的行为
 *
 * Created by zhenguo on 11/26/14.
 */
public interface IState {

    public void handle(Context context);

}
```
ConcreteStateA:具体状态类A
```java
/**
 * 具体状态类A
 *
 * Created by zhenguo on 11/26/14.
 */
public class ConcreteStateA implements IState{
    @Override
    public void handle(Context context) {
        System.out.println("状态A");
        context.setState(new ConcreteStateB());
    }
}
```
ConcreteStateB:具体状态类B
```java
/**
 * 具体状态类B
 *
 * Created by zhenguo on 11/26/14.
 */
public class ConcreteStateB implements IState {
    @Override
    public void handle(Context context) {
        System.out.println("状态B");
        context.setState(new ConcreteStateA());
    }
}
```
Context:维护一个ConcreteState子类的实例，这个实例定义当前的状态。
```java
/**
 * Context类，维护一个ConcreteState子类的实例，这个实例定义当前的状态。
 *
 * Created by zhenguo on 11/26/14.
 */
public class Context {

    private IState state;

    public Context(IState state) {
        this.state = state;
    }

    public void setState(IState state) {
        this.state = state;
    }

    public void request() {
        state.handle(this);
    }

}
```
Client:客户端调用类
```java
/**
 * 当一个对象的内在状态改变时允许改变其行为，这个对象看起来像是改变了其类。
 *
 * Created by zhenguo on 11/26/14.
 */
public class Client {

    public static void main(String[] args) {
        Context context = new Context(new ConcreteStateA());
        // 不断地进行请求，同时更改状态
        context.request();
        context.request();
        context.request();
        context.request();
    }

}
```


  
