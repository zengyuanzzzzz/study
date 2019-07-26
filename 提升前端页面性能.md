## study
**20190725**
### 毫秒必争，前端网页性能最佳实践
你愿意为打开一个网页等待多长时间？我一秒也不愿意等。但是事实上大多数网站在响应速度方面都让人失望。现在越来越多的人开始建立自己的网站，博客，你的网页响应速度如何呢？在这篇文章中我们来介绍一下提高网页性能的最佳实践，以及相应的问题解决方案.
* 网页内容
  * 减少http请求次数
  * 减少DNS查询次数
  * 避免页面跳转
  * 缓存Ajax
  * 减少DOM元素数量
  * 根据域名划分内容
  * 减少iframe数量
  * 避免404
* 服务器
  * 使用GET Ajax请求
  * 使用CND
  * 配置ETags
  * 避免空的图片src
* Cookie
  * 减少Cookie大小
  * 页面内容使用无Cookie域名
* CSS
  * 将样式表置顶
  * 避免CSS表达式
  * 用<link>代替@import
  * 避免使用Filters
* JavaScript
  * 将脚本置地
  * 使用外部JavaScript和CSS文件
  * 精简JavaScript和CSS
  * 去除重复脚本
  * 减少DOM访问
  * 使用智能事件处理
* 图片
  * 优化图像
  * 优化CSS Sprite
  * 不要再HTML中缩放图片
  * 使用小且可缓存的favicon.ico
* 移动客户端
  * 保持单个内容小于25KB
  * 打包组建成符合文档
  
## 网页内容
### 减少http请求次数
减少请求次数是缩短响应时间的关键！可以通过简化页面设计来减少请求次数，但页面内容较多可以采用以下技巧。
1. 捆绑文件: 现在有很多现成的库可以帮你将多个脚本文件捆绑成一个文件，将多个样式表文件捆绑成一个文件，以此来减少文件的下载次数。例如在asp.net中可以使用ScriptManager，asp.net MVC中的Bundling。
2. CSS Sprites: 就是把多个图片拼成一副图片，然后通过CSS来控制在什么地方具体显示这整张图片的什么位置。给大家看个熟悉的Sprites实例。
```
.app-icon-read {
    background-position

: 0 0;

}
.app-icon {
    background

: url("/pics/app/app_icons_50_5.jpg") no-repeat scroll 0 0 transparent;


    border-radius: 10px 10px 10px 10px;
    box-shadow: 1px 1px 2px #999999;
    display: inline-block;
    height

: 50px;


    width

: 50px;

}
```
3.  Image Maps： 也是将多幅图拼在一起，然后通过坐标来控制显示导航。这里有个经典的例子，选中图片中的某个人就会将你带到不同的链接。

### 减少DNS查询次数
DNS查询也消耗响应时间，如果我们的网页内容来自各个不同的domain (比如嵌入了开放广告，引用了外部图片或脚本)，那么客户端首次解析这些domain也需要消耗一定的时间。DNS查询结果缓存在本地系统和浏览器中一段时间，所以DNS查询一般是对首次访问响应速度有所影响。下面是我清空本地dns后访问博客园主页dns的查询请求。看少去还不少哦。

### 避免页面跳转
当客户端收到服务器的跳转回复时，客户端再次根据服务器回复中的location指定的地址再次发送请求，例如以下跳转回复。

      HTTP/1.1 301 Moved Permanently
      Location: http://example.com/newuri
      Content-Type: text/html

当客户端遇到这种回复的时候，用户只能等待客户端再次发送请求，有的网站甚至会一直跳n次，跳到他想带你去的地方…当然在这个时候用户看不到任何页面内容，只有浏览器的进度条一直在刷新。

### 缓存Ajax
Ajax可以帮助我们异步的下载网页内容，但是有些网页内容即使是异步的，用户还是在等待它的返回结果，例如ajax的返回是用户联系人的下拉列表。所以我们还是要注意尽量应用以下规则提高ajax的响应速度。
* 添加Expires 或 Cache-Control报文头使回复可以被客户端缓存
* 压缩回复内容
* 减少dns查询
* 精简javascript
* 避免跳转
* 配置Etags


### 减少DOM元素数量
网页中元素过多对网页的加载和脚本的执行都是沉重的负担，500个元素和5000个元素在加载速度上会有很大差别。

想知道你的网页中有多少元素，通过在浏览器中的一条简单命令就可以算出，
```
document.getElementsByTagName('*').length
```
### 减少iframe数量
使用iframe要注意理解iframe的优缺点
优点
* 可以用来加载速度较慢的内容，例如广告。
* 安全沙箱保护。浏览器会对iframe中的内容进行安全控制。
* 脚本可以并行下载
缺点
* 即使iframe内容为空也消耗加载时间
* 会阻止页面加载
* 没有语义
### 避免404
404我们都不陌生，代表服务器没有找到资源，我们要特别要注意404的情况不要在我们提供的网页资源上，客户端发送一个请求但是服务器却返回一个无用的结果，时间浪费掉了。

更糟糕的是我们网页中需要加载一个外部脚本，结果返回一个404，不仅阻塞了其他脚本下载，下载回来的内容(404)客户端还会将其当成Javascript去解析。
## 服务器
### 使用GET Ajax请求
浏览器在实现XMLHttpRequest POST的时候分成两步，先发header，然后发送数据。而GET却可以用一个TCP报文完成请求。另外GET从语义上来讲是去服务器取数据，而POST则是向服务器发送数据，所以我们使用Ajax请求数据的时候尽量通过GET来完成。

### 避免空的图片src
空的图片src仍然会使浏览器发送请求到服务器，这样完全是浪费时间，而且浪费服务器的资源。尤其是你的网站每天被很多人访问的时候，这种空请求造成的伤害不容忽略。

浏览器如此实现也是根据RFC 3986 - Uniform Resource Identifiers标准，空的src被定义为当前页面。

所以注意我们的网页中是否存在这样的代码
```
straight HTML
<img src="">

JavaScript
var img = new Image();
img.src = "";
```
## Cookie
### 减少Cookie大小
Cookie被用来做认证或个性化设置，其信息被包含在http报文头中，对于cookie我们要注意以下几点，来提高请求的响应速度，

* 去除没有必要的cookie，如果网页不需要cookie就完全禁掉
* 将cookie的大小减到最小
* 注意cookie设置的domain级别，没有必要情况下不要影响到sub-domain
* 设置合适的过期时间，比较长的过期时间可以提高响应速度。
## CSS
### 将样式表置顶
经样式表(css)放在网页的HEAD中会让网页显得加载速度更快，因为这样做可以使浏览器逐步加载已将下载的网页内容。这对内容比较多的网页尤其重要，用户不用一直等待在一个白屏上，而是可以先看已经下载的内容。

如果将样式表放在底部，浏览器会拒绝渲染已经下载的网页，因为大多数浏览器在实现时都努力避免重绘，样式表中的内容是绘制网页的关键信息，没有下载下来之前只好对不起观众了。
### 避免CSS表达式
CSS表达式可以动态的设置CSS属性，在IE5-IE8中支持，其他浏览器中表达式会被忽略。例如下面表达式在不同时间设置不同的背景颜色。
```
background-color: expression( (new Date()).getHours()%2 ? "#B8D4FF" : "#F08A00" );
```
CSS表达式的问题在于它被重新计算的次数远比我们想象的要多，不仅在网页绘制或大小改变时计算，即使我们滚动屏幕或者移动鼠标的时候也在计算，因此我们还是尽量避免使用它来防止使用不当而造成的性能损耗。
如果想达到类似的效果我们可以通过简单的脚本做到。
```
<html>
<head>
</head>
<body>
<script type="text/javascript">
var currentTime = new Date().getHours();
if (currentTime%2) {
    if (document.body) {
        document.body.style.background = "#B8D4FF";
    }
}
else {
    if (document.body) {
        document.body.style.background = "#F08A00";
    }
}
</script>
</body>
</html>
```
### 用<link>代替@import
避免使用@import的原因很简单，因为它相当于将css放在网页内容底部。
## JavaScript
### 将脚本置地
HTTP/1.1 specification建议浏览器对同一个hostname不要超过两个并行下载连接， 所以当你从多个domain下载图片的时候可以提高并行下载连接数量。但是当脚本在下载的时候，即使是来自不同的hostname浏览器也不会下载其他资源，因为浏览器要在脚本下载之后依次解析和执行。

因此对于脚本提速，我们可以考虑以下方式
* 把脚本置底，这样可以让网页渲染所需要的内容尽快加载显示给用户。
* 现在主流浏览器都支持defer关键字，可以指定脚本在文档加载后执行。
* HTML5中新加了async关键字，可以让脚本异步执行。
### 使用外部JavaScript和CSS文件
使用外部Javascript和CSS文件可以使这些文件被浏览器缓存，从而在不同的请求内容之间重用。

同时将Javascript和CSS从inline变为external也减小了网页内容的大小。

使用外部Javascript和CSS文件的决定因素在于这些外部文件的重用率，如果用户在浏览我们的页面时会访问多次相同页面或者可以重用脚本的不同页面，那么外部文件形式可以为你带来很大的好处。但对于用户通常只会访问一次的页面，例如microsoft.com首页，那inline的javascript和css相对来说可以提供更高的效率。
### 精简JavaScript和CSS
精简就是将Javascript或CSS中的空格和注释全去掉，
```
body {
    line-height: 1;
}
ol, ul {
    list-style: none;
}
blockquote, q {
    quotes: none;
}
```
精简后版本
```
body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}
```
## 图片
### 优化图像
当美工完成了网站的图片设计后，我们可以在上传图片之前对其做以下优化
* 检查GIF图片中图像颜色的数量是否和调色板规格一致。如果你发现图片中只用到了4种颜色，而在调色板的中显示的256色的颜色槽，那么这张图片就还有压缩的空间。可以使用imagemagick检查：
identify -verbose image.gif 
* 尝试把GIF格式转换成PNG格式，看看是否节省空间。大多数情况下是可以压缩的。下面这条简单的命令可以安全地把GIF格式转换为PNG格式：
convert image.gif image.png 
* 在所有的PNG图片上运行pngcrush（或者其它PNG优化工具）。例如：
pngcrush image.png -rem alla -reduce -brute result.png 
* 在所有的JPEG图片上运行jpegtran。这个工具可以对图片中的出现的锯齿等做无损操作，同时它还可以用于优化和清除图片中的注释以及其它无用信息
jpegtran -copy none -optimize -perfect src.jpg dest.jpg 
