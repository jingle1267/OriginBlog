Interpreter Pattern
===================

  解释器模式(Interpreter), 给定一个语言，定义它的文法的一种表示，并定义一个解释器，这个解释器使用该表示来解释语言中的句子。

###适用场景###

1. 重复发生的问题可以使用解释器模式
2. 一个简单语法需要解释的场景

###优点###

1. 可扩展性比较好，灵活
2. 增加了新的解释表达式的方式
3. 易于实现文法

###缺点###

1. 执行效率比较低，可利用场景比较少
2. 对于复杂的文法比较难维护

###UML结构图###

![Interpreter Pattern](http://ihongqiqu.com/imgs/post/InterpreterPattern.png)

###源码###

抽象表达式，声明一个抽象的解释操作

```java
public interface AbstractExpression {

    public void interpret(Context context);

}
```

终结符表达式

```java
public class TerminalExpression implements AbstractExpression {

    @Override
    public void interpret(Context context) {
        System.out.println("终端解释器");
    }

}
```

非终结符表达式

```java
public class NonterminalExpression implements AbstractExpression {

    @Override
    public void interpret(Context context) {
        System.out.println("非终端解释器");
    }

}
```

包含解释器之外的一些全局信息

```java
public class Context {

    private String input;
    private String output;

    public String getInput() {
        return input;
    }

    public void setInput(String input) {
        this.input = input;
    }

    public String getOutput() {
        return output;
    }

    public void setOutput(String output) {
        this.output = output;
    }
}
```

客户端调用
解释器模式(Interpreter)，给定一个语言，定义它的文法的一种表示，并定义一个解释器，
这个解释器使用该表示来解释语言中的句子。

```java
public class Client {

    public static void main(String[] args) {
        Context context = new Context();

        ArrayList<AbstractExpression> list = new ArrayList<AbstractExpression>();
        list.add(new TerminalExpression());
        list.add(new NonterminalExpression());
        list.add(new TerminalExpression());
        list.add(new NonterminalExpression());

        for (AbstractExpression expression : list) {
            expression.interpret(context);
        }
    }

}
```


