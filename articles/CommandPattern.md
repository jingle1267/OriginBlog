Command Pattern
===============

  命令模式(Command)，将一个请求封装成一个对象，从而使你可用不同的请求对客户进行参数化；对请求队列或记录请求日志，以及支持可撤销的操作。

###适用场景###

  对于大多数请求响应模式的功能，比较适合使用命令模式，命令模式对实现记录日志、撤销操作等功能比较方便。

###优点###

1. 它能容易地设计一个命令队列；
2. 在需要的情况下，可以较容易地将命令记入日志；
3. 允许接受请求的一方决定是否要否决请求；
4. 可以容易地实现对请求的撤销和重做；
5. 由于加进新的具体命令类不影响其他的类，因此增加新的具体命令类很容易。

###缺点###

  增加系统的复杂性，这里的复杂性应该主要指的是类的数量

###UML结构图###

![DecoratorPattern](http://ihongqiqu.com/imgs/post/CommandPatternUML.png)

###源码###

接受者，知道如何实施与执行一个与请求相关的操作。

```java
public class Receiver {

    public void action() {
        System.out.println("执行操作");
    }

}
```

命令抽象类，用来声明执行操作的接口

```java
public abstract class Command {

    protected Receiver receiver;

    public Command(Receiver receiver) {
        this.receiver = receiver;
    }

    public abstract void execute();
}
```

命令实现类，将一个抽象者对象绑定于一个动作，调用接受者响应的操作，以实现Execute

```java
public class ConcreteCommand extends Command {

    public ConcreteCommand(Receiver receiver) {
        super(receiver);
    }

    @Override
    public void execute() {
        receiver.action();
    }
}
```

要求命令执行这个请求

```java
public class Invoker {

    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void executeCommand() {
        command.execute();
    }
    
}
```

  客户端调用
  
  命令模式(Command)，将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化；对请求队列或记录请求日志，以及支持可撤销的操作。

```java
public class Client {

    public static void main(String[] args) {
        Receiver receiver = new Receiver();
        Command command = new ConcreteCommand(receiver);
        Invoker invoker = new Invoker();
        invoker.setCommand(command);
        invoker.executeCommand();
    }

}
```