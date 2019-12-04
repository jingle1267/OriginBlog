Composite Pattern
===============

  组合模式(Composite)，将对象组合成树形结构以表示‘部分-整体’的层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性。

###适用场景###
  需求中是体现部分与整体层次的结构是，以及你希望用户可以忽略组合对象与单个对象的不通过，统一地使用组合结构中的所有对象时，就应该考虑用组合模式了。

###优点###
1. 高层模块调用简单。一棵树形机构中的所有节点都是Component，局部和整体对调用者来说没有任何区别，也就是说，高层模块不必关心自己处理的是单个对象还是整个组合结构，简化了高层模块的代码。
2. 节点自由增加。使用了组合模式后，增加一个树枝节点、树叶节点变得非常容易，只要找到它的父节点就成，非常容易扩展，符合开闭原则，对以后的维护非常有利。

###缺点###
  组合模式有一个非常明显的缺点，看到我们在客户端调用中的定义，提到树叶和树枝使用时的定义了吗？直接使用了实现类！这在面向接口编程上是很不恰当的，与依赖倒置原则冲突，读者在使用的时候要考虑清楚，它限制了你接口的影响范围。

###UML结构图###
![CompositePattern](https://94275.cn/imgs/post/CompositePattern.png)

###源码###
Component:组合对象抽象类
```java
/**
 * 组合对象抽象类
 *
 * Created by zhenguo on 11/30/14.
 */
public abstract class Component {

    protected String name;

    public Component(String name) {
        this.name = name;
    }

    public abstract void add(Component component);

    public abstract void remove(Component component);

    public abstract void display(int depth);

    protected String getDepthStr(int depth) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < depth; i++) {
            sb.append("-");
        }
        return sb.toString();
    }

}
```
Leaf:叶子节点，无子节点
```java
/**
 * 叶子节点，无子节点
 *
 * Created by zhenguo on 11/30/14.
 */
public class Leaf extends Component {

    public Leaf(String name) {
        super(name);
    }

    @Override
    public void add(Component component) {
        System.out.println("Cannot add to a leaf!");
    }

    @Override
    public void remove(Component component) {
        System.out.println("Cannot remove to a leaf!");
    }

    @Override
    public void display(int depth) {
        System.out.println(getDepthStr(depth) + name);
    }

}
```
Composite:子节点
```java
/**
 * 子节点
 *
 * Created by zhenguo on 11/30/14.
 */
public class Composite extends Component {

    private List<Component> children = new ArrayList<Component>();

    public Composite(String name) {
        super(name);
    }

    @Override
    public void add(Component component) {
        children.add(component);
    }

    @Override
    public void remove(Component component) {
        children.remove(component);
    }

    @Override
    public void display(int depth) {
        System.out.println(getDepthStr(depth) + name);
        for (Component component : children) {
            component.display(depth + 2);
        }
    }
}
```
Client:客户端调用
```java
/**
 * 客户端调用
 * 组合模式(Composite)，将对象组合成树形结构以表示‘部分-整体’的层次结构。组合模式使得用户
 * 对单个对象和组合对象的使用具有一致性。
 *
 * Created by zhenguo on 11/30/14.
 */
public class Client {

    public static void main(String[] args) {
        Composite root = new Composite("root");
        root.add(new Leaf("Leaf A"));
        root.add(new Leaf("Leaf B"));

        Composite composite = new Composite("Composite X");
        composite.add(new Leaf("Leaf XA"));
        composite.add(new Leaf("Leaf XB"));

        root.add(composite);

        Composite composite1 = new Composite("Composite XY");
        composite1.add(new Leaf("Leaf XYA"));
        composite1.add(new Leaf("Leaf XYB"));

        composite.add(composite1);

        root.add(new Leaf("Leaf C"));

        Leaf leaf = new Leaf("Leaf D");
        root.add(leaf);
        root.remove(leaf);

        root.display(1);
    }

}
```
