## study
20190725
### css3实现旋转正方体
**过渡动画 transition**
过渡动画过渡的是操作的元素属性
可写在一块：
```
transition：all 0.5s easy-in-out 0.5s;
```
也可分开写：
```
transition-delay: 0.5s;过渡的时间延迟
transition-duration: 0.2s;过渡的时间
transition-property: all;过渡的属性
transition-timing-function: linear;  过渡的方式
```
**transform动画**
transform:平移值：translate(100px)  可以分为三种x,y,z  默认向右移动
旋转值：rotate(45deg)   分为x,y,z   默认z轴
伸缩动画scale: 一个值的时候等距伸缩  两个值的时候代表宽高比例 
skew:斜动画

**animation帧动画**
需要先用@keyframes定义动画，然后在加给需要此动画的div。
```
animation: animateInfo 5s linear infinite;
```
animateInfo为动画的名字，5s为动画的持续时间，linear为动画将匀速完成一个周期，infinite为动画的播放次数为循环

这个方法是把元素叠在一起在展开
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>旋转正方形</title>
    <style type="text/css">
        #d4{
            height: 180px;width: 180px;/*容器大小*/
            position: relative;/*相对定位*/
            margin: 200px auto;/*上下300,左右对齐*/
            transform: rotateX(30deg)rotateY(30deg);/*容器初始旋转角度沿着x，y轴3D旋转*/
            transform-style: preserve-3d;/*容器内元素随容器一起转*/
            animation: name 10s infinite ;/*设置旋转方式 设置循环播放次数*/
        }
        @-webkit-keyframes name{/*以百分比来规定改变发生的实践，from和to等价0到100%*/
            from{transform:rotateX(30deg) rotateY(30deg);}/*设置旋转起点*/
            to{transform:rotateX(30deg)  rotateY(390deg);}/*设置旋转终点*/
        }
        #d4 div{
            height: 180px;width: 180px;/*设置所有元素的大小*/
            position: absolute;/*绝对定位*/
            font-size: 70px;/*元素内字体大小*/
            border: 20px red double;/*设置元素边框*/
            line-height:180px ;/*设置文字高度与父级元素相等*/
            text-align: center;/*设置文字水平居中*/
        }
        #d4 div:nth-child(1){
            transform: rotateY(90deg);/*旋转方式*/
            transform-origin: right; /*以矩形右边框为Y轴*/
        }
        #d4 div:nth-child(2){
        }

        #d4 div:nth-child(3){
            transform: rotateY(-90deg);
            transform-origin: left;/*以矩形左边框为Y轴*/
        }
        #d4 div:nth-child(4){
            transform: translateZ(220px);/*沿Z轴平移*/
        }
        #d4 div:nth-child(5){
            transform: rotateX(-90deg);
            transform-origin: bottom; /*以矩形上边框为Y轴*/
        }
        #d4 div:nth-child(6){
            transform: rotateX(90deg);
            transform-origin: top; /*以矩形下边框为Y轴*/
        }
    </style>
</head>
<body>
<div id="d4">
    <div >1</div>
    <div >2</div>
    <div >3</div>
    <div >4</div>
    <div >5</div>
    <div >6</div>
</div>
</body>
</html>
```
