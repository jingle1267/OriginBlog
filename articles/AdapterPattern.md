Adapter Pattern
===============

  适配器模式(Adapter)，将一个类的接口转换成客户希望的另外一个接口。Adapter模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。适配器模式实现方式有两种：类适配和对象适配

###适用场景###
  适配器模式主要应用于希望复用一些现存的类，但是接口又与复用环境要求不一致的情况。两个系统双方要产生关系，但是双方不太容易修改的时候就需要考虑使用适配器模式。

###优点###
1. 将目标类和适配者类解耦；
2. 增加了类的透明性和复用性，将具体的实现封装在适配者类中，对于客户端类来说是透明的，而且提高了适配者的复用性；
3. 灵活性和扩展性都非常好，符合开闭原则；

###缺点###
  类适配对Java、C#等不支持多继承的语言来说具有一定的局限性；

###UML结构图###
类适配UML结构图：
![ClassAdapterPattern](https://94275.cn/imgs/post/ClassAdapterPattern.png)
对象适配UML结构图：
![ObjectAdapterPattern](https://94275.cn/imgs/post/ObjectAdapterPattern.png)

###源码###
Source:源,需要适配的对象
```java
/**
 * 源
 *
 * Created by zhenguo on 11/29/14.
 */
public class Source {

    public void run() {
        System.out.println("Run");
    }

}
```
ITarget:目标接口，期望的接口
```java
/**
 * 目标接口
 *
 * Created by zhenguo on 11/29/14.
 */
public interface ITarget {

    public void run();

    public void fly();

}
```
ClassAdapter:类适配
```java
/**
 * 类适配器
 *
 * Created by zhenguo on 11/29/14.
 */
public class ClassAdapter extends Source implements ITarget{
    @Override
    public void fly() {
        System.out.println("Fly");
    }
}
```
OjbectAdapter:对象适配
```java
/**
 * 对象适配
 *
 * Created by zhenguo on 11/29/14.
 */
public class ObjectAdapter implements ITarget {

    private Source source = new Source();

    @Override
    public void run() {
        source.run();
    }

    @Override
    public void fly() {
        System.out.println("Fly");
    }
}
```
Client:客户端调用
```java
/**
 * 客户端调用
 * 适配器模式(Adapter)，将一个类的接口转换成客户希望的另外一个接口。Adapter模式使得原本由于接口
 * 不兼容而不能一起工作的那些类可以一起工作。
 * 适配器模式实现方式有两种：类适配和对象适配
 *
 * Created by zhenguo on 11/29/14.
 */
public class Client {

    public static void main(String[] args) {
        // 类适配
        System.out.println("类适配：");
        ClassAdapter classAdapter = new ClassAdapter();
        classAdapter.run();
        classAdapter.fly();

        // 对象适配
        System.out.println("对象适配：");
        ObjectAdapter objectAdapter = new ObjectAdapter();
        objectAdapter.run();
        objectAdapter.fly();

    }

}
```


