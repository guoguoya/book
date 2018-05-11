# you_dont_konw_js

## 作用域（scope）

定义：``名字``与实体的``绑定``保持有效的那部分计算机程序。

不同的编程语言可能有不同的作用域和``名字解析``。同一语言内也可能存在多种作用域，随实体的类型变化而不同，作用域类别影响变量的绑定方式。

JavaScript采用词法作用域。

## RHS 和LHS

"赋值操作的目标是谁(LHS)”以及“谁是赋值操作的源头(RHS)"


## 函数表达式（info：wiki 什么是表达式）

q:函数在什么时候会被当成一个表达式？

```js
(function(){ console.log(123)});
    setTimeout(function sign(){ console.log('danger') }, 1000);
    sign();//VM225:1 Uncaught ReferenceError: sign is not defined
```

## 函数作用域和块作用域

### try/catch 
catch部分会创建一个块级作用域，声明的变量仅仅在catch内部有效。

###闭包的定义

函数在其定义外的作用域执行。

###提升

函数首先被提升，然后是变量被提升。
## this

this的绑定取决于函数的调用方式。

当一个函数被调用时，会创建一个活动记录（有时候也称为执行上下文）。这个记录会包含函数在哪里被调用（调用栈），函数调用的方法，函数调用的参数等信息。this就是记录的其中一个属性，会在函数执行的过程中用到。

###this的绑定方式

默认绑定

在非strict mode 下this会被绑定到全局对象上，在strict mode下 this 会被绑定到undefined上。

###判断this

1.函数在new中被调用时，this绑定于新创建的对象
2.函数通过call、apply调用，this绑定于指定的对象
3.函数在某个上下文对象中调用。this绑定与那个上下文的对象。
4.如果都不是的，则使用默认绑定。在严格模式下，绑定到undefined上，在非严格模式下，绑定到全局对象上。

###this的几种特殊
1.被忽略的this
当以 null或者undefined作为绑定对象传入call，apply，bind中时，改绑定将被忽略，实际将变成默认绑定。

2.间接引用

3.软绑定

```js
    
    Function.prototype.softBind = function (context) {
        const args = Array.prototype.slice.call(arguments, 1);
        const fn = this; 
        const retfn = function() {
            let self = context;
            if (this && (typeof window != 'undefined' || this != window) && (typeof global != 'undefined' || this != global)) {
                self = this;
            }
            fn.apply(self, args.concat(Array.prototype.slice.call(arguments)));
        }

        return retfn;
    }
```

##对象

>>对象的内容是由一些存储在特定命名位置的值组成的，我们称之为属性。一般对象的内容不会存在对象的容器内部。存储在对象容器内部的是这些属性的名称。

## [[Get]]

在语言规范中，myObject.a实际上是[[Get]]操作，对象默认内置的[[Get]]操作。

## [[Put]]

在语言规范中，这是一个赋值规范操作，调用对象默认内置的[[Put]]操作。

## getter and setter（访问描述符）

在es5中可以通过getter 和setter部分改写默认操作，但是只能针对对象的单个属性。
getter是一个隐藏函数，setter也是一个隐藏函数，会在设置属性的时候调用（q:那我是不是可以认为每一次属性的访问都是getter 和setter的调用，其实是[[Get]],[[Put]]中的其中一步？）

不管是对象文字语法中的get a() {} , defineProperty()中的显示定义，两者都会在对象中创建一个不包含值的属性，对于这个属性的访问会自动调用一个隐藏函数，它的返回值会被当成属性访问的返回值。

## 禁止扩展

Object.preventExtensions();

禁止一个对象添加新属性并且保留已有属性。

Object.seal（）

在Object.preventExtensions()的基础上，并且把所有现有属性设置成configurable：false;

Object.freeze()

在Object.seal()的基础上，

##混合对象类

##原型

im:属性设置和屏蔽

对象通过原型关联。

[[Prototype]]机制就是存在于对象中的一个内部链接，它会引用其他对象。既原型链。

用Object.create(null)可以构建一个字典。


q:采用内部委托还是直接委托？看使用场景吧。

### 行为委托

使用委托还是类的形式实现继承有待抉择。

这章的观点强烈了，有待考证。

q:为什么要在原型上共享属性（非fn）这样做的意义是什么，有没有其他替代的方法？

super 是在定义时静态绑定的。


