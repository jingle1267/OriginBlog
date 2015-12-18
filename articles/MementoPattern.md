Memento Pattern
===============

  备忘录模式(Memento),再不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样以后就可将该对象恢复到原先保存的状态。

###适用场景###
1. Memento模式比较适用于功能比较复杂的，但需要维护或记录属性历史的类，或者需要保存的属性只是众多属性中的一小部分是，Originator可以根据保存的Memento信息还原到前一状态。
2. 如果某个系统中使用命令模式时，需要实现命令的撤销功能，那么命令模式可以使用备忘录模式来存储可撤销的状态。
3. 当角色的状态改变的时候，有可能这个状态无效，这时候就可以使用暂时存储起来的备忘录将状态复原。

###优点###
  要保存的细节封装在了Memento中，如果需要修改保存的细节，这个时候不会影响客户端。

###缺点###
  角色状态需要完整存储到备忘录对象中，如果状态数据很大很多，那么在资源消耗上，备忘录对象会非常耗内存。

###UML结构图###
![MementoPattern](http://ihongqiqu.com/imgs/post/MementoPattern.png)

###源码
Memento:备忘录类
```java
/**
 * 备忘录类
 *
 * Created by zhenguo on 11/30/14.
 */
public class Memento {

    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}
```
Originator:发起人
```java
/**
 * 发起人
 *
 * Created by zhenguo on 11/30/14.
 */
public class Originator {

    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    public void setMemento(Memento memento) {
        state = memento.getState();
    }

    public Memento createMemento() {
        return new Memento(state);
    }

    public void show() {
        System.out.println("Current State : " + state);
    }

}
```
Caretaker:管理者类
```java
/**
 * 管理者类
 *
 * Created by zhenguo on 11/30/14.
 */
public class Caretaker {

    private Memento memento;

    public Memento getMemento() {
        return memento;
    }

    public void setMemento(Memento memento) {
        this.memento = memento;
    }
}
```
Client:客户端调用
```java
/**
 * 客户端调用
 * 备忘录模式(Memento)，再不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。
 * 这样以后就可将该对象恢复到原先保存的状态。
 *
 * Created by zhenguo on 11/30/14.
 */
public class Client {

    public static void main(String[] args) {
        Originator originator = new Originator();
        originator.setState("On");
        originator.show();

        Caretaker caretaker = new Caretaker();
        caretaker.setMemento(originator.createMemento());

        originator.setState("Off");
        originator.show();

        originator.setMemento(caretaker.getMemento());
        originator.show();

    }

}
```


