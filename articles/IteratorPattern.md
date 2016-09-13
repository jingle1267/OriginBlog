Iterator Pattern
================

  迭代模式(Iterator)，提供一种方法顺序访问一个聚合对象中各个元素，而又不暴露该对象的内部表示。

###适用场景###

1. 当你需要访问一个聚集对象，而且不管这些对象是什么都需要遍历的时候，你就应该考虑用迭代器模式。
2. 你需要对聚集有多重方式遍历时，可以考虑用迭代器模式。

###优点###

  迭代器(Iterator)模式就是分离了集合对象的遍历行为，抽象出一个迭代器类来负责，这样既可以做到不暴露集合的内部结构，有可让外部代码透明地访问集合内部的数据。

###缺点###

  对于比较简单的遍历（像数组或者有序列表），使用迭代器方式遍历较为繁琐，大家可能都有感觉，像ArrayList，我们宁可愿意使用for循环和get方法来遍历集合。
  
###UML结构图###

![Iterator Pattern](http://ihongqiqu.com/imgs/post/IteratorPattern.png)

###源码###

迭代器接口

```java
public interface Iterator {

    public Object next();

    public boolean hasNext();

}
```

具体迭代器实现类

```java
public class ConcreteIterator implements Iterator {

    private List list = new ArrayList();
    private int cursor = 0;

    public ConcreteIterator(List list) {
        this.list = list;
    }

    public boolean hasNext() {
        if (cursor == list.size()) {
            return false;
        }
        return true;
    }

    public Object next() {
        Object obj = null;
        if (this.hasNext()) {
            obj = this.list.get(cursor++);
        }
        return obj;
    }
}
```

聚集接口

```java
public interface Aggregate {

    public void add(Object obj);
    public void remove(Object obj);
    public Iterator iterator();
}
```

具体聚集类

```java
public class ConcreteAggretate implements Aggregate{

    private List list = new ArrayList();
    public void add(Object obj) {
        list.add(obj);
    }

    public Iterator iterator() {
        return new ConcreteIterator(list);
    }

    public void remove(Object obj) {
        list.remove(obj);
    }

}
```

客户端掉用

```java
public class Client {

    public static void main(String[] args) {
        Aggregate ag = new ConcreteAggretate();
        ag.add("小明");
        ag.add("小红");
        ag.add("小刚");
        Iterator it = ag.iterator();
        while(it.hasNext()){
            String str = (String)it.next();
            System.out.println(str);
        }
    }

}
```



