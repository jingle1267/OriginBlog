Proxy Pattern
=============

代理模式(Proxy)，为其他对象提供一种代理以控制对这个对象的访问。
  
###设计原则###
  遵循单一职责的原则。

###适用原则###
1. 远程代理，也就是为一个对象在不同的地址空间提供局部代表。这样可以隐藏一个对象存在于不同地址空间的事情。
2. 虚拟代理，是根据需要创建开销很大的对象。通过它来存放实例化需要很长时间的真实对象。
3. 安全代理，用来控制真是对象访问的权限。
4. 智能指引，是指当调用真是的对象时，代理处理另外一些事情。
  在直接访问对象时带来的问题，比如说：要访问的对象在远程的机器上.在面向对象系统中，有些对象由于某些原因（比如对象创建开销很大，或者某些操作需要安全控制，或者需要进程外的访问），直接访问会给使用者或者系统结构带来很多麻烦，我们可以在访问此对象时加上一个对此对象的访问层。

###优点###
1. 职责清晰。真实的角色就是实现实际的业务逻辑，不用关心其他非本职责的事务，通过后期的代理完成一件完成事务，附带的结果就是编程简洁清晰。
2. 高扩展性
3. 代理对象可以在客户端和目标对象之间起到中介的作用，这样起到了的作用和保护了目标对象的作用。

###缺点###
1. 由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。
2. 实现代理模式需要额外的工作，有些代理模式的实现非常复杂。

###UML结构图###
![ProxyPattern](https://94275.cn/imgs/post/ProxyPattern.png)

###源码###
IProject:抽象借口
```java
/**
 * 抽象接口
 *
 * Created by zhenguo on 11/22/14.
 */
public interface ISubject {

    /**
     * 抽象方法
     */
    public void request();

}
```

RealProject:真实的对象
```java
/**
 * 真实的对象
 *
 * Created by zhenguo on 11/22/14.
 */
public class RealSubject implements ISubject {
    /**
     * 真实的请求
     */
    @Override
    public void request() {
        System.out.println("真实的请求");
    }
}
```

Proxy:代理
```java
/**
 * 代理模式
 *
 * Created by zhenguo on 11/22/14.
 */
public class Proxy implements ISubject {

    private ISubject subject;

    @Override
    public void request() {
        System.out.println("代理开始");
        if (this.subject == null) {
            this.subject = new RealSubject();
        }
        this.subject.request();
        System.out.println("代理结束");
    }
}
```

Client:客户端调用
```java
/**
 * 代理模式(Proxy)，为其他对象提供一种代理以控制对这个对象的访问。
 *
 * Created by zhenguo on 11/22/14.
 */
public class Client {

    public static void main(String[] args) {
        Proxy proxy = new Proxy();
        proxy.request();
    }

}
```


