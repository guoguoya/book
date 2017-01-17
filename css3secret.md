# secret

###css 小技巧
 - 可以用em或者rem实现组件整体大小统一缩放。、

 - background-color 和 background-img 是同时作用的 而且 img 在生成是图层高于 color 这样我们可以比较优雅地实现由亮暗面的按钮。
 ```css

    button {
        background-img: linear-gradient(rgba(0,0,0,.2));
    }
 ```
 - inherit 这个属性值可以用在任何css属性中。它总是绑定到父元素的计算值（对伪元素来说，则会取生成该伪元素的宿主元素）。

### 边框和背景
  背景是作用于盒模型的边框以及以内的区域
```css

    body {
      background-color: red;
    }
    div {

      box-sizing: border-box;
      height: 100px;
      width: 100px;
      border: 10px solid rgba(0,0,0,.2);
      background-color: #000000;
      background-clip: content-box; //可以针对背景截取其中的一部分
    }

```

  多重box-shadow可以实现多重边框。
  注：box-shadow 不会影响布局，鼠标的点击事件不会在box-shadow上触发，一种解决方法是设置成inset

```css

    div {
      height: 200px;
      width: 200px;
      margin: 20px;
      box-shadow: 0 0 0px 5px red inset,
                  0 0 0px 15px green inset;
    }
```

outline 和box-shadow 一样不会影响布局。 这东西和box-shadow 可以一起用， outline 的图层高于 box-shadow。

outline-offset
```css
    div {
      height: 200px;
      width: 200px;
      margin: 20px;
      outline: 5px dashed blue;
      box-shadow: 0 0 0px 5px red ,
                  0 0 0px 15px green;
    }
```

### 通过3d转换实现梯形