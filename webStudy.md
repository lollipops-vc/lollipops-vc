# HTML

## 1，html5新特性

html的新特性主要表现再五个方面：声明方式，语义化标签，音频、视频，表单控件，5个API（本地存储、画布、地理、拖拽释放、Web Workers)。

### 1.1 声明方式

html4规定了三种声明方式：，分别是严格模式（Strict），过渡模式(Transitional )和框架集模式(Frameset)；而html5因为不是SGML的子集，只需要<!DOCTYPE>就可以了。

严格模式 Strict

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">
```

过渡模式 Transitional

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
```

框架集 Frameset

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN"
"http://www.w3.org/TR/html4/frameset.dtd">
```

html5

```
<!DOCTYPE html>
```

### 1.2 语义化标签

* header :表示头部内容
* nav：表示导航部分
* section:表示页面内的一个区块
* aside:表示侧边栏，包含与内容相关各种链接。它是特殊的section；如果aside标签被包含在article中时，作为主要内容的附属信息部分，其中的内容可以是与当前文章有关的相关资料、标签、名次解释等
* article:表示一个区块内的一个独立区域，定义一个文档，页面，或者网站中自成一体的内容
* footer:表示页面的底部部分

details 

summary 

dialog

```javascript
<header>
    <nav>导航栏</nav>
</header>
<section>
    <aside>侧边栏</aside>
    <article>独立内容</article>
</section>
<footer>尾部</footer>
```

优点：

1 语义化具有可读性，是的文档结构清晰

2 浏览器便于读取，易于SEO优化

3 展现在用户中，用户体验好

4 便于团队开发和维护

### 1.3 音频,视频

* audio:音频播放标签，同video标签的使用方法一样，但audio用于对音频的播放，支持的格式有：mp3、wav、ogg；

* video:视频播放标签，支持的播放格式有：ogg、mp3、webm；该标签可嵌套多个source标签用于表现同一个视频多种播放方式，当前一个视频格式不支持时就轮到下一个source标签直到有一个source标签内可以播放就停止向下寻找，如果没有一个可以播放的就展示当前的内容

相关属性:

* autoplay:自动播放,值为布尔值，当视频标签加载完成后会`自动播放`，但是若浏览器有限制自动播放的相关规定则会导致该属性失效。
* controls:音频或视频的控件显示，值为布尔值，或者称为`显示标签`的存在更合适
* loop:循环播放，值为布尔值，当视频或音频播放完后，会`自动继续`播放当前的文件
* muted:静音播放，值为布尔值，通常该属性配和autoplay和loop，可以使video标签一直`无声播放`视频
* poster:预先加载一个`图片在视频之前显示`，值为图片路径，通常称之为视频封面


### 1.4 表单控件

  html5拥有多个表单输入类型，这些新特性提供了更好的输入控制和验证

* color :颜色
* date:日期
* datetime
* datetime-local:含有本地时间的日历
* email :邮箱
* month
* number :数值
* range:范围控制
* search:搜索框
* tel:手机号
* time:时间
* url:网页地址
* week
* file:文本,上传多个文件加上multiple属性
* image:图片
* submit:提交
  表单属性:
* placeholder:占位符
* required:必填项
* autofocus:自动聚焦
* autocomplete:备选项,用于提示之前填写过的内容，再次填写时会自动提示；该属性的值为on或off，一般默认为on是打开的（email的是默认off关闭的）拥有自动完成功能。当用户在自动完成域中开始输入时，浏览器应该在该域中显示填写的选项。
* minlength/maxlength:用于规定最少字数和最长字数

### 1.5 5个API

#### 1.5.1本地存储

常用：localStorage

localStorage

本地离线存储，长期存储数据，浏览器关闭之后数据不会丢失

sessionStorage

浏览器关闭后自动删除

##### 衍生面试题:cookies、sessionStorage和localStorage解释及区别

**cookie和seesion**:cookie和session都是用来跟踪浏览器用户身份的会话方式

* 保持状态:cookie保存再浏览器端,session保存在服务器端

* 使用方式

  cookie:如果不在浏览器中设置过期时间,cookie被保存在内存中,生命周期随浏览器的关闭而结束,这种cookie简称会话cookie,如果设置了过期时间,cookie是被保存在硬盘中,关闭浏览器后,数据仍然存在,知道过期时间结束.cookie是服务器发送客户端的特殊信息,以文本的方式保存在客户端,每次请求都带上

  session:当服务器收到请求需要创建session机制,首先会检查客户端请求中是否包含sessionid,如果有,服务器根据id返回session对象.如果没有,服务器会创建新的session对象.并把sessionis在本次相应中返回给客户端,通常使用cookie方式存储sessionid到客户端，在交互中浏览器按照规则将sessionid发送给服务器。如果用户禁用cookie，则要使用URL重写，可以通过response.encodeURL(url) 进行实现；API对encodeURL的结束为，当浏览器支持Cookie时，url不做任何处理；当浏览器不支持Cookie的时候，将会重写URL将SessionID拼接到访问地址后。

* 存储内容:cookie只能存储字符串,session通过类似与Hashtable的数据结构来保存，能支持任何类型的对象(session中可含有多个对象)

* 存储大小:cookie,单个cookie不能超过4kb,session没有大小限制

* 安全性:

  cookie:cookie欺骗,cookie截获,session的安全性更高

  原因:

    (1) sessionID 存储在cookie中,若要攻破session,先要攻破cookie

    (2) seesionID 需要人登录,或者启动seesion_start,所以攻破cookie也不一定得到sessionID

    (3) 第二次启动session_start后，前一次的sessionID就是失效了，session过期后，sessionID也随之失效。

    (4) sessionID是加密的

* 应用场景:

  cookie:         

  （1）判断用户是否登录过网站，以便下次登录时能够实现自动登录（或者记住密码）。
  （2）保存上次登录的事件等信息。
  （3）保存上次查看的页面
  （4）浏览计数

  seesion:

  （1）网上商城中的购物车
  （2）保存用户登录信息
  （3）将某些数据放入session中，供同一用户的不同页面使用
  （4）防止用户非法登录

* 缺点

  cookie:

  （1）大小受限
  （2）用户可以操作（禁用）cookie，使功能受限
  （3）安全性较低
  （4）有些状态不可能保存在客户端
  （5）每次访问都要传送cookie给服务器，浪费宽带
  （6）cookie数据有路径（path）的概念，可以限制cookie只属于某个路径下。

  seesion:

  （1）session保存的东西越多，就越占用服务器内存，对于用户在线人数较多的网站，服务器的内存压力会比较大
  （2）依赖于cookie（sessionid保存在cookie），如果禁用cookie，则要使用URL重写
  （3）创建session变量有很大的随意性，可随时调用，不需要开发者做精确地处理，所以过度的使用session变量将会导致代码不可读而且不好维护。

  **WebStorage:** **localStorage（本地存储）**和**sessionStorage（会话存储）**

* 生命周期

localStorage的生命周期是永久的，关闭页面或浏览器之后localStorage中的数据也不会消失。localStorage除非主动删除数据，否则数据永远不会消失。
sessionStorage的生命周期是仅在当前会话下有效。sessionStorage引入了一个“浏览器窗口”的概念，sessionStorage是在同源的窗口中始终存在的数据。只要这个浏览器窗口没有关闭，即使刷新页面或者进入同源另一个页面，数据依然存在。但是sessionStorage在关闭了浏览器窗口后就会被销毁。同时独立的打开同一个窗口同一个页面，sessionStorage也是不一样的。

* 存储大小

localStorage和sessionStorage的存储数据大小一般都是：5MB

* 存储位置

localStorage和sessionStorage都保存在客户端，不与服务器进行交互通信

* 存储内容类型

localStorage和sessionStorage只能存储字符串类型，对于复杂的对象可以使用ECMAScript提供的JSON对象的stringify和parse来处理

* 获取方式

localStorage：window.localStorage
sessionStorage：window.sessionStorage

* 应用场景

localStorage：常用于长期登录（+判断用户是否已登录），适合长期保存在本地的数据
sessionStorage：敏感账号一次性登录

**WebStorage的优点:**

（1）存储空间更大：cookie为4KB，而WebStorage是5MB

（2）节省网络流量：WebStorage不会传送到服务器，存储在本地的数据可以直接获取，也不会像cookie一样每次请求都会传送到服务器，所以减少了客户端和服务端的交互，节省了网络流量

（3）对于那种只需要在用户浏览一组页面期间保存而关闭浏览器后就可以丢弃的数据，sessionStorage会非常方便

（4）快速显示：有的数据存储在WebStorage上再加上浏览器本身的缓存。获取数据时可以从本地获取会比从服务器端获取快得多，所以速度更快

（5）安全性：WebStorage不会随着HTTP header发送到服务器端，所以安全性相对于cookie来说会比较高一些，不会担心截获，但是仍然存在伪造问题

（6）WebStorage提供了一些方法，数据操作比cookie方便

#### 1.5.2 地理 Geolocation

地理位置API允许用户向Web应用程序提供他们的位置，处于隐私考虑，报告地理位置前会先请求用户许可。

#### 1.5.3 拖拽释放

使元素可拖动，把 draggable 属性设置为 true ：

#### 1.5.4 画布 Canvas

可以用作图形的容器处理，可以很简单画出一些图像不需要借用别的图片，比如一个简单的时钟就完全可以由canvas很简单的画出，节约资源

svg绘图:使用xml描述2D图形的语言

SVG（可缩放矢量图形（Scalable Vector Graphics））表示可缩放矢量图形。他是基于文本的图形语言，使用文本，线条，点等来进行图像绘制，这使得他轻便，显示更加迅速。

相关属性:

* version:相关的xml的版本号

* circle:画圆

  cx:x轴

  cy:y轴

  r:半径

  stroke:外边线条的颜色

  stroke-width:外边线条的宽度

  fill:圆的填充色

* rect:矩形

  x:x轴

  y:y轴

  width:宽

  height:高

  fill:填充色

  stroke:外边实心线

  stroke-width:外边实心线的宽度

* polygon:折线
    points:坐标值,每个点的坐标值用空格区分开,最后链接再一起形成图像

#### 1.5.5 Web Worker

web worker 是运行在后台的JavaScript，独立与其他脚本，不会影响页面的性能，可以后台运行

作用：为JavaScript创造多线程环境，允许主线程创建Worker线程，将一些任务分配给后者运行。在主线程运行的同时，Worker线程在后台运行，两者互不干扰。等到Worker线程完成计算任务，再将结果返回给主线程。这样的好处就是，一些计算密集型或者高延迟的任务，被Worker线程负担了，主线程（通常负责UI交互)就会很流畅，不会被阻塞或拖慢。

## 2,浏览器内核

理解:渲染引擎(Layout Engine或Rendering Engine)和JS引擎。

渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。
JS引擎：解析和执行javascript来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

常见的浏览器内核和对应浏览器

- `Trident`：IE内核
- `Gecko`：Firefox内核
- `Presto`：Opera前内核(已废弃)
- `Webkit`：Safari内核，Chrome内核原型，开源
- `Blink`：由Google和Opera Software开发，Chrome（28及往后版本）、Opera（15及往后版本）和Yandex浏览器中使用

## 3,defer和async的区别

没有`defer`或`async`，浏览器在遇到`script`标签后，会立即加载并执行标签中的脚本，“立即”指的是在渲染该`script`标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。

有`defer`，加载后续文档元素的过程将和`script.js`的加载并行进行（异步），但是`script.js`的执行要在所有元素解析完成之后，`DOMContentLoaded`事件触发之前完成。

有`async`，加载和渲染后续文档元素的过程将和`script.js`的加载并行进行（异步），但当`script.js`加载完后会立即执行，即停止加载和渲染后续文档元素，执行`script.js`。

```
<script>
<script defer>
<script async>
```



# css

## 1,css3新特性

### 1.1选择器

伪元素选择器

::before

::after

::first-line

::first-letter

::section

伪类选择器：

.list>li:first-child     选中第一个子元素

.list>li:last-child     选中最后一个子元素

.list>li:nth-child(n)  选中第五个子元素

.list>li:nth-child(odd)  选中偶数行

.list>li:nth-child(even)  选中奇数行

.list>li:nth-child(2n)  支持数学表达式，选中偶数行

.list>:nth-of-type(1)  选择类型匹配的，选中的是第五个li,跳过ul中其他类型

其他常用特性：

阴影

边线

弧度

滤镜

背景的扩充

定位（display）

### 1.2 媒体查询

css2中已经存在了媒体查询,最开始用来指定对应的设备，如tv表示电视、screen表示电 脑、print表示打印机；css3提供了媒体查询，主要针对不同分辨率的屏幕

```

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>@media</title>
		<style type="text/css">
			/* 当屏幕像素达到1500px以上,背景显示橙色 */
			@media only screen and (min-width: 1500px) {
			.example {background: orange;}
			}
			/* 当屏幕像素在600px到1200px之间,背景显示粉色 */
			@media only screen and (max-width: 1200px) and (min-width: 600px){
			.example {background: pink;}
			}
			
		</style>
	</head>
	<body>
		<div class="example">
			这是一个关于媒体样式的例子
		</div>
	</body>

```

###   1.3 @font-face字体

```

@font-face
{
font-family: myFirstFont;
src: url('/example/css3/Sansation_Light.ttf')
,url('/example/css3/Sansation_Light.eot'); /* IE9+ */
}
div
{
font-family:myFirstFont;
```

### 1.4 css3的变换效果

**transform 主要用来实现变幻效果**

```
2D效果：

平移动画：translate(x轴的位置，y轴的位置)          Eg:  transform:translate(100px,200px)

缩放动画：scale(数值)                            Eg:  transform:scale(1.5)

旋转动画：rotate(数值+弧度deg)                    Eg:  transform:rotate(20deg)

倾斜动画：skew(x轴deg,y轴deg)                    Eg: transform:skew(20deg,30deg)旋转x轴y轴

3D效果：

rotateX()方法，围绕其在一个给定度数X轴旋转的元素。Eg：transform:rotateX(50deg);
```

### 1.5 css3过渡效果

![](D:\workSpace\noteBook\css01.png)

### 1.6 css3帧动画

![](D:\workSpace\noteBook\css02.png)

### 1.7 渐变（Gradients）

- **线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向**

  background-image: linear-gradient(direction, color-stop1, color-stop2, ...);

- **径向渐变（Radial Gradients）- 由它们的中心定义**

- background: radial-gradient(center, shape size, start-color, ..., last-color);

### 1.8 css3多列

column-count 属性指定了需要分割的列数

![](D:\workSpace\noteBook\css03.png)

## 2,rgba()和opacity的透明效果有什么不同

rgba()和opacity都能实现透明效果，但最大的不同是opacity作用于元素，以及元素内的所有内容的透明度，

而rgba()只作用于元素的颜色或其背景色。（设置rgba透明的元素的子元素不会继承透明效果！）

## 3,css盒子模型

标准盒子模型：宽度=内容的宽度（content）+ border + padding + margin
低版本IE盒子模型：宽度=内容宽度（content+border+padding）+ margin

box-sizing属性：

用来控制元素的盒子模型的解析模式，默认为content-box
context-box：W3C的标准盒子模型，设置元素的 height/width 属性指的是content部分的高/宽
border-box：IE传统盒子模型。设置元素的height/width属性指的是border + padding + content部分的高/宽
4，css选择器

CSS选择符：id选择器(#myid)、类选择器(.myclassname)、标签选择器(div, h1, p)、相邻选择器(h1 + p)、子选择器（ul > li）、后代选择器（li a）、通配符选择器（*）、属性选择器（a[rel=”external”]）、伪类选择器（a:hover, li:nth-child）

可继承的属性：font-size, font-family, color

不可继承的样式：border, padding, margin, width, height

优先级（就近原则）：!important > [ id > class > tag ]
!important 比内联优先级高

## 4，盒子居中

方法一：定位

```
.parent{

position:relative;

}

.child{

position:absolute;

top:50%;

left:50%;

margin-top:-50px;

margin-left:-50px;

}
```

方法二：margin：auto

```
.parent{

position:relative;

}

.child{

position:absolute;

margin:auto;

top:0;

left:0;

right:0;

bottom:0;

}
```

方法三：利用display:table-cell

```
.parent{

display:table-cell;

vertical-align:middle;

text-align:center;

}

.child{

display:inline-block;

}
```

方法四：利用display：flex;设置垂直水平都居中；

```
.parent{

display:flex;

justify-content:center;

align-items:center;

}
```

方法五：计算父盒子与子盒子的空间距离（直接移动的px，与方法一思路一样）

方法六：利用transform

```
.parent{

position:relative;

}

.child{

position:absolute;

top:50%;

left:50%;

transform:translate(-50%,-50%);

}
```

方法七：利用calc计算

```
.parent{

position:relative;

}

.child{

position:absolute;

top:calc(200px);//（父元素高-子元素高）÷ 2=200px

let:calc(200px);//（父元素宽-子元素宽）÷ 2=200px

}
```

## 5,CSS中link和@import的区别是：

Link属于html标签，而@import是CSS中提供的

在页面加载的时候，link会同时被加载，而@import引用的CSS会在页面加载完成后才会加载引用的CSS

@import只有在ie5以上才可以被识别，而link是html标签，不存在浏览器兼容性问题

Link引入样式的权重大于@import的引用（@import是将引用的样式导入到当前的页面中）

# JavaScript

## 1,typeof会有哪些返回值

Typeof可以判断的简单数据类型："number"、"string"、"boolean"、"object"、"function" 和 "undefined"。

注意:typeof (null )=  "object"

## 2,数组方法:

　　数组总共有22种方法，本文将其分为对象继承方法、数组转换方法、栈和队列方法、数组排序方法、数组拼接方法、创建子数组方法、数组删改方法、数组位置方法、数组归并方法和数组迭代方法共10类来进行详细介绍

### **对象继承方法**:toString(),toLocaleString(),alueOf()

数组是一种特殊的对象，继承了对象Object的toString()、toLocaleString()和valueOf()方法

* **toString()**:

  返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串,该方法的返回值与不使用任何参数调用join()方法返回的字符串相同,　由于alert()要接收字符串参数，它会在后台调用toString()方法，会得到与toString()方法相同的结果

  ```
  alert([1,2,3]);//'1,2,3'
  ```

  

* **toLocaleString()**:

toLocaleString()是toString()方法的本地化版本，经常返回与toString()方法相同的值，如果数组中的某一项的值是null或者undefined，则该值在toLocaleString()和toString()方法返回的结果中以空字符串表示

```
var colors = [1,undefined,2,null,3];
console.log(colors.toString());//'1,,2,,3'
console.log(colors.toLocaleString());//'1,,2,,3'
```

* **valueOf()**:返回数组对象本身

  

### **数组转换方法**:join(),

* **join()**:Array.join()方法是String.split()方法的逆向操作，后者是将字符串分割成若干块来创建一个数组

  　　数组继承的toLocaleString()和toString()方法，在默认情况下都会以逗号分隔的字符形式返回数组项；而join()方法可以使用不同的分隔符来构建这个字符串，join()方法只接收一个参数，用作分隔符的字符串，然后返回包含所有数组项的字符串

    　　如果不给join()方法传入任何值，则使用逗号作为分隔符.

若join()方法的参数是undefined，标准浏览器以逗号为分隔符返回字符串，而IE7-浏览器以'undefined'为分隔符返回字符串

如果数组中的某一项的值是null或者undefined，则该值在join()方法返回的结果中以空字符串表示

### **栈和队列方法**:push(),pop(),shift(),unshift()

* **push()**:　push()方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。所以，该数组会改变原数组

如果需要合并两个数组，可以使用apply方法:

```
var a = [1, 2, 3];
var b = [4, 5, 6];
console.log(a,Array.prototype.push.apply(a, b));//[1,2,3,4,5,6] 6
```

[注意]如果使用call方法，则会把数组b整体看成一个参数

```
var a = [1, 2, 3];
var b = [4, 5, 6];
console.log(a,Array.prototype.push.call(a, b));//[1,2,3,[4,5,6]] 4
```

* **pop()**:pop()方法从数组末尾移除最后一项，减少数组的length值，然后返回移除的项。所以，该数组会改变原数组

  对空数组使用pop()方法，不会报错，而是返回undefined

* **shift()**:移除数组中的第一个项并返回该项，同时数组的长度减1。所以，该数组会改变原数组

​       对空数组使用shift()方法，不会报错，而是返回undefined

* **unshift()**:在数组前端添加任意个项并返回新数组长度。所以，该数组会改变原数组

​       当使用多个参数调用unshift()时，参数是一次性插入的而非一次一个地插入。这意味着最终的数组中插入的元素的顺序和它们在参数列表中的顺序一致

```
var a = ['a', 'b', 'c'];
console.log(a,a.unshift('x','y','z')); //['x','y','z','a', 'b', 'c'] 6
```

### **数组排序方法**:reverse(),sort()

* **reverse()**:用于反转数组的顺序，返回经过排序之后的数组；而原数组顺序也发生改变

* **sort()**:默认情况下，sort()方法按字符串升序排列数组项，sort方法会调用每个数组项的toString()方法，然后比较得到的字符串排序，返回经过排序之后的数组，而原数组顺序也发生改变

​       如果数组包含undefined元素，它们会被排到数组的尾部

```
var array = ['3',3,undefined,2,'2'];
console.log(array,array.sort());//["2", 2, "3", 3, undefined] ["2", 2, "3", 3, undefined]
```

　sort()方法可以接受一个比较函数作为参数，以便指定哪个值在哪个值的前面。比较函数接收两个参数，如果第一个参数应该位于第二个参数之前则返回一个负数，如果两个参数相等则返回0，如果第一个参数应该位于第二个参数之后则返回一个正数

```
function compare(value1,value2){
    if(value1 < value2){
        return -1;
    }else if(value1 > value2){
        return 1;
    }else{
        return 0;
    }
}
var array = ['5px',50,1,10];
//当数字与字符串比较大小时，字符串'5px'会被转换成NaN，这样结果就是false
console.log(array.sort(compare));//["5px",1, 10, 50]

```

使用sort()方法创建一个随机数组:

```
function compare(){
    return Math.random() - 0.5;
}
var array = [1,2,3,4,5];
console.log(array.sort(compare));//[2,1,5,4,3]
```

### **数组拼接方法**:concat()

* **concat()**:　concat()方法基于当前数组中的所有项创建一个新数组，先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。所以concat()不影响原数组

  　　如果不给concat()方法传递参数时，它只是复制当前的数组；如果参数是一个或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中；如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾

　         如果不提供参数，concat()方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是如果  数组成员包括复合类型的值（比如对          象），则新数组拷贝的是该值的引用

```
//该方法实际只复制了数组的第一维，数组第一维存放的是第二维的引用，而第二维才是实际存放他们的内容
var numbers = [1,2];
var newNumbers = numbers.concat();
console.log(numbers,newNumbers);//[1,2] [1,2]
numbers[0] = 0;
console.log(numbers,newNumbers);//[0,2] [1,2]

var numbers = [[1,2]];
var newNumbers = numbers.concat();
console.log(numbers,newNumbers);//[[1,2]] [[1,2]]
numbers[0][0] = 0;
console.log(numbers,newNumbers);//[[0,2]] [[0,2]]
```

concat()方法也可以用于将对象合并为数组，但是必须借助call()方法

```
var newArray = Array.prototype.concat.call({ a: 1 }, { b: 2 })
console.log(newArray);// [{ a: 1 }, { b: 2 }]
console.log(newArray[0].a);//1
```

### **创建子数组方法**:slice()

* **slice()**:slice()方法基于当前数组中的一个或多个项创建一个新数组，接受一个或两个参数，即要返回项的起始和结束位置，最后返回新数组，所以slice()不影响原数组

  　　slice(start,end)方法需要两个参数start和end，返回这个数组中从start位置到(但不包含)end位置的一个子数组；如果end为undefined或不存在，则返回从start位置到数组结尾的所有项

    　　如果start是负数，则start = max(length + start,0)

    　　如果end是负数，则end = max(length + end,0)

    　　start和end无法交换位置

    　　如果没有参数，则返回原数组

slice()方法涉及到Number()转型函数的隐式类型转换，当start被转换为NaN时，相当于start = 0；当end被转换为NaN时(end为undefined除外)，则输出空数组

```
var numbers = [1,2,3,4,5];
console.log(numbers.slice(NaN));//[1,2,3,4,5]
console.log(numbers.slice(0,NaN));//[]
console.log(numbers.slice(true,[3]));//[2,3]
console.log(numbers.slice(null,undefined));//[1,2,3,4,5]
console.log(numbers.slice({}));//[1,2,3,4,5]
```

　可以使用slice()方法将类数组对象变成真正的数组

```
var arr = Array.prototype.slice.call(arrayLike);

Array.prototype.slice.call({ 0: 'a', 1: 'b', length: 2 })// ['a', 'b']
Array.prototype.slice.call(document.querySelectorAll("div"));
Array.prototype.slice.call(arguments);
```

### **数组删改方法**:splice()

* **splice()**:splice()和slice()拥有非常相似的名字，但它们的功能却有本质的区别。splice()方法用于删除原数组的一部分成员，并可以在被删除的位置添加入新的数组成员，该方法会改变原数组

  　　splice()返回一个由删除元素组成的数组，或者如果没有删除元素就返回一个空数组

    　　splice()的第一个参数start指定了插入或删除的起始位置。如果start是负数，则start = max(length + start,0)；如果start是NaN，则相当于start = 0,第二个参数number指定了应该从数组中删除的元素的个数。如果省略第二个参数，从起始点开始到数组结尾的所有元素都将被删除。如果number是负数或NaN或undefined，则number=0，因此不删除元素

  ​       如果只提供一个元素，相当于将原数组在指定位置拆分成两个数组

```
var a = [1,2,3,4,5,6,7,8];
console.log(a,a.splice());// [1,2,3,4,5,6,7,8] []
var a = [1,2,3,4,5,6,7,8];
console.log(a,a.splice(4));// [1,2,3,4] [5,6,7,8]
var a = [1,2,3,4,5,6,7,8];
console.log(a,a.splice(-9));//max(-9+8,0)=0 [] [1,2,3,4,5,6,7,8]
var a = [1,2,3,4,5,6,7,8];
console.log(a,a.splice(NaN));//[] [1,2,3,4,5,6,7,8]
var a = [1,2,3,4,5,6,7,8];
console.log(a,a.splice(1,NaN));//[1,2,3,4,5,6,7,8] []
var a = [1,2,3,4,5,6,7,8];
console.log(a,a.splice(1,undefined));//[1,2,3,4,5,6,7,8] []
//如果后面还有更多的参数，则表示这些就是要被插入数组的新元素
var a = [1,2,3,4,5];
console.log(a,a.splice(2,0,'a','b'));//[1,2,'a','b',3,4,5] []
console.log(a,a.splice(2,2,[1,2],3));//[1,2,[1,2],3,3,4,5] ['a','b']
```

### **数组位置方法**:indexOf(),lastIndexOf()

* **indexOf()**:indexOf(search,start)方法接收search和start两个参数，返回search首次出现的位置，如果没有找到则返回-1

  　　search参数表示要搜索的项；使用严格相等运算符（===）进行比较

```
var arr = [1,2,3,'1','2','3'];
console.log(arr.indexOf('2'));//4
console.log(arr.indexOf(3));//2
console.log(arr.indexOf(0));//-1
```

　start参数表示该搜索的开始位置，该方法会隐式调用Number()转型函数，将start非数字值(undefined除外)转换为数字。若忽略该参数或该参数为undefined或NaN时，start = 0

```
var arr = ['a','b','c','d','e','a','b'];
console.log(arr.indexOf('a',undefined));//0
console.log(arr.indexOf('a',NaN));//0
console.log(arr.indexOf('a',1));//5
```

indexOf()方法兼容写法

```
if (typeof Array.prototype.indexOf != "function") {
  Array.prototype.indexOf = function (searchElement, fromIndex) {
    var index = -1;
    fromIndex = fromIndex * 1 || 0;
    for (var k = 0, length = this.length; k < length; k++) {
      if (k >= fromIndex && this[k] === searchElement) {
          index = k;
          break;
      }
    }
    return index;
  };
}
```

* **lastIndexOf()**:与indexOf()不同，lastIndexOf()从右向左查找

  　　lastIndexOf(search,start)方法接收search和start两个参数，返回search第一次出现的位置，如果没有找到则返回-1

    　　search参数表示要搜索的项；使用严格相等运算符（===）进行比较

```
var arr = [1,2,3,'1','2','3'];
console.log(arr.lastIndexOf('2'));//4
console.log(arr.lastIndexOf(3));//2
console.log(arr.lastIndexOf(0));//-1
```

　　start表示该搜索的开始位置，该方法会隐式调用Number()转型函数，将start非数字值(undefined除外)转换为数。若忽略该参数或该参数为undefined或NaN时，start = 0

　　与字符串的lastIndexOf()方法不同，当search方法为负数时，search = max(0,length+search)

```
var arr = ['a','b','c','d','e','a','b'];
console.log(arr.lastIndexOf('b'));//6
console.log(arr.lastIndexOf('b',undefined));//-1
console.log(arr.lastIndexOf('a',undefined));//0
console.log(arr.lastIndexOf('b',NaN));//-1
console.log(arr.lastIndexOf('b',1));//1
console.log(arr.lastIndexOf('b',-1));//max(0,-1+7)=6; 6
console.log(arr.lastIndexOf('b',-5));//max(0,-5+7)=2; 1
console.log(arr.lastIndexOf('b',-50));//max(0,-50+7)=0; -1
```

【tips】返回满足条件的项的所有索引值

　　可以通过循环调用indexOf()或lastIndexOf()来找到所有匹配的项

```
function allIndexOf(array,value){
    var result = [];
    var pos = array.indexOf(value);
    if(pos === -1){
        return -1;
    }
    while(pos > -1){
        result.push(pos);
        pos = array.indexOf(value,pos+1);
    }
    return result;
}
var array = [1,2,3,3,2,1];
console.log(allIndexOf(array,1));//[0,5]   
```

lastIndexOf()方法兼容写法 

```
if (typeof Array.prototype.lastIndexOf != "function") {
  Array.prototype.lastIndexOf = function (searchElement, fromIndex) {
    var index = -1, length = this.length;
    fromIndex = fromIndex * 1 || length - 1;
    for (var k = length - 1; k > -1; k-=1) {
        if (k <= fromIndex && this[k] === searchElement) {
            index = k;
            break;
        }
    }
    return index;
  };
}
```

### **数组归并方法**:reduce(),reduceRight()

* **reduce()**:

reduce()方法需要两个参数。第一个是执行化简操作的函数。化简函数的任务就是用某种方法把两个值组合或化简为一个值，并返回化简后的值

　　化简函数接受四个参数，分别是：

　　【1】初始变量，默认为数组的第一个元素值。函数第一次执行后的返回值作为函数第二次执行的初始变量，依次类推

　　【2】当前变量，如果指定了第二个参数，则该变量为数组的第一个元素的值，否则，为第二个元素的值

　　【3】当前变量对应的元素在数组中的索引(从0开始)

　　【4】原数组对象

　　化简函数的这四个参数之中，只有前两个是必须的，后两个则是可选的

```
var a = [1,2,3,4,5];
var sum = a.reduce(function(x,y){return x+y},0);//数组求和
var product = a.reduce(function(x,y){return x*y},1);//数组求积
var max = a.reduce(function(x,y){return (x>y)?x:y;});//求最大值
```

在空数组上，不带初始值参数调用reduce()将导致类型错误异常。如果调用它的时候只有一个值——数组只有一个元素并且没有指定初始值，或者有一个空数组并且指定一个初始值——reduce()只是简单地返回那个值而不会调用化简函数

```
var arr = [];
arr.reduce(function(){});//Uncaught TypeError: Reduce of empty array with no initial value

var arr = [];
arr.reduce(function(){},1);//1
```

reduce()方法兼容写法

```
if (typeof Array.prototype.reduce != "function") {
  Array.prototype.reduce = function (callback, initialValue ) {
     var previous = initialValue, k = 0, length = this.length;
     if (typeof initialValue === "undefined") {
        previous = this[0];
        k = 1;
     }
    if (typeof callback === "function") {
      for (k; k < length; k++) {
         this.hasOwnProperty(k) && (previous = callback(previous, this[k], k, this));
      }
    }
    return previous;
  };
}
```

**reduceRight()**:reduceRight()的工作原理和reduce()一样，不同的是它按照数组索引从高到低（从右到左）处理数组，而不是从低到高

### **数组迭代方法**:map(),forEach(),filter(),some(),every()

　ECMAScript5为数组定义了5个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象——影响this的值。传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响访问的返回值

* **map()**:　map()方法对数组的每一项运行给定函数，返回每次函数调用的结果组成的数组

```
[1,2,3].map(function(item,index,arr){return item*item});//[1,4,9]
[1,2,3].map(function(item,index,arr){return item*index});//[0,2,6]
```

map()方法还可以接受第二个参数，表示回调函数执行时this所指向的对象

```
var arr = ['a','b','c'];
[1,2].map(function(item,index,arr){return this[item]},arr);//['b','c']
```

　在实际使用的时候，可以利用map()方法方便地获得对象数组中的特定属性值

```
var users = [{name:'t1',email:'t1@qq.com'},{name:'t2',email:'t2@qq.com'},{name:'t3',email:'t3@qq.com'}];
console.log(users.map(function(item,index,arr){return item.email}));//["t1@qq.com", "t2@qq.com", "t3@qq.com"]
```

map()方法还可以用于类数组对象

```
Array.prototype.map.call('abc',function(item,index,arr){return item.toUpperCase()});//["A", "B", "C"]
```

map()方法兼容写法

```
if (typeof Array.prototype.map != "function") {
  Array.prototype.map = function (fn, context) {
    var arr = [];
    if (typeof fn === "function") {
      for (var k = 0, length = this.length; k < length; k++) {      
         arr.push(fn.call(context, this[k], k, this));
      }
    }
    return arr;
  };
}
```

* **forEach()**:　forEach()方法对数组中的每一项运行给定函数，这个方法没有返回值。本质上与for循环迭代数组一样。如果需要有返回值，一般使用map方法

　forEach()方法除了接受一个必须的回调函数参数，第二个参数还可以接受一个可选的上下文参数(改变回调函数里面的this指向)

```
var out = [];
[1, 2, 3].forEach(function(elem){
  this.push(elem * elem);
}, out);
console.log(out);// [1, 4, 9]
```

第二个参数对于多层this非常有用，因为多层this通常指向是不一致的，可以使用forEach()方法的第二个参数固定this

```
var obj = {
  name: '张三',
  times: [1, 2, 3],
  print: function () {
  //该this指向obj
      console.log(this);
    this.times.forEach(function (n) {
    //该this指向window
      console.log(this);
    });
  }
};
obj.print();
```

```
var obj = {
  name: '张三',
  times: [1, 2, 3],
  print: function () {
  //该this指向obj
      console.log(this);
    this.times.forEach(function (n) {
    //该this同样指向obj
      console.log(this);
    },this);
  }
};
obj.print();
```

　　forEach()循环可以用于类数组对象,与for循环不同，对于稀疏数组，forEach()方法不会在实际上不存在元素的序号上调用函数

　forEach()方法无法在所有元素都传递给调用的函数之前终止遍历。也就是说，没有像for循环中使用的相应的break语句。如果要提前终止，必须把forEach()方法放在一个try块中，并能抛出一个异常

```
var a = [1,2,3,4,5];
a.forEach(function(item,index,arr){
    try{
      if(item == 2) throw new Error;    
    }catch(e){
        console.log(item);
    }
});
```

　forEach()方法兼容写法

```
if(typeof Array.prototype.forEach != 'function'){
    Array.prototype.forEach = function(fn,context){
        for(var k = 0,length = this.length; k < length; k++){
            if(typeof fn === 'function' && Object.prototype.hasOwnProperty.call(this,k)){
                fn.call(context,this[k],k,this);
            }
        }
    }
}
```

* **filter()**:　filter()方法对数组中的每一项运行给定函数，该函数会返回true的项组成的数组。该方法常用于查询符合条件的所有数组项

```
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
});// [4, 5]   
```

filter()方法还可以接受第二个参数，指定测试函数所在的上下文对象(this对象)

```
var Obj = function () {
  this.MAX = 3;
};
var myFilter = function (item) {
  if (item > this.MAX) {
    return true;
  }
};
var arr = [2, 8, 3, 4, 1, 3, 2, 9];
arr.filter(myFilter, new Obj());// [8, 4, 9]
```

filter()会跳过稀疏数组中缺少的元素，它的返回数组总是稠密的，所以可以压缩稀疏数组的空缺,如果要压缩空缺并删除undefined和null元素，可以这样使用filter()方法

　　filter()方法兼容写法

```
if (typeof Array.prototype.filter != "function") {
  Array.prototype.filter = function (fn, context) {
    var arr = [];
    if (typeof fn === "function") {
       for (var k = 0, length = this.length; k < length; k++) {
          fn.call(context, this[k], k, this) && arr.push(this[k]);
       }
    }
    return arr;
  };
}
```

* **some()**:　　some()方法对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true。并且当且仅当数值中的所有元素调用判定函数都返回false，它才返回false

```
a = [1,2,3,4,5];
a.some(function(elem, index, arr){return elem%2===0;})//true
a.some(isNaN);//false
```

在空数组上调用some()方法会返回false

　some()方法兼容写法

```
if (typeof Array.prototype.some != "function") {
  Array.prototype.some = function (fn, context) {
    var passed = false;
    if (typeof fn === "function") {
         for (var k = 0, length = this.length; k < length; k++) {
          if (passed === true) break;
          passed = !!fn.call(context, this[k], k, this);
      }
    }
    return passed;
  };
}
```

* **every()**:　every()方法对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true；只要有一项返回false，则返回false

```
a = [1,2,3,4,5];
a.every(function(elem, index, arr){elem < 10;})//true
a.every(function(elem, index, arr){return elem%2 ===0;});//false
```

在空数组上调用every()方法会返回true

every()方法兼容写法

```
if (typeof Array.prototype.every != "function") {
  Array.prototype.every = function (fn, context) {
    var passed = true;
    if (typeof fn === "function") {
       for (var k = 0, length = this.length; k < length; k++) {
          if (passed === false) break;
          passed = !!fn.call(context, this[k], k, this);
      }
    }
    return passed;
  };
}
```

### **总结**:

javascript数组方法特意定义为通用的，因此它们不仅应用在真正的数组而且在类数组对象上都能正确工作。这22种方法中，除了toString()和toLocaleString()以外的所有方法都是通用的

　　可以改变原数组的方法总共有7种：包括unshift()、shift()、push()、pop()这4种栈和队列方法，reverse()和sort()这2种数组排列方法，数组删改方法splice()

一些常用封装方法:

**数组去重方法封装**:

```
Array.prototype.norepeat = function(){
    var result = [];
    for(var i = 0; i < this.length; i++){
        if(result.indexOf(this[i]) == -1){
            result.push(this[i]);
        }
    }
    return result;
}
var arr = ['a','ab','a'];
console.log(arr.norepeat());//['a','ab']
```

**测试数组是否包含特定值的方法封装**:

```
Array.prototype.inArray = function(value){
    for(var i = 0; i < this.length; i++){
        if(this[i] === value){
            return true;
        }
    }
    return false;
}
var arr = ['a','ab','a'];
console.log(arr.inArray('b'));//false
console.log(arr.inArray('a'));//true
```

