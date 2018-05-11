## BEM

###OOCSS基本原则

1. Separate structure and skin。


```
        #button {
          width: 200px;
          height: 50px;
          padding: 10px;
          border: solid 1px #ccc;
          background: linear-gradient(#ccc, #222);
          box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
        }

        #box {
          width: 400px;
          overflow: hidden;
          border: solid 1px #ccc;
          background: linear-gradient(#ccc, #222);
          box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
        }

        //对比
        .button {
          width: 200px;
          height: 50px;
        }

        .box {
          width: 400px;
          overflow: hidden;
        }

        .skin {
          border: solid 1px #ccc;
          background: linear-gradient(#ccc, #222);
          box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
        }
```


2. Separate container and content。

```
        #sidebar h3 {
          font-family: Arial, Helvetica, sans-serif;
          font-size: 2em;
          line-height: 1;
          color: #777;
          text-shadow: rgba(0, 0, 0, .3) 3px 3px 6px;
        }

        #footer h3 {
          font-family: Arial, Helvetica, sans-serif;
          font-size: 1.5em;
          line-height: 1;
          color: #777;
          text-shadow: rgba(0, 0, 0, .3) 2px 2px 4px;
        }
        //对比
        title 

```

### 认识

说明以下代码是针对当前公司前端框架采取的规范。  
BEM只是一种命名方法。  
使用BEM统一命名，使团队能够保持一致的命名风格，提供语义化的命名。  
使用BEM命名方法减少class之间的嵌套。  

### 基本介绍

块，元素，修饰。  

+  块是页面中可被复用的组件或者称作一个模块，对其的命名应该是一个目的性的词，而不是一个状态词。
    *  块之间是可以相互嵌套的。
    *  嵌套的级数是无限的。
+  元素依赖于块的，对其的命名应该是一个目的性的词。
    *  同一块的元素是可以相互嵌套的。
    *  嵌套的级数是无限的。
    *  块与元素也是可以嵌套的。
+  修饰是对块和元素的描述。

###如何选择block和element

如何选择使用块与元素。
If a section of code might be reused and it doesn't depend on other page components being implemented, you should create a block.

If the section of code can't be used separa

### BEM命名格式

B 表示block E 表示元素 M 表示修饰
用 \- 链接单词，用 \_\_ 表示元素，用 \-\- 表示修饰。

class类名的四种基本格式: B, B\_\_E,  B\-\-M, B\_\_E\-\-M。

###css格式

* 不能使用元素选择器。

### 类名抽象约定

我们需要找到一个平衡点，避免过度抽象与过度具体。

1.一个dom节点一般不要超过5个类名（过多的类的组合反而会导致阅读困难）

###基本原则

**块之间相互独立** 

**bad** 
```css
.panel {
  //...
}
.panel .btn{
  //...
}

```

**good**
```css
.panel {
  //...
}

.panel__btn {
  //...
}
```

**元素依赖于块**

**bad** 
```
  <div class="modal__btn"></div> //元素不能单独存在
```

**good**
```
<div class="modal">
  <div class="modal__btn"></div>
</div>
```

**修饰依赖于块或元素**

**bad** 
```
  <div class="modal--primary></div> //元素不能单独存在
```

**good**
```
<div class="modal modal--primary">

</div>
```


**元素书写方式**

**Bad**
```css
.tabbed-pane {
  font-size: 16px;
}

.tabbed-pane .text{ //出现了嵌套
    font-size: 20px;
}

.tabbed-pane-text{  //没有用分隔符区分text。
    font-size: 20px;
}
```

**Good**
```css
.tabbed-pane {
  font-size: 16px;
}

.tabbed-pane__text {
  font-size: 20px;
}

.tabbed-pane--primary {
  color: @brand-primary;
}
```


**Bad** 
```css
.nav__item__text {
  font-size: 16px;
    //这种命名方式导致元素之间相互依赖
}

.nav__item--primary--size-large {
  color: @brand-primary;
  font-size: 20px;
    //多个修饰词组成的类会导致不必要的冗余
}
```

**Good**
```css
.nav__text {
  font-size: 16px;
}

.nav__item--primary {
 font-size: 16px;
}
```

**多个BEM实例同时作用在一个DOM节点上**

```
<div class="header">
    <!--
        The `search-form` block is mixed with the `search-form` element
        from the `header` block
    -->
    <div class="search-form header__search-form"></div>
</div>
```

相关参考
* [getbem](http://getbem.com/)
* [bem](https://en.bem.info/)
* [bem-site代码库](https://github.com/bem-site)

<a name="pre-modified"></a>
###用前缀修饰class

s- (section) 表示节（用于业务上的block)//考虑中3

```css
.s-teacher-introduce {
  padding: 10px 15px;
}

.s-interview {

}

```

o- (object) 表示对象(一般而言用于表示抽象的结构)

```css
.o-layout {
  //...
}

.o-layout__item {
  //...
}

.o-container {
  //...
}

.o-media {
  //...
}

```


c- (component) 表示组件(相对于o-更倾向于功能)

```css
.c-btn {
  //...
}

.c-panel {
  //...
}
```

u- (utility)表示公用类

```css
.u-clearfix {
  &:before,
  &:after {
    content: " ";
    display: table;
  }  

  &:after {
    clear: both;
  }
}

.u-text-center {
  text-align: center; 
}
```

is- 表示状态 

```css

.is-open {
  display: block;
  //...
}

.is-loading {
  //...
}

```

js- 表示这个dom上被绑定了事件

```html
<div class="js-modal"></div>

// $(".js-modal").on('click', function(){

    });
```

_ 表示hack类

```html
<div class="js-modal"></div>

// $(".js-modal").on('click', function(){

    });
```


### css文件结构

这一块需要针对不同框架来决定目录结构的。


## 如何合理命名
//TODO

### 相关思想

>如果你对类命名越具体，那么你的类将越不通用
>类名的长度会影响文件的大小，和渲染的速度

### 简写词 映射表

// 根据相关准则简写

 三个字母的简写大部分情况能 26 * 26 * 26 + 26 * 26 + 26 
#### 规则
  1.  如果单词长度少于等于3则取全
  2.  如果是-连接的属性，则取相关的首字母或者根据1
  3.  如果是单个词一般而言是取首3个字母,或者取前2个字母+最后一个字母
  4.  按一般习惯取的取的字母
+ 属性
+ 前缀
+ 方位词
+ 尺寸性质的词
+ 常用
+ 属性值

 type       | name            | for short 
 ----       |----             | ---------
 property   | font-size       | fs     
 -          | font-weight     | fw
 -          | text-align      | ta
 -          | text-index      | ti
 -          | line-height     | lh
 -          | letter-spacing  | ls
 -          | padding         | pad
 -          | padding-top     | pt
 -          | padding-right   | pr
 -          | padding-bottom  | pb
 -          | padding-left    | pl 
 -          | margin          | mar
 -          | margin-top      | mt  
 -          | margin-right    | mr
 -          | margin-bottom   | mb  
 -          | border          | bor 
 -          | border-top      | bort
 -          | border-right    | borr
 -          | border-bottom   | borb
 -          | border-left     | borl
 -          | border-radius   | br
 -          | display         | dis  
 -          | background      | bg
 -          | position        | pos
 -          | vertical-align  | va
 -          | top             | t
 -          | right           | r
 -          | bottom          | b
 -          | left            | l
 -          | height          | hei
 -          | width           | wid
 -          | float           | flt
 -          | clear           | clr
 -          | max-height      | maxh
 -          | max-width       | maxw
 -          | overflow        | ovf
 -          | visibility      | vis
 -          | clip            | clp
 -          | z-index         | zi
 -          | table-layout    | tl
 -          | color           | colr
 -          | cursor          | cur
 - prefix   | section         | s
 -          | object          | o
 -          | utility         | u
 -          | component       | c
 -          | javascript      | js
 -          | is              | is
 -          | has             | has
 -          | theme           | the
 - size     | super small     | xsm
 -          | small           | sm
 -          | middle          | md
 -          | large           | lg
 -          | super large     | xlg
 - value    | middle          | mid
 -          | top             | t
 -          | right           | r
 -          | bottom          | b
 -          | left            | l
 -          | center          | ctr
 -          | table           | tb
 -          | percentage      | xofy(eg. x = 1 ; y = 1)
 -          | block           | blk
 - normal   | information     | info
 -          |                 |
 - structure|                 |
 -          | body            | bd
 -          | foot            | ft
 -          | head            | hd
 -          | left            | l
 -          | right           | r
 -          | bottom          | b
 -          | top             | t