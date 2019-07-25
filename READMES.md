## study
20190725
你可以在很多地方看到三角形（小三角）：tooltips提示框、下拉菜单、甚至在loading载入动画里。不管你喜欢还是不喜欢，这些小元素对各UI元素之间的联系关系式很重要的。
下面我将介绍两种方法：
### CSS 边框
优点
* 很容易的通过修改一些CSS代码属性值而更改颜色和大小
* 这是一个跨浏览器的解决方案。

缺点
* 这个方式使用的是border,所以你不能添加阴影、渐变、和其他一些CSS3效果
* 请记住，IE6是不支持透明边界的-如果你关心这个问题
* 如果你使用火狐浏览器，要知道，CSS的“透明”有时可能不会是透明的，特别是在对角线边框，越多更多 here.
```
        .triangle{
            border-color: #57af1a #fff #fff #fff;
            border-style: solid;
            border-width: 100px 60px 0 60px;
            height:0;
            width: 0;
        }
 ```
 ![triangle](http://www.daqianduan.com/wp-content/uploads/2012/10/entity-triangle.png)
 
 ###HTML 字符
 它是基于使用可用的Unicode字符列表的字符。
优点
* 它是一个跨浏览器的技术
* 您可以使用CSS3的text-shadow属性添加阴影。

缺点
* 不能使用太多的CSS3效果，除了使用文字阴影。
* 在所有的浏览器，这是相当不可能实现像素完美。
```
        .entity-triangle{
            font-size: 12em;
            color: #f7931d;
            text-shadow: 0px 7px 3px red;
        }
 ```
 ![triangle](http://www.daqianduan.com/wp-content/uploads/2012/10/entity-triangle.png)
