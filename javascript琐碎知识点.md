# JavaScript琐碎知识点

### 1.instanceof的用法

在js高级的技巧中会用instanceof来创建作用域安全的构造函数。
instanceof运算符希望左操作数是一个对象，右操作数表示对象的类。如果左侧的对象是右侧类的实例，则表达式返回true；否侧返回false。Javascript中对象的类似通过初始化它们的构造函数来定义的。这样的话，instanceof的右操作数应当是一个函数。比如：

```
var d = new Date();    //通过计算Date()构造函数来创建一个新对象
d instanceof Date;     //计算结果为true，d是有Date()创建的
d instanceof Object;   //计算结果为true,所有对象都是Object的实例
d instanceof Number;   //计算结果为false，d不是一个Number对象
var a =[1,2,3];        //通过数组直接量的写法创建一个数组
a instanceof Array;    //计算结果为true，a是一个数组
a instanceof Object;   //计算结果为true，所有数组都是对象
a instanceof RegExp;   //计算结果为false，数组不是一个正则表达式
```

需要注意的是，所有对象都是Object的实例。但通过instanceof判断一个对象是否是一个类的实例的时候，这个判断也会包含对“父类”的检测。如果instanceof的左操作数不是一个对象的话，instanceof返回false,如果右操作数不是一个函数，则会抛出一个类型错误异常。

