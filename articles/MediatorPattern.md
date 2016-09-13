Mediator Pattern
================

  中介者模式(Mediator), 用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。

###适用场景###

1. 一组定义良好的对象，现在要进行复杂的通信。
2. 定制一个分布在多个类中的行为，而又不想生成太多的子类。

###优点###

1. 降低了系统对象之间的耦合性，使得对象易于独立的被复用。
2. 提高系统的灵活性，使得系统易于扩展和维护。

###缺点###

  中介者模式的缺点是显而易见的，因为这个“中介“承担了较多的责任，所以一旦这个中介对象出现了问题，那么整个系统就会受到重大的影响。

###UML结构图###

![Mediator Pattern](http://ihongqiqu.com/imgs/post/MediatorPattern.png)

###源码###

抽象中介者

```java
public interface Mediator {

    public void send(Colleague colleague, String message);

}
```

具体中介者类

```java
public class ConcreteMediator implements Mediator {

    private ConcreteColleague1 colleague1;
    private ConcreteColleague2 colleague2;

    public void setColleague1(ConcreteColleague1 colleague1) {
        this.colleague1 = colleague1;
    }

    public void setColleague2(ConcreteColleague2 colleague2) {
        this.colleague2 = colleague2;
    }

    @Override
    public void send(Colleague colleague, String message) {
        if (colleague == colleague1) {
            colleague2.notify(message);
        } else {
            colleague1.notify(message);
        }
    }

}
```

抽象同事类

```java
public abstract class Colleague {

    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }
}
```

具体同事对象1

```java
public class ConcreteColleague1 extends Colleague {

    public ConcreteColleague1(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.send(this, message);
    }

    public void notify(String message) {
        System.out.println(getClass().getSimpleName() + " get message : " + message);
    }

}
```

具体同事对象2

```java
public class ConcreteColleague2 extends Colleague {

    public ConcreteColleague2(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.send(this, message);
    }

    public void notify(String message) {
        System.out.println(getClass().getSimpleName() + " get message : " + message);
    }
}
```

 客户端调用
 中介者模式(Mediator)，用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显式地
相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。

```java
public class Client {

    public static void main(String[] args) {
        ConcreteMediator mediator = new ConcreteMediator();

        ConcreteColleague1 colleague1 = new ConcreteColleague1(mediator);
        ConcreteColleague2 colleague2 = new ConcreteColleague2(mediator);

        mediator.setColleague1(colleague1);
        mediator.setColleague2(colleague2);

        colleague1.send("吃饭了吗？");
        colleague2.send("没有呢，你要请客？");

    }

}
```
