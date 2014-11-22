简单工厂
========

  简单工厂模式是属于创建型模式，又叫做静态工厂方法（Static Factory Method）模式，简单工厂模式是由一个工厂对象决定创建出哪一种产品类的实例。简单工厂模式是工厂模式家族中最简单实用的模式。
  
###设计原则###
  迪米特法则：一个对象应该对其他对象保持最少的了解。

###适用场景###
  简单工厂模式分离产品的创建者和消费者，有利于软件系统结构的优化。

###优点###
  工厂类是整个模式的关键所在。它包含必要的判断逻辑，能够根据外界给定的信息，决定究竟应该创建哪个具体类的对象。用户在使用时可以直接根据工厂类去创建所需的实例，而无需了解这些对象是如何创建以及如何组织的。有利于整个软件体系结构的优化。

###缺点###
  由于工厂类集中了所有实例的创建逻辑，这就直接导致一旦这个工厂出了问题，所有的客户端都会受到牵连；而且由于简单工厂模式的产品室基于一个共同的抽象类或者接口，这样一来，但产品的种类增加的时候，即有不同的产品接口或者抽象类的时候，工厂类就需要判断何时创建何种种类的产品，这就和创建何种种类产品的产品相互混淆在了一起，违背了单一职责，导致系统丧失灵活性和可维护性。而且更重要的是，简单工厂模式违背了“开放封闭原则”，就是违背了“系统对扩展开放，对修改关闭”的原则，因为当我新增加一个产品的时候必须修改工厂类，相应的工厂类就需要重新编译一遍。

###UML结构图###
![SimpleFactoryPattern](http://worthed.com/imgs/post/SimpleFactoryPattern.png)

###源码###
Operation:运算类接口
```java
/**
 * 运算接口
 *
 * Created by zhenguo on 11/22/14.
 */
public interface Operation {

    /**
     * 计算两个操作数的运算值
     *
     * @param num1 操作数1
     * @param num2 操作数2
     * @return 返回两个操作数的运算值
     */
    public double operate(Double num1, Double num2);

}
```

AddOperation:加法运算类
```java
/**
 * 加法实现类
 *
 * Created by zhenguo on 11/22/14.
 */
public class AddOperation implements Operation {
    @Override
    public double operate(Double num1, Double num2) {
        return num1 + num2;
    }
}
```

SubOperation:减法运算类
```java
/**
 * 减法实现类
 *
 * Created by zhenguo on 11/22/14.
 */
public class SubOperation implements Operation {
    @Override
    public double operate(Double num1, Double num2) {
        return num1 - num2;
    }
}
```

SimpleFactory:简单工厂
```java
/**
 * 简单工厂类
 *
 * Created by zhenguo on 11/22/14.
 */
public class SimpleFactory {

    /**
     * 获取与参数运算符相匹配的类实例
     *
     * @param operator 运算符
     * @return 返回与参数运算符相匹配的类实例
     */
    public Operation createOperation(char operator) {
        switch (operator) {
            case '+':
                return new AddOperation();
            case '-':
                return new SubOperation();
            case '*':
                return new MulOperation();
            case '/':
                return new DivOperation();
            default:
                try {
                    throw new Exception("找不到与" + operator + "相匹配的运算符");
                } catch (Exception e) {
                    e.printStackTrace();
                }

        }
        return null;
    }
}
```

Client:客户端调用类
```java
/**
 * 简单工厂模式是属于创建型模式，又叫做静态工厂方法（Static Factory Method）模式，
 * 简单工厂模式是由一个工厂对象决定创建出哪一种产品类的实例。简单工厂模式是工厂模式家族中最简单实用的模式。
 *
 * Created by zhenguo on 11/22/14.
 */
public class Client {

    public static void main(String[] args) {
        SimpleFactory simpleFactory = new SimpleFactory();

        Operation addOperation = simpleFactory.createOperation('+');
        System.out.println(addOperation.operate(3.0, 5.0));

        Operation subOperation = simpleFactory.createOperation('-');
        System.out.println(subOperation.operate(3.0, 5.0));

        Operation mulOperation = simpleFactory.createOperation('*');
        System.out.println(mulOperation.operate(3.0, 5.0));

        Operation divOperation = simpleFactory.createOperation('/');
        System.out.println(divOperation.operate(3.0, 5.0));

    }

}
```


  
