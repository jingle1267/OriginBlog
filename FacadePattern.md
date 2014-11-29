Facade Pattern
==============

  外观模式(Facade)，又叫门面模式，它是为子系统中的一组接口提供一个一致的界面，此模式定义了一个高层接口，这个接口是的这一子系统更加容易使用。
  
###适用原则###
  首先，在设计初期阶段，应该有意识地将不同的两个层分离，层与层之间建立外观Facade；其次，在开发阶段，子系统往往因为不断的重构演化变得越来越复杂，增加外观Facade可以提供一个简单的接口，减少他们之间的依赖；第三，在维护一个遗留的大型系统时，可能这个系统已经非常难以维护和扩展了，你可以为新系统开发一个外观Facade类，来提供设计粗糙或高度复杂的遗留代码的比较清晰简单的接口，让新系统与Facade对象交互，Facade与遗留带啊交互所有复杂的工作。
  
###优点###
1. 它对客户屏蔽子系统组件，因而减少了客户处理的对象的数目并使得子系统使用起来更加方便。
2. 它实现了子系统与客户之间的松耦合关系，而子系统内部的功能组件往往是紧耦合的。
3. 如果应用需要，它并不限制它们使用子系统类。因此你可以在系统易用性和通用性之间加以选择。

###缺点###
  不符合开闭原则。

###UML结构图###
![FacadePattern](https://github.com/jingle1267/octopress/raw/master/source/imgs/post/FacadePattern.png)

###源码###
Facade:外观类
```java
/**
 * 外观类
 *
 * Created by zhenguo on 11/27/14.
 */
public class Facade {

    private SubSystemOne one;
    private SubSystemTwo two;
    private SubSystemThree three;

    public Facade() {
        one = new SubSystemOne();
        two = new SubSystemTwo();
        three = new SubSystemThree();
    }

    public void methodA() {
        System.out.println("方法组A:");
        one.methodOne();
        three.methodThree();
    }

    public void methodB() {
        System.out.println("方法组A:");
        two.methodTwo();
        three.methodThree();
    }

}
```
SubSystemOne:子系统One
```java
/**
 * 子系统One
 *
 * Created by zhenguo on 11/27/14.
 */
public class SubSystemOne {

    public void methodOne() {
        System.out.println("子系统One的方法One");
    }

}
```
SubSystemTwo:子系统Two
```java
/**
 * 子系统Two
 *
 * Created by zhenguo on 11/27/14.
 */
public class SubSystemTwo {

    public void methodTwo() {
        System.out.println("子系统Two方法Two");
    }

}
```
SubSystemThree:子系统Three
```java
/**
 * 子系统Three
 *
 * Created by zhenguo on 11/27/14.
 */
public class SubSystemThree {

    public void methodThree() {
        System.out.println("子系统Three方法Three");
    }

}
```
Client:客户端调用
```java
/**
 * 客户端调用
 * 外观模式(Facade)，为子系统中的一组接口提供一个一致的界面，此模式定义了一个高层接口，这个接口是的这一子系统更加容易使用。
 *
 * Created by zhenguo on 11/27/14.
 */
public class Client {

    public static void main(String[] args) {
        Facade facade = new Facade();

        facade.methodA();
        facade.methodB();
    }

}
```
