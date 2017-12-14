## JS基础知识

### JS作用域

JavaScript的作用域仅存在于函数范围中。

C语言和Java语言，作用域是`block-level scope`的，块级作用域。花括号就是一个作用域。

JavaScript语言，作用域是`function-level scope`的，比如if语句就不是一个作用域。

```js
var x = 1;
console.log("x=" + x);//1
if(true) {
    var x = 2;
    console.log("x=" + x); //2
}
console.log("x=" + x);
```

在JavaScript中，需要实现`block-level scope`，就是通过自执行函数创建临时作用域：

```js
var x = 1;
console.log("x=" + x);//1
if(true) {
    (function foo() {
        var x = 2;
        console.log("x=" + x); //2
    }());
}
console.log("x=" + x); //1
```

### 函数被提升

函数的声明方式主要有两种：声明式和变量式；

> 声明式会自动将声明式放在前面并且执行赋值过程。

```js
function test() {
    bar(); 
    function bar() {  //function declaration, 
        console.log("this will run?");
    }
}
test();
```

```js
function test() {
    foo();
    var foo = function() { //function express assigned to local variable 'foo'
        console.log("this will run?");
    }
}
test();
```

> 带有命名的函数变量式声明，是不会提升到作用域范围内。
```js
var bar = function foo() {
    console.log("foo run");
}

bar();
foo(); //ReferenceError "foo is not defined"
```
## 变量对象

### 基本类型
js 五种基本类型：number，string，boolean，undefined，null;

五种基本类型保存在内存的栈中，大小固定，复制其变量时会创建这个值的副本。使用typeof区分，这些值是在底层上直接实现的，不是Object，没有原型，没有构造函数。

### 引用类型
引用类型的值是对象，则保存在堆内存中。引用类型的变量实际上是一个指针，它保存在栈中，指向堆内存中的对象，复制引用类型变量实际是复制该指针，用instanceof区分。

### typeof 返回值
用来检测一个对象是否已经定义或者是否已经赋值。

typeof 实际返回类型只有六种：

- string
- number
- boolean
- undefined
- object
- function

> 检测一个对象的类型，强烈推荐使用Object.prototype.toString方法；typeof的一些返回值在标准文档中并未定义。
> typeof 适用于检测基本类型(primitive types)，Object 类型检测使用Object.prototype.toString；

### instanceof 操作符
用来比较两个操作符的构造函数。只是在比较自定义的对象时，才有意义。

如果用来比较内置类型，将会和`typeof`操作符一样用处不大。


#### JavaScript中的undefined和not define的区别：

JS中，未声明的变量会直接抛出异常 var {name} is not defined，如果没有处理异常，代码就会停止运行。

声明未赋值的变量会是undefined，但是不会抛出异常。











