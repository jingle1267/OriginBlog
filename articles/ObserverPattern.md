Observer Pattern
================

  观察者模式(Observer)，又叫发布-订阅模式(Publish/Subscribe)，定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主体对象在状态发生变化时，会通知所有观察者对象，使它们能够自动更新自己。
  
###适用场景###
  当一个对象的改变需要同时改变其他对象的时候，而且它不知道具体有多少对象有待改变时，应该考虑使用观察者模式。一个抽象模型有两个方面，其中一方面依赖于另一方面，这时用观察者模式可以将这两者封装在独立的对象中使它们各自的独立的改变和复用。
  
###优点###
1. 观察者模式在被观察者和观察者之间建立一个抽象的耦合。
2. 观察者模式支持广播通讯。

###缺点###
1. 如果一个被观察者对象有很多的直接和间接的观察者的话，将所有的观察者都通知到会花费很多时间。
2. 如果在被观察者之间有循环依赖的话，被观察者会触发它们之间进行循环调用，导致系统崩溃。在使用观察者模式是要特别注意这一点。
3. 如果对观察者的通知是通过另外的线程进行异步投递的话，系统必须保证投递是以自恰的方式进行的。
4. 虽然观察者模式可以随时使观察者知道所观察的对象发生了变化，但是观察者模式没有相应的机制使观察者知道所观察的对象是怎么发生变化的。
  
###UML结构图###
![ObserverPattern](https://94275.cn/imgs/post/ObserverPattern.png)

###源码###
Subject:主题或叫抽象通知者
```java
/**
 * 主题或叫抽象通知者
 *
 * Created by zhenguo on 11/29/14.
 */
public abstract class Subject {

    private List<Observer> observers = new ArrayList<Observer>();

    /**
     * 增加观察者
     * @param observer
     */
    public void attach(Observer observer) {
        observers.add(observer);
    }

    /**
     * 移除观察者
     * @param observer
     */
    public void detach(Observer observer) {
        observers.remove(observer);
    }

    /**
     * 通知所有观察者
     */
    public void notifyAllObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }

}
```
Observer:抽象观察者
```java
/**
 * 抽象观察者
 *
 * Created by zhenguo on 11/29/14.
 */
public abstract class Observer {

    public abstract void update();

}
```
ConcreteSubject:具体主题或具体通知者
```java
/**
 * 具体主题或具体通知者
 *
 * Created by zhenguo on 11/29/14.
 */
public class ConcreteSubject extends Subject {

    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }
}
```
ConcreteObserver:具体观察者
```java
/**
 * 具体观察者
 *
 * Created by zhenguo on 11/29/14.
 */
public class ConcreteObserver extends Observer {

    private String name;
    private ConcreteSubject subject;

    public ConcreteObserver(String name, ConcreteSubject subject) {
        this.name = name;
        this.subject = subject;
    }

    @Override
    public void update() {
        System.out.println("观察者 " + name + " 的状态是 " + subject.getState());
    }

    public ConcreteSubject getSubject() {
        return subject;
    }

    public void setSubject(ConcreteSubject subject) {
        this.subject = subject;
    }
}
```
Client:客户端调用
```java
/**
 * 客户端调用
 * 观察者模式(Observer)，又叫发布-订阅模式(Publish/Subscribe)，定义了一种一对多的依赖关系，让多个观察者对象
 * 同时监听某一个主题对象。这个主体对象在状态发生变化时，会通知所有观察者对象，使它们能够自动更新自己。
 *
 * Created by zhenguo on 11/29/14.
 */
public class Client {

    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();

        subject.attach(new ConcreteObserver("A", subject));
        subject.attach(new ConcreteObserver("B", subject));
        subject.attach(new ConcreteObserver("C", subject));

        subject.setState("XYZ");
        subject.notifyAllObservers();

    }

}
```

  
