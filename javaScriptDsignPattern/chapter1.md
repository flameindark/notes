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
#### 1.3 封装：
> 含义：封装的目的是将信息隐藏、隐藏实现的细节。使得对象相对于其他对象是透明的，因为其他对象都不关心他的内部实现
1.原型模式和基于原型继承的JavaScript对象系统：
    - JavaScript中所有的对象的根对象为Object.prototype,javascript中几乎所有的函数都能当成构造函数。当当前对象无法响应某个请求(不存在某个方法或属性)会把请求委托给它自己的原型。
    - new关键字的操作的中有一个步骤就是将示例对象的__proto__属性指向类的prototype对象，及实例对象从类那里获取原型链

### 2.this、call、apply:
#### 2.1.this的指向：
1. this是基于函数执行环境动态绑定的(大致执行环境有以下几种)：
    - 作为对象的方法调用 -> 这个当然是指向改对象 如：obj.getA()那么getA方法中的this就是指向obj对象
    - 作为普通函数调用 -> 此时指向全局对象，浏览器中为window。 如 var getName = obj.getName; getName();此时getName相当于window.getName()那么this当然指向window。但是在ES5严格模式中此时this会是undefined
    - 构造函数调用 -> 如果构造函数显式返回一个对象，那么this最终指向new出来的对象为该显式对象，否则this指向new出来的对象。示例如下：
    ```javascript
        var MyClass = function(){
            this.name = 'seven';
            return {
                name: 'anne'   //显式的返回一个对象
            }
        }
        var obj = new MyClas();
        alert(obj.name) //输出：anne，此时的obj为{name:'anne'}

        var MyClass = function(){
            this.name = 'seven';
            return 'anne' //非显式返回一个对象
        }
        var obj = new MyClas();
        alert(obj.name) //输出：seven

    ```
    - call,apply调用.这个就是call和apply的作用
#### 2.2 call,apply