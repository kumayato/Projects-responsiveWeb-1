==项目知识点总结==
---


# 工具包扩展
- normalize.css 
  + 初始化css
  + npm install normalize.css

- owlcarousel2 
  + 响应式轮播效果
  + 感受：刚开始觉得这个插件好好用，零学习成本又简单，后来发现不稳定，有一些bug，不是很好用。

- picturefill
  + 实现响应式图片
 
- browsersync
  + [browsersync](http://www.browsersync.cn/)：实现浏览器文件同步更改，自动刷新页面。
  

# 相关网站
- [caniuse兼容性查询](http://caniuse.com/)
- [BFC扩展](http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)
- [Autoprefixer](http://autoprefixer.github.io/) ：自动给CSS添加前缀，解决浏览器的兼容问题，很方便！
- [owlcarousel2](http://owlcarousel2.github.io/OwlCarousel2/) ： 实现轮播的插件。
- [picturefill](http://scottjehl.github.io/picturefill/) ：实现响应式图片。
- [tinypng](https://tinypng.com/) ：对png的图片进行压缩。

# PC端的样式(px em rem)
- px
  + 一个px相当于一个像素
- em
  + 相对长度单位
  + em的参照物为父元素的font-size
  + em具有继承的特点
  + 当没有font-size时，浏览器会有一个默认的em设置 ： 1em = 16px
- rem
  + 和em一样是相对单位，但是em是相对于其父元素来设置字体大小的,而rem是相对于根元素<html>,所有更加安全且便于控制。
  + 兼容性，ie8和部分ie9不支持。
  + ==注意==：在中文版的chrome浏览器中，rem有一个最小下限是12px。如果你设置的1rem = 10px;chrome浏览器会自动转化为12px，就会造成偏差，如果要精确设置，建议使用px。

# CSS初始化样式
- 可以引用工具包normalize.css初始化样式
- 1rem = 10px 便于换算
```
/*一般浏览器的默认font-sizes是16px,将font-size: 62.5%相当于10px,方便后面用rem等相对单位的换算*/
html {
    font-size: 62.5%;   /*相当于10px*/
    color : #666;
}
body {
    font-size: 1.2rem;   /*相当于12px*/
    line-height: 1.5;
    background-color: #f7f7f7;
}
```


# CSS工具样式
```
/*块状元素居中*/
.center-block {
    display: block;
    margin-left: auto;
    margin-right: auto;
}


/*左右浮动*/
.pull-right {
    float: right !important;
}
.pull-left {
    float: left !important;
}

/*文字对齐*/
.text-right {
    text-align: right !important;
}
.text-left {
    text-align: left !important;
}
.text-center {
    text-align: center !important;
}


/*隐藏显示*/
.hide {
    display: none !important;
}
.show {
    display: block !important;
}
.invisible {
    visibility: hidden;
}

/*文字隐藏*/
.text-hide {
    font: 0/0 a;
    color: transparent;
    text-shadow: none;
    background-color: transparent;
    border: 0;
}


/*清除浮动*/
.clearfix::before,
.clearfix::after {
    content: " ";
    display: table;
}
.clearfix::after {
    clear: both;
}
```


# 伪元素清除浮动

- 方式一

```

.clearfix::after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix {
    zoom: 1;
}

```

- 方式二
```
.clearfix::after {
    content: " ";
    display: table;
    clear : both
}

```

- 方式三
  + 优点：可以防止浏览器顶部的空白崩溃。两个盒子上下margin会发生叠加，这种方式可以防止叠加。

```
.clearfix::before,
.clearfix::after {
    content: " ";
    display: table;
}
.clearfix::after {
    clear: both;
}
```


# CSS的模糊点
- font-size: 0：通过给父盒子设置font-size: 0，可以消除inline-block之间的默认间距。

- cale()：用于动态计算长度值。需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)。

- text-overflow
  + clip  修剪文本。
  + ellipsi 显示省略符号来代表被修剪的文本。
  
- white-space
  + nowrap 文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。
  + normal 空白会被浏览器忽略，但是如果文本太长会换行。
  + pre 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。

- 配合使用：一长串文字不换行且结尾以省略号省略。

```
text-overflow: ellipsis;
overflow: hidden;
white-space: nowrap;
```

- 修改图片背景为黑白（图片和背景图片）

```
img {
    -webkit-filter: grayscale(100%); 
    /* Chrome, Safari, Opera */
    filter: grayscale(100%);
}
```

# 媒体查询
> 在媒体查询中使用rem和em

- 因为媒体查询的级别是高于html的，所以在媒体查询里如果要使用rem/em这样的相对单位，参照的不再是html的设置，而是浏览器的默认设置。
例如浏览器的默认字体大小是16px,800px = 50rem。

```
/*屏幕的宽度小于等于800px*/
@media only screen and (max-width: 50em) {
    
}

/*屏幕的宽度在481px-800px之间*/
@media only screen and (min-width: 30.0625em) and (max-width: 50em){

}

/*屏幕的宽度小于等于400px*/
@media only screen and (max-width: 30em){

}
```


> only

- 加only，老的浏览器不认识，后面的不会执行，媒体查询不起作用。

- 不加only，老的浏览器会认识 screen，但是不认识后面的条件，会忽略条件，把媒体查询里面的东西全部应用，可能会导致页面错乱。

# 响应式图片
> srcset属性

- 通过在img标签下设置属性srcset，浏览器会根据屏幕的宽度，网速，cooking,DPR等因素来决定要用哪一种图片。
- 注意兼容性
```
<img src="img/test.png" alt="图片"
srcset="img/test-l.png 1600w,img/test-m.png 800w, img/test.png 480w">
        
```

> sizes属性
- 通过在img标签下设置属性size，告诉浏览器以什么视口来显示图片，默认 size = "100vw" vw指的是viewport width视口宽度。

```
<img src="img/test.png" alt="图片"
srcset="img/test-l.png 1600w,img/test-m.png 800w, img/test.png 480w"
sizes="(min-width:800px) 800px, 100vw"

/*屏幕宽度大于等于800px的时候，图片的宽度都是800px,小于800px的时候，图片的宽度自适应*/
>
        
```
> picture标签
- 一个<picture>标签里面可以包含多个<source>标签，每个<source>标签里可以使用媒体查询和设置srcset属性，浏览器会遍历<picture>标签中的每个<source>标签，根据当下的情况，找到最合适的srcset,然后来设置<img>标签。
- 兼容性较差，配合picturefill插件来使用。
[github](https://github.com/scottjehl/picturefill/)


```
<picture>
    <source media="(max-width : 36em)"
            srcset="img/test-s.jpg 768w">
    <source srcset="img/test.jpg 1800w">
    <img src="img/test.jpg 1800w" alt="">
</picture>
```


# 响应式布局的注意点
- 用rem/em等相对单位代替px更好
- 不要给每个盒子固定高度和宽度，宽度用百分比来设置，高度可以通过给盒子内部的元素设置行高和padding来撑开父盒子。
- 响应式图片。

# 处理兼容性
[picturefill](https://github.com/scottjehl/picturefill/) ： 处理picture标签的兼容。

[html5shiv](https://github.com/aFarkas/html5shiv)：处理html5标签的兼容。

[Respond](https://github.com/scottjehl/Respond) : 处理媒体查询的兼容。

[modernizr](https://modernizr.com/) ：检测各类兼容性。

[caniuse](http://caniuse.com/) ： 各个兼容性查询。

[browserhacks](http://browserhacks.com/)：各个浏览器的兼容性写法
