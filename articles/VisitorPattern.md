Visitor Pattern
===============

  访问者模式(Visitor)，表示一个作用于某对象结构中的各元素的操作。它使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

###适用场景###

1. 对象结构中对象对应的类很少改变，但经常需要在此对象结构上定义新的操作
2. 需要对一个对象结构中的对象进行很多不同的并且不相关的操作，而需要避免让这些操作“污染”这些对象的类，也不希望在增加新操作时修改这些类

###优点###

1. 使得新增新的访问操作变得更加简单
2. 能够使得用户在不修改现有类的层次结构下，定义该类层次结构的操作
3. 将有关元素对象的访问行为集中到一个访问者对象中，而不是分散搞一个个的元素类中

###缺点###

1. 增加新的元素类很困难。在访问者模式中，每增加一个新的元素类都意味着要在抽象访问者角色中增加一个新的抽象操作，并在每一个具体访问者类中增加相应的具体操作，违背了“开闭原则”的要求
2. 破坏封装。当采用访问者模式的时候，就会打破组合类的封装
3. 比较难理解。貌似是最难的设计模式了

###UML结构图###

![Visitor Pattern](http://ihongqiqu.com/imgs/post/VisitorPattern.png)

###源码###



```java
public interface Element {

    public void accept(Visitor visitor);

}
```

```java
public interface Visitor {

    public void visitElementA(Element element);

    public void visitElementB(Element element);

}
```

```java
public class ConcreteElementA implements Element {

    @Override
    public void accept(Visitor visitor) {
        visitor.visitElementA(this);
    }

    public void operation() {

    }
}
```

```java
public class ConcreteVisitor1 implements Visitor {
    @Override
    public void visitElementA(Element element) {
        System.out.println(element.getClass().getSimpleName() + " 被 " + this.getClass().getSimpleName() + " 访问");
    }

    @Override
    public void visitElementB(Element element) {
        System.out.println(element.getClass().getSimpleName() + " 被 " + this.getClass().getSimpleName() + " 访问");
    }
}
```

```java
public class ObjectStructure {

    private List<Element> elements = new ArrayList<Element>();

    public void attach(Element element) {
        elements.add(element);
    }

    public void detach(Element element) {
        elements.remove(element);
    }

    public void accept(Visitor visitor) {
        for (Element element : elements) {
            element.accept(visitor);
        }
    }

}
```

客户端调用
访问者模式(Visitor)，表示一个作用于某对象结构中的各元素的操作。
它使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

```java
public class Client {

    public static void main(String[] args) {
        ObjectStructure structure = new ObjectStructure();
        structure.attach(new ConcreteElementA());
        structure.attach(new ConcreteElementB());

        Visitor visitor1 = new ConcreteVisitor1();
        Visitor visitor2 = new ConcreteVisitor2();

        structure.accept(visitor1);
        structure.accept(visitor2);
    }

}
```
