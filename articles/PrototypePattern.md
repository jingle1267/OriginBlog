原型模式
========

  原型模式(Prototype)，用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。原型模式其实就是从一个对象再创建另外一个可定制的对象，而且不需知道任何的创建的细节。

   原型模式主要实现有深拷贝和强拷贝两种方式。浅拷贝：对值类型的成员变量进行值的复制,对引用类型的成员变量只复制引用,不复制引用的对象；深拷贝：对值类型的成员变量进行值的复制,对引用类型的成员变量也进行引用对象的复制。
  
###适用原则###
1. 资源优化场景：类初始化需要消化非常多的资源，这个资源包括数据、硬件资源等。
2. 性能和安全要求的场景：通过new产生一个对象需要非常繁琐的数据准备或访问权限，则可以使用原型模式。
3. 一个对象多个修改者的场景：一个对象需要提供给其他对象访问，而且各个调用者可能都需要修改其值时，可以考虑使用原型模式拷贝多个对象供调用者使用。

###优点###
1. 性能好：使用原型模式创建对象比直接new一个对象在性能上要好的多，因为Object类的clone方法是一个本地方法，它直接操作内存中的二进制流，特别是复制大对象时，性能的差别非常明显。
2. 简化对象创建：使用原型模式的另一个好处是简化对象的创建，使得创建对象就像我们在编辑文档时的复制粘贴一样简单。

###缺点###
  每一个类都必须配备一个克隆方法。配备克隆方法需要对类的功能进行通盘考虑，这对于全新的类来说不是很难，而对于已经有的类不一定很容易，特别是当一个类引用不支持序列化的间接对象，或者引用含有循环结构的时候。
  
###UML结构图###
![PrototypePattern](https://94275.cn/imgs/post/PrototypePattern.png)

###源码###
Prototype:抽象原型角色
```java
/**
 * 抽象原型角色
 *
 * Created by zhenguo on 11/23/14.
 */
public interface Prototype {

    /**
     * 克隆自身的方法
     *
     * @return 一个从自身克隆出来的对象
     */
    public Object clone();

}
```

ConcretePrototype:具体的原型实现对象
```java
/**
 * 具体的实现对象
 *
 * Created by zhenguo on 11/23/14.
 */
public class ConcretePrototype implements Prototype {

    public String name = "tag";
    public int age = 0;

    public ConcretePrototype(String tag) {
        name = tag;
    }

    @Override
    public Object clone() {
        // 最简单的克隆，新建一个自身对象。
        ConcretePrototype concretePrototype = new ConcretePrototype(this.name);
        concretePrototype.age = this.age;
        return concretePrototype;
    }
}
```

Client:客户端调用
```java
/**
 * 原型模式(Prototype)，用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。
 * 原型模式其实就是从一个对象再创建另外一个可定制的对象，而且不需知道任何的创建的细节。
 *
 * Created by zhenguo on 11/23/14.
 */
public class Client {

    public static void main(String[] args) {

        ConcretePrototype concretePrototype = new ConcretePrototype("张三");
        concretePrototype.age = 24;

        ConcretePrototype concretePrototype1 = (ConcretePrototype) concretePrototype.clone();
        concretePrototype1.age = 14;

        System.out.println(String.format("用户：%s 年龄：%d", concretePrototype.name, concretePrototype.age));
        System.out.println(String.format("用户：%s 年龄：%d", concretePrototype1.name, concretePrototype1.age));

    }

}
```


  
  
  
