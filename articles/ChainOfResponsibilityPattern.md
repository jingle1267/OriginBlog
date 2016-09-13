Chain Of Responsibility Pattern
===============================

  职责链模式(Chain of Responsibility)：使多个对象都有机会处理请求，从而避免请求的发送者和接受者之间的耦合关系。将这个对象连成一条链，并沿着这条链传递该请求，直到又一个对象处理它为止。

### 适用场景

1. 有多个对象可以处理同一个请求，具体哪个对象处理该请求由运行时刻自动确定
2. 在不明确指定接收者的情况下，向多个对象中的一个提交一个请求
3. 可动态指定一组对象处理请求

### 优点

1. 降低耦合度
2. 可简化对象的相互连接
3. 增强给对象指派职责的灵活性
4. 增加新的请求处理类很方便

### 缺点

1. 不能保证请求一定被接收
2. 系统性能将受到一定影响，而且在进行代码调试时不太方便；可能会造成循环调用

### UML结构图

![Chain Of Responsibility Pattern](http://ihongqiqu.com/imgs/post/ChainOfResponsibilityPattern.png)

### 源码

定义一个处理请求的接口

```java
public abstract class Handler {

    protected Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    public abstract void handlerRequest(int request);

}
```

具体处理者类1
当请求数在0到10之间则有权处理，否则转到下一位。

```java
public class ConcreteHandler1 extends Handler {
    @Override
    public void handlerRequest(int request) {
        if (request >= 0 && request < 10) {
            System.out.println(getClass().getSimpleName() + " 处理请求 " + request);
        } else if (successor != null) {
            successor.handlerRequest(request);
        }
    }
}
```

具体处理者者2
当请求数在10到20之间则有权处理，否则转到下一位

```java
public class ConcreteHandler2 extends Handler {
    @Override
    public void handlerRequest(int request) {
        if (request >= 10 && request < 20) {
            System.out.println(getClass().getSimpleName() + " 处理请求 " + request);
        } else if (successor != null) {
            successor.handlerRequest(request);
        }
    }
}
```

具体处理者者3
当请求数在20到30之间则有权处理，否则转到下一位

```java
public class ConcreteHandler3 extends Handler {
    @Override
    public void handlerRequest(int request) {
        if (request >= 20 && request < 30) {
            System.out.println(getClass().getSimpleName() + " 处理请求 " + request);
        } else if (successor != null) {
            successor.handlerRequest(request);
        }
    }
}
```

客户端调用
职责链模式(Chain of Responsibility)，使多个对象都有机会处理请求，从而避免请求的发送者和接受者之间的耦合关系。将这个对象连成一条链，并沿着这条链传递该请求，直到有一个对象处理它为止。

```java
public class Client {

    public static void main(String[] args) {
        Handler handler1 = new ConcreteHandler1();
        Handler handler2 = new ConcreteHandler2();
        Handler handler3 = new ConcreteHandler3();
        handler1.setSuccessor(handler2);
        handler2.setSuccessor(handler3);

        int[] requests = {2, 15, 25, 10, 20};
        for (int request : requests) {
            handler1.handlerRequest(request);
        }
    }

}
```
