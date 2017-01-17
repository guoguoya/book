#ES6代码规范对照



* let的特点
    - let只在代码块内有效
    - let不能重复同一代码块内重复定义
    - let不存在变量提升

```
    const temp = [];
    
    for ( let i = 0; i <= 10; i++) {
        temp.push(function(i){
            console.log(i);
        });
    }

    const t = [];
    
    for ( var i = 0; i <= 10; i++) {
        t.push(function(i){
            console.log(i);
        });
    }

```


* const 的特点
    - const 只在代码块内有效
    - 只能保证变量名指向的地址不变，不能保证变量名的属性值不变
    - const不存在变量提升

```
    const temp = 1;
    let t = 2; 
    //temp = t ;
```


这样做的好处是防止重复声明、声明前就调用、变量提升所造成的问题。


```
var c = 10;

function test() {
  console.log(c)
  {
    var c = 2;
  }
}
//undefined
```


    
通过字面量的方式声明变量

```
  var temp = {};

```


浏览器对ES6支持的程度不同   建议加上babel-polyfill

通过自身的fn 处理一些操作

```
var t = [1, 2, 3, 4, 5, 6];
var c = t.forEach(function(){
    
}) 

```
 

通过Object.assign 实现快速赋值

```
    class initPeiChart{
        constructor(props) {
            Object.assign(this,props);
            //最好设置默认值;

        }
    }
    //对比
    class initPeiChart{
        constructor(prop) {
            this.elem = $(prop.elem);
            this.saveTarget = $('.'+this.elem.find('table').data('saveTo'));
            this.productIds = this.saveTarget.val() ? this.saveTarget.val() : '';
            this.converKey = {'classroom': '班级','course':'课程'};
        }
    }
```


switch 中 请用{} 包裹case的代码 

```
    var type = 'int';
    switch(t) {
        case 'int': {
            break;
        } 

        default: {
            
            break;
        }
    }
```


大部分不涉及dom操作的函数中保证函数是一个纯函数。

```
  class tool {
    constructor(props){

    }
    merge() {
        return [].slice.apply(arguments).reduce(function(str, item){
          return str.concat(item);
        });
    }
  }
  window.Tool = new tool();
  var t = Tool.merge('sdfdf','asdfsdf','sadfsdf');
```

单独处理dom操作的函数。

```
    initEvent() {
        const $context = this.element;
        $context.on('click', '.item-reset', this.itemReset.bind(this));
        $context.on('click', 'input[type="radio"]', this.radioSelected.bind(this));
        $context.on('click', '.js-delete-mark', this.deleteMark.bind(this));
        $context.on('click','.js-delete-all-mark',this.deleteAllMark.bind(this));
        $context.on('click', 'input[type="checkbox"]', this.checkboxSelected.bind(this));
   }

```


在全局作用域或者函数作用域中 可以使用函数声明，在块作用域中使用函数表达式。
若写的js是一个职责单一的内容，则可以认为模块的作用域是该js的私有作用域，否则请用class加以区分。
    
```
    //a.js

    function init() {

        initEvent();
    }

    function initEvent(){

    }

    class Select{
        constructor(props) {
            init();
        }
    }

    //a.js
    class person{
        constructor() {

        }

        _init() {
            _initEvent();
        }

        _initEvent() {

        }
    }

```



   在对于偏向过程化的fn在最后返回this最好返回this可以链式调用。

        class person {
            constructor(props) {
                Object.assign(this, {name: 'default', age: 'default'}, props);
            }
            postMessage(msg) {
                console.log(msg);
                return this;
            }
        }

        const temp = new person().postMessage('I am born');



   短路表达式 与 多重短路表达式

        var temp  = a || b ; // if (a) { temp = a; } else { temp = b;}
        var temp = a && b ; // if (a) { temp = b; } else { temp = a;}


通过不同的方式进行映射，在JavaScript中常常采用对象的属性和值做一层映射。
```
    class Event {
      constructor() {  
        var event = {
          'click': function(){},
          'blur': function(){},
          'focus': function(){}
        }
        this.event = event;
      }

      _cb(e) {
        return e && (this.event[e] || false) ||  ;
      }
    }
    var temp = new Event();
    temp.cb('click')

    class Event {
      constructor() {  
        var event = {
          'click': function(){ console.log('click'); return 'click';},
          'blur': function(){},
          'focus': function(){}
        }
        this.event = event;
      }

      cb(e) {
        return e && this.event[e]  && this.event[e]() ;
      }
    }
    var temp = new Event();
    var a = temp.cb('click'); 
```

   采用尾调用的写法。  
   
   ```
    function fib(a0, a1, item) {
        if(item - 2 == 0) {
            return a1;
        } else if(item - 2 < 0) {
            return false;
        }

        return fib(a1, a0 + a1, item--);
    }

    var temp = fib(0, 1, 2);
   ```


   在写兼容性的代码的时候请直接返回对应的函数。  
   
   ```
    var addEvent = function() {
        if (document.addEventListener) {
            return function(dom,event,cb) {
                dom.addEventListener(event,cb);
            }
        }
        else {
            return fuction(dom,event,cb) {
                dom.attachEvent(`on{event}`,cb);
            }
        }
    }();
   ```
   addeven



为了增加代码的可阅读性

做出下列规定

与初始化相关的fn 以^init。  
  
```
    class ProductSelect {
        constructor(prop) {

        }
        init(){
            this._initTable();
            this._typeahead();
            this._bindSelect();
            this._closeModal();
            this._removeTdEvent();
            //这里不要添加其他实际业务的代码
        }
    }
```

  

   采用class的方法定义类，不显示采用prototype的方式添加方法，如果需要定义方法进行扩展。  
        class person {
            constructor(props) {
            }

            extend(obj) {
                Object.Assign(this.__proto__,obj);
            }

            static extend(obj) {
                Object.Assign(this.__proto__,obj);
            }
        }
   用context命名上下文this。  

        function(){
            const context = this; 
            return function() {}
        }
