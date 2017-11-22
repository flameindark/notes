## 基础知识
#### 1.1: 动态类型语言鸭子类型：
>编写程序时不指定变量的类型，只要它叫起来像鸭子、走起路来像鸭子那么就认为>它就是鸭子。比较宽松，书写代码时少了许多类型申明、但是也容易产生莫名奇妙>的错误
#### 1.2 多态：
> 含义： 同一操作对于不同的对象上会有不同的执行结果。即对同一个逻辑不同对象的不同实现。
1. JavaScript与Java多态比较：
    - java在实现多态时必须对象的类型进行指定限制了多态的灵活性，如Duck和Chicken都有makesound方法，假如我们的执行多态实现的方法如下：
    ```javascript
    public class AnimalSound{
        public void say(Duck duck){
            duck.makesound()
        }
    }
    ```
    显然因为AnimalSound的say方法指定了只能传Duck类型那么它就不能用于发出Chicken的叫声。这时需要给Duck和Chicken指定同一个父类或实现同一个接口，将say方法的参数的参数改为该父类才行。这无疑增加了代码量，并且也不够灵活如果新增了其他对象也必须要继承该父类或实现同一个接口。
    
    - 而js则不会限制参数的类型，只要该对象有makesound方法就能通过say方法调用该对象的makesound方法
