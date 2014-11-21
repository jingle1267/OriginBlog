Factory Method Pattern
======================

  工厂方法模式，英文Factory method pattern，工厂方法模式是简单工厂模式的进化版， 看本文之间最好先看一下简单工厂模式。工厂方法模式是定义一个创建产品对象的工厂接口，工厂接口本身不去创建对象，而是交给其子类或者是其实现类去创建，将实际创建工作推迟到子类中进行。  
###设计原则###
1. 开放-封闭原则。针对扩展是开放的，针对修改是封闭的。
2. 里氏代换原则。Liskov Substitution Principle，简称LSP。子类型必须能替换掉他们的父类型。
3. 依赖倒置原则。 也叫依赖倒转原则，Dependence Inversion Principle，对抽象进行编程，不要对实现进行编程。

###适用场景###
1. 作为一种创建类模式，在任何需要生成复杂对象的地方，都可以使用工厂方法模式。
2. 工厂模式是一种典型的解耦模式，迪米特法则在工厂模式中表现的尤为明显。假如调用者自己组装产品需要增加依赖关系时，可以考虑使用工厂模式。将会大大降低对象之间的耦合度。
3. 由于工厂模式是依靠抽象架构的，它把实例化产品的任务交由实现类完成，扩展性比较好。也就是说，当需要系统有比较好的扩展性时，可以考虑工厂模式，不同的产品用不同的实现工厂来组装。

###优点###
1. 在工厂方法模式中，工厂方法用来创建客户所需要的产品，同时还向客户隐藏了哪种具体产品类将被实例化这一细节，用户只需要关心所需产品对应的工厂，无需关心创建细节，甚至无需知道具体产品类的类名。
2. 基于工厂角色和产品角色的多态性设计是工厂方法模式的关键。它能够使工厂可以自主确定创建何种产品对象，而如何创建这个对象的细节则完全封装在具体工厂内部。工厂方法模式之所以又被称为多态工厂模式，正是因为所有的具体工厂类都具有同一抽象父类。
3. 使用工厂方法模式的另一个优点是在系统中加入新产品时，无需修改抽象工厂和抽象产品提供的接口，无需修改客户端，也无需修改其他的具体工厂和具体产品，而只要添加一个具体工厂和具体产品就可以了，这样，系统的可扩展性也就变得非常好，完全符合“开闭原则”。

###缺点###
1. 在添加新产品时，需要编写新的具体产品类，而且还要提供与之对应的具体工厂类，系统中类的个数将成对增加，在一定程度上增加了系统的复杂度，有更多的类需要编译和运行，会给系统带来一些额外的开销。
2. 由于考虑到系统的可扩展性，需要引入抽象层，在客户端代码中均使用抽象层进行定义，增加了系统的抽象性和理解难度，且在实现时可能需要用到DOM、反射等技术，增加了系统的实现难度。

###UML结构图###

![FactoryMethodPattern](http://worthed.com/imgs/post/FactoryMethodPattern.png)

###源码###

Operation:运算基类，抽象出getResult()方法。
```java
/**
 * 操作抽象类
 * Created by zhenguo on 11/21/14.
 */
public abstract class Operation {

    protected double num1;
    protected double num2;

    /**
     * 返回结果
     * @return
     */
    public abstract double getResult();

    public double getNum1() {
        return num1;
    }

    public void setNum1(double num1) {
        this.num1 = num1;
    }

    public double getNum2() {
        return num2;
    }

    public void setNum2(double num2) {
        this.num2 = num2;
    }
}
```

AddOperation:加法运算类
```java
/**
 * 加法操作
 * Created by zhenguo on 11/21/14.
 */
public class AddOperation extends Operation {
    @Override
    public double getResult() {
        return num1 + num2;
    }
}
```

SubOperation:减法运算类
```java
/**
 * 减法操作
 * Created by zhenguo on 11/21/14.
 */
public class SubOperation extends Operation {
    @Override
    public double getResult() {
        return num1 - num2;
    }
}
```

IFactory:创建运算类的工厂接口，包含一个创建运算类的抽象方法。
```java
/**
 * 工厂抽象
 * Created by zhenguo on 11/21/14.
 */
public interface IFactory {

    public Operation createOperation();

}
```

AddFactory:加法工厂，实现IFactory，创建加法运算类。
```java
/**
 * 加法工厂
 * Created by zhenguo on 11/21/14.
 */
public class AddFactory implements IFactory {
    @Override
    public Operation createOperation() {
        return new AddOperation();
    }
}
```

SubFactory:减法工厂，实现IFactory，创建减法运算类。
```java
/**
 * 减法工厂
 * Created by zhenguo on 11/21/14.
 */
public class SubFactory implements IFactory {
    @Override
    public Operation createOperation() {
        return new SubOperation();
    }
}
```
