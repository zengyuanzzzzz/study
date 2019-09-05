# css元素居中
##水平居中
###行内元素水平居中
>给父元素增加text-align：center；属性。

```
    <style>
        .main {
            width: 300px;
            height: 300px;
            background-color: #50ba8b;
            text-align: center;元素水平居中
        }
    </style>
    <div class="main">
    	<span class="content">
        	我是要居中的行内元素span
    	</span>
	</div>
```        
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/1.png)
可以快速实现块级元素内部行内元素水平的居中。此方法对inline、inline-block、inline-table和inline-flex等行内元素水平居中有效。如果块级元素内部包着另外一个块级元素，我们可以将内部块级元素转变为行内块元素，再通过设置元素居中以达到水平居中。
###块级元素水平居中
一、直接给元素增加margin：0 auto；属性。

>实现原理：块元素的水平方向有七个宽度属性：①左外边距，②左边框，③左内边距，④元素宽度（width），⑤右内边距，⑥右边框，⑦右外边距。但是，七个属性中有四个（左右内边距、左右边框），不能设为auto，宽度默认为0；另外三个属性（width、左右外边距）可以设为auto，也就是说，另外三个的宽度之和要等于包含块的宽度。所以当块的宽度为300px时，左右边距平分300px减去元素宽度。


```
    <style>
        .content{
            width: 300px;
            height: 300px;
            background: pink;
        }
        .main{
            width: 100px;
            height: 100px;
            background: deeppink;
            margin: 0 auto;
        }
    </style>
	<div class="content">
    	<div class="main"></div>
	</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/2.png)
 
缺点：必须知道元素的宽度以及父元素需为块级元素，不能脱离文档流（如设置position:absolute）,则无效。


二. 将块级元素设置为display：table，表现为类似为block，但宽度为内容宽，然后将其设置水平居中。

```
    <style>
        .content{
            width: 300px;
            background: pink;
        }
        .main{
            display: table;
            background: deeppink;
            margin: 0 auto;
        }
    </style>
    <div class="content">
    <div class="main">demo
    </div>
</div>

``` 
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/table.png)
 优点：适用于不知道元素的宽高的情况。
 
 缺点：大多数浏览器（IE6/7除外）对其支持良好。
 
###多块级元素水平居中
一、利用inline-block
>将要水平排列的块状元素设为display:inline-block，然后在父级元素上设置text-align:center，达到与上面的行内元素的水平居中一样的效果。

```
   <style>
        .content{
            width: 300px;
            height: 300px;
            background: pink;
            text-align: center;

        }
        .main{
            display: inline-block;
            width: 50px;
            height: 50px;
            background: deeppink;
        }
    </style>

</head>
<body>
<div class="content">
    <div class="main">
    </div>
    <div class="main">
    </div>
    <div class="main">
    </div>
</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/inlineblock.png)
优点：适用于所有浏览器

缺点：使居中元素变成行内元素而致使无法设置宽高。
##垂直居中
###单行内联垂直居中
>利用line-height 和 height 相等使元素居中。

```
    <style>
        .main {
            width: 300px;
            height: 300px;
            background-color: #50ba8b;
            line-height: 300px;
        }
    </style>

<div class="main">
    	<span class="content">
        	我是要居中的行内元素span
    	</span>
</div>

```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/neilianyuansu.png)
优点：适用于所有浏览器

缺点：只对文本有效(块级元素无效)，这个方法在小元素上非常有用，例如使按钮文本或者单行文本居中。

###多行内联垂直居中
一、利用表布局（table)和vertical-align: middle使元素居中

```
    <style>
        .main {
            display: table;
            width: 400px;
            height: 300px;
            background-color: #50ba8b;
        }
        .content{
            display: table-cell;
            vertical-align: middle;
        }
    </style>

</head>
<body>
<div class="main">
    	<span class="content">
        	我是要居中的行内元素span我是要居中的行内元素span
            我是要居中的行内元素span我是要居中的行内元素span
            我是要居中的行内元素span我是要居中的行内元素span
    	</span>
</div>
```

 ![行内元素水平居中](/Users/zengyuan/Desktop/image/duohangneilian.png)
优点：这在子元素不确定宽高和数量时，特别实用！

缺点：大多数浏览器（IE6/7除外）对其支持良好。table-cell会被其他一些CSS属性破坏，在使用display:table-cell与float或position属性尽量不同用。table-cell不感知margin，在父元素上设置table-row等属性，也会使其不感知height。IE6、7 不支持vertical-align这个样式。

二、使用line-height 及 vertical-align
>设置 .content 元素的 display 为 inline-block。作用在于既能重置外部的 line-height 为正常大小，又能保持行内元素特性，从而可以设置 vertical-align 属性;因为行内元素默认都是基线对齐的，所以我们通过对 .content 元素设置 vertical-align: middle; 来调整多行文本的垂直位置，从而实现我们想要的“垂直居中”效果。这种方式也适用于 图片等替换元素 的垂直居中效果。

```
.main {
    width: 300px;
    background-color: #50ba8b;

    line-height: 300px;
}

.content {
    display: inline-block;
    background-color: #5b4d4e;
    color: #FFFFFF;
    line-height: 20px;
    margin: 0 20px;
    vertical-align: middle;
}
<div class="main">
    <span class="content">
        我是要居中的行内元素span <br>
        我是要居中的行内元素span
    </span>
</div>
```

##水平垂直居中
一、使用absolute和负margin对元素进行水平垂直居中（已知元素宽度高度）
>首先用绝对定位（top: 50%;left: 50%;）使子元素左上角定位到父级元素的正中当使用， 因为是以左上角为原点，故不处于中心位置


```
    <style>
        .content{
            position: relative;
            width: 400px;
            height: 400px;
            background: pink;
        }
        .top{
            width: 100%;
            height: 50%;
            border-bottom: 1px solid black;
        }
        .main{
            width: 100px;
            height: 100px;
            background: deeppink;
            position: absolute;
            top: 50%;
            left:50%;
        }
    </style>
    <div class="content">
    <div class="top"></div>
    <div class="main"></div>
</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/positionfumargin.png)
>margin-top: -50px;margin-left: -50px;使元素本身向上和向左移动自己width和height的一半达到居中效果。

 ![行内元素水平居中](/Users/zengyuan/Desktop/image/positionfumargin1.png)
优点：可对脱离文档流的元素实现居中，适用于所有浏览器。

缺点：必须声明外部容器元素的height和必须提前知道被居中块级元素的尺寸，否则无法准确实现垂直居中。



 
二、使用absolute和transfrom元素进行垂直居中（未知元素的宽度和高度）

>首先用绝对定位（top: 50%;left: 50%;）使子元素左上角定位到父级元素的中心， 因为是以左上角为原点，故不处于中心位置

```
  <style>
        .content{
            position: relative;
            width: 300px;
            height: 300px;
            background: pink;
        }
        .top{
            width: 100%;
            height: 50%;
            border-bottom: 1px solid black;
        }
        .top-info{
            width: 50%;
            height: 100%;
            border-right: 1px solid black;
        }
        .content2{
            width: 50%;
            height: 100%;
            border-right: 1px solid black;
        }
        .main{
            position: absolute;
            top: 50%;
            left: 50%;
            width: 100px;
            height: 100px;
            background: deeppink;
        }
    </style>
    <div class="content">
    <div class="top">
        <div class="top-info"></div>
    </div>
    <div class="content2"></div>
    <div class="main">
    </div>
	</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/positionfumargin.png)
 
>再使用transform:translate(-50%,-50%) 使子元素往上（x轴）,左（y轴）移动自身长宽的 50%，以使其居于中心位置。

 ![行内元素水平居中](/Users/zengyuan/Desktop/image/positionfumargin1.png)

缺点：CSS transform 在部分就浏览器上需要使用 前缀;IE9(-ms-), IE10+以及其他现代浏览器才支持，有浏览器兼容问题；外部容器需要设置height；如果内容包含文字，现在的浏览器合成技术会使文字模糊不清。

优点：tranlate（）函数中的百分比是相对于自身宽高的百分比在不知道自身宽高的情况下，可以利用它来进行水平垂直居中。

三、使用absolute和margin：auto实现元素水平垂直居中（已知元素宽高） 
   
```
<style>
        .content{
            position: relative;
            width: 300px;
            height: 300px;
            background: pink;
            text-align: center;

        }
        .main{
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;
            width: 100px;
            height: 100px;
            background: deeppink;
        }
    </style>

</head>
<body>
<div class="content">
    <div class="main">
    </div>
</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/dingwei.png)
 优点：简单
 缺点：此法同样只适用于那些我们已经知道它们的宽度或高度的元素，IE(IE8 beta)中无效，它只支持IE9+,谷歌，火狐等符合w3c标准的现代浏览器。

四、使用display：table-cell；将元素转换成表格样式(类似td和th)，再利用表格的样式来进行居中(未知元素宽高)。

```
    <style>
        .content{
            display: table-cell;
            vertical-align: middle;
            text-align: center;
            width: 300px;
            height: 300px;
            background: pink;
        }
        .main{
            display: inline-block;
            width: 100px;
            height: 100px;
            background: deeppink;
        }
    </style>
    <div class="content">
    	<div class="main"></div>
	 </div>
```

 ![行内元素水平居中](/Users/zengyuan/Desktop/image/dingwei.png)
优点：使父元素内的所有行内元素水平垂直居中（内部div设置display:inline-block即可）。这在子元素不确定宽高和数量时，特别实用！
缺点：table-cell同样会被其他一些CSS属性破坏，float, position:absolute，所以，在使用display:table-cell与float:left或是position:absolute属性尽量不同用。IE6、7 不支持vertical-align这个样式。
 
 

###使用弹性布局（display:flex）实现元素居中


>弹性布局适应不同屏幕的大小和不同的设备类型。主要思想是给予容器控制内部元素高度和宽度的能力。目前已得到以下浏览器支持：

 ![行内元素水平居中](/Users/zengyuan/Desktop/image/liulanqi.png)
实现元素居中使用的属性如下：


* display：flex/inline-flex（内联块级）；适用需要居中元素的父类容器上；
* justify-content:center; 该属性定义了项目在主轴上的对齐方式。属性值center使元素垂直居中。
* align-items: center;属性定义项目在交叉轴上如何对齐。属性值center使元素水平居中。

优点：简单，方便，可以不用知道子元素的宽高，。

缺点：使用flex容器内元素，即flex item的float，clear、vertical-align属性将失效。由于现在弹性盒子是css3的新的布局模式，所以有些浏览器还没有兼容，需要添加一些浏览器前缀，以达到兼容的效果。

一. 单个元素水平居中

在这段代码里我们只需要给h1标签的父元素添加两个属性就可以了，justify-content其作用就是 让class类为box的div盒子居中。盒 子居中了，盒子里面的元素就自然居中了，他的好处就是不需要对需居中的元素（h1）设置任何样式，如果：width，margin。

 
 
```
    <style>
        .content{
            display: flex;
            width: 100%;
            background: pink;
            justify-content: center;
        }
        .main{
            font-size: 1rem;
            padding: 1rem;
            border: 1px dashed #FFF;
            color: #FFF;
            font-weight: normal;
        }
    </style>
    <div class="content">
    <div class="main">
        flex弹性布局使元素居中
    </div>
	</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/flex单行.png)

二. 多个元素水平居中
 
```
     <style>
        .content{
            display: flex;
            width: 100%;
            background: pink;
            justify-content: center;
        }
        .main{
            font-size: 1rem;
            padding: 1rem;
            border: 1px dashed #FFF;
            color: #FFF;
            font-weight: normal;
        }
    </style>
    
    <div class="content">
    <div class="main">
        flex弹性布局使元素居中
    </div>
    <div class="main">
        flex弹性布局使元素居中
    </div>
    <div class="main">
        flex弹性布局使元素居中
    </div>
	</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/flexduohang.png)
 
3. 单个元素垂直居中

给父元素定义一个高，不需要给目标元素设置高度就能使元素垂直居中

```
    <style>
        .content{
            display: flex;
            width: 300px;
            height: 300px;
            background: pink;
            align-items: center;
        }
        .main{
            font-size: 1rem;
            padding: 1rem;
            border: 1px dashed #FFF;
            color: #FFF;
            font-weight: normal;
        }
    </style>
    <div class="content">
    <div class="main">
        flex弹性布局使元素居中
    </div>
	</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/flexchuizhidanhang.png)

4. 多行元素并排垂直居中

由于弹性容器.content添加了 display:flex; 属性，子元素默认是水平排列的，所以子元素不管多少个都是显示在一行。

```
    <title>块级元素居中</title>
    <style>
        .content{
            display: flex;
            width: 300px;
            height: 300px;
            background: pink;
            align-items: center;
        }
        .main{
            font-size: 1rem;
            padding: 1rem;
            border: 1px dashed #FFF;
            color: #FFF;
            font-weight: normal;
        }
    </style>
    <div class="content">
    <div class="main">
        flex弹性布局使元素居中
    </div>
    <div class="main">
        flex弹性布局使元素居中
    </div>
    <div class="main">
        flex弹性布局使元素居中
    </div>
	</div>
```

 ![行内元素水平居中](/Users/zengyuan/Desktop/image/flexchuizhiduohang.png)

5. 多行元素垂直居中 

使用 flex-direction:column; 主轴为竖直方向，属性使main元素以主轴从上往下排列。

```
    <style>
        .content{
            display: flex;
            width: 300px;
            height: 300px;
            background: pink;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }
        .main{
            font-size: 1rem;
            padding: 1rem;
            border: 1px dashed #FFF;
            color: #FFF;
            font-weight: normal;
        }
    </style>

<div class="content">
    <div class="main">
        flex弹性布局使元素居中
    </div>
    <div class="main">
        flex弹性布局使元素居中
    </div>
    <div class="main">
        flex弹性布局使元素居中
    </div>
</div>
```
 ![行内元素水平居中](/Users/zengyuan/Desktop/image/flexchuizhishuiping.png)


