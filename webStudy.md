# HTML/HTTP/浏览器

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

  session:当服务器收到请求需要创建session机制,首先会检查客户端请求中是否包含sessionid,如果有,服务器根据id返回session对象.如果没有,服务器会创建新的session对象.并把sessionis在本次相应中返回给客户端,通常使用cookie方式存储sessionid到客户端，在交互中浏览器按照规则将sessionid发送给服务器。65如果用户禁用cookie，则要使用URL重写，可以通过response.encodeURL(url)4

  75 进行实现；API对encodeURL的结束为，当浏览器支持Cookie时，url不做任何处理；当浏览器不支持Cookie的时候，将会重写URL将SessionID拼接到访问地址后。

* 存储内容:cookie只能存储字符串,session通过类似与Hashtable的数据结构来保存，能支持任何类型的对象(session中可含有多个对象)

* 存储大小:cookie,单个cookie不能超过4kb,session没有大小限制

* 安全性:

  cookie:cookie欺骗,cookie截获,session的安全性更高

  原因:

    (1) sessionID 存储在cookie中,若要攻破session,先要攻破c///ookie

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

## 4,事件冒泡和事件捕获：

* 事件冒泡

1.事件冒泡： 如果一个元素的事件被触发 ，所有父级元素同名事件会被依次触发

​        btn -> div -> body -> html -> document -> window

 2.事件冒泡一直就在我们身边，只是之前 我们没有 为 父元素 添加 同名事件而已！

 3.事件冒泡好处： 如果一个父元素中所有的子元素需要注册同名事件，只需要给父元素注册即可

4.事件对象的一些属性介绍:

   this: 谁调函数，函数中的this就代表谁 --- 事件源：指的 当前执行的事件处理函数 所属的 dom对象

   e.currentTarget ： 和this一模一样，唯一的区别就是有兼容性。 以后用this是最多的

   e.target : 真正的事件触发源 -- 真正触发这个事件的源头（子元素）  -- IE8 : e.srcElement 

 5.事件冒泡的影响： 需求产生冲突

   新增需求：弹出登录框之后，点击页面空白区域隐藏登录框和bg

   问题：点击link无法弹出登录框。  

   原因：

​     a.点击link之后出发它的事件弹出登录框 

​     b.由于事件冒泡影响，会立即出发document的点击事件，登录框一出来就隐藏的

​     解决：e.stopPropagation(); 阻断事件冒泡

* 事件捕获

事件捕获： 如果一个元素的事件被触发，会先触发最顶级的元素的同名事件，

​    然后一级一级往下触发，直到目标元素

​      window->document->html->body->父元素->事件源

  事件捕获事件冒泡完全相反的过程

  如何注册捕获阶段的事件:唯一方式：  addEventListener注册，第三个参数一定要是 true

   IE没有捕获 addEventListener(事件名,事件处理函数，是否捕获阶段)

阻止冒泡也可以阻止捕获

 事件的三个阶段:

​    捕获阶段  目标阶段  冒泡阶段

​    排列显示: 捕获阶段最先显示(从大到小)  目标(被触发事件)  冒泡阶段(从小到大)

## 5,同源策略

A网页设置的 Cookie，B网页不能打开，除非这两个网页"同源"。所谓"同源"指的是"三个相同"。协议,端口,域名相同

同源政策的目的，是为了保证用户信息的安全，防止恶意的网站窃取数据。

如何解决跨域:

1、 通过jsonp跨域

```
//原生
<script>
    var script = document.createElement('script');
    script.type = 'text/javascript';

    // 传参一个回调函数名给后端，方便后端返回时执行这个在前端定义的回调函数
    script.src = 'http://www.domain2.com:8080/login?user=admin&callback=handleCallback';
    document.head.appendChild(script);

    // 回调执行函数
    function handleCallback(res) {
        alert(JSON.stringify(res));
    }
 </script>
 //jquery ajax：
 $.ajax({
    url: 'http://www.domain2.com:8080/login',
    type: 'get',
    dataType: 'jsonp',  // 请求方式为jsonp
    jsonpCallback: "handleCallback",    // 自定义回调函数名
    data: {}
});
//vue.js：
this.$http.jsonp('http://www.domain2.com:8080/login', {
    params: {},
    jsonp: 'handleCallback'
}).then((res) => {
    console.log(res); 
})
//jsonp缺点：只能实现get一种请求。
```

2、 document.domain + iframe跨域

此方案仅限主域相同，子域不同的跨域应用场景。

实现原理：两个页面都通过js强制设置document.domain为基础主域，就实现了同域。

1.）父窗口：(http://www.domain.com/a.html)

```
<iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
<script>
    document.domain = 'domain.com';
    var user = 'admin';
</script>
```

2.）子窗口：(http://child.domain.com/b.html)

```
<script>
    document.domain = 'domain.com';
    // 获取父窗口中变量
    alert('get js data from parent ---> ' + window.parent.user);
</script>
```

3、 location.hash + iframe
4、 window.name + iframe跨域
5、 postMessage跨域
6、 跨域资源共享（CORS）
7、 nginx代理跨域
8、 nodejs中间件代理跨域
9、 WebSocket协议跨域

## 6,HTML的优点和缺点

优点:

* 网络标准统一,由W3C网推荐

* 多设备,跨平台

* 即时更新

* 提高可用性和改进用户的友好体验

* 涉及到网站的抓取和索引的时候,对于SEO很友好

* 可以给站点带来更多的多媒体元素

缺点:

* 安全:同事web Storage,web Socket这样的功能很容易被黑客利用,来盗取用户的信息和资料

* 完善性,许多特性各浏览器的支持成都也不一样

* 性能:某些平台的引擎问题导致html5性能低下

* 浏览器兼容问题:iE9以下浏览器几乎全军覆没

## 7,在地址栏里输入一个URL,到这个页面呈现出来，中间会发生什么？

DNS解析->TCP链接->发送HTTP请求->服务器请求并返回HTTP报文->浏览器解析渲染页面->链接结束

输入url后，首先需要找到这个url域名的服务器ip,为了寻找这个ip，浏览器首先会寻找缓存，查看缓存中是否有记录，缓存的查找记录为：浏览器缓存-》系统缓存-》路由器缓存，缓存中没有则查找系统的hosts文件中是否有记录，如果没有则查询DNS服务器，得到服务器的ip地址后，浏览器根据这个ip以及相应的端口号，构造一个http请求，这个请求报文会包括这次请求的信息，主要是请求方法，请求说明和请求附带的数据，并将这个http请求封装在一个tcp包中，这个tcp包会依次经过传输层，网络层，数据链路层，物理层到达服务器，服务器解析这个请求来作出响应，返回相应的html给浏览器，因为html是一个树形结构，浏览器根据这个html来构建DOM树，在dom树的构建过程中如果遇到JS脚本和外部JS连接，则会停止构建DOM树来执行和下载相应的代码，这会造成阻塞，这就是为什么推荐JS代码应该放在html代码的后面，之后根据外部央视，内部央视，内联样式构建一个CSS对象模型树CSSOM树，构建完成后和DOM树合并为渲染树，这里主要做的是排除非视觉节点，比如script，meta标签和排除display为none的节点，之后进行布局，布局主要是确定各个元素的位置和尺寸，之后是渲染页面，因为html文件中会含有图片，视频，音频等资源，在解析DOM的过程中，遇到这些都会进行并行下载，浏览器对每个域的并行下载数量有一定的限制，一般是4-6个，当然在这些所有的请求中我们还需要关注的就是缓存，缓存一般通过Cache-Control、Last-Modify、Expires等首部字段控制。 Cache-Control和Expires的区别在于Cache-Control使用相对时间，Expires使用的是基于服务器 端的绝对时间，因为存在时差问题，一般采用Cache-Control，在请求这些有设置了缓存的数据时，会先 查看是否过期，如果没有过期则直接使用本地缓存，过期则请求并在服务器校验文件是否修改，如果上一次 响应设置了ETag值会在这次请求的时候作为If-None-Match的值交给服务器校验，如果一致，继续校验 Last-Modified，没有设置ETag则直接验证Last-Modified，再决定是否返回304

## 8,前段性能优化

* 减少http请求次数合并资源，减少HTTP 请求数，minify / gzip 压缩，webP，lazyLoad。

* 加快请求速度：预解析DNS，减少域名数，并行加载，CDN 分发。

* 缓存：HTTP 协议缓存请求，离线缓存 manifest，离线数据缓存localStorage。

* 延迟加载 lazyLoad

  ```
  //引入
  <script type="text/javascript" src="jquery.js"></script>
  <script type="text/javascript" src="jquery.lazyload.js"></script>
  <img class="lazy" alt="" width="640" height="480" data-original="img/example.jpg" />
  
  $(function() {
      $("img.lazy").lazyload({[''
      threshold : 200//设置 threshold 为 200 令图片在距离屏幕 200 像素时提前加载.
      event : "click"//设置,点击时触发
      effect : "fadeIn"//添加页面效果,淡入淡出
  });
  });
  ```

* 渲染：JS/CSS优化，加载顺序，服务端渲染，pipeline。

   预加载:预加载相当于是快用户一步，在空闲的时候就把用户即将用到的资源加载完，等用户实际需要使用时，资源已经存在在本地，自然就跳过了整个加载的等待时间。(与懒加载做对比)

   1. Prefetch:你可以把 Prefetch 理解为资源预获取。一般来说，可以用   Prefetch 来指定在紧接着之后的操作或浏览中需要使用到的资         源，让浏览器提前获取。由于仅仅是提前获取资源，因此浏览器不会对资源进行预处理，并且像 CSS 样式表、JavaScript 脚本这样的资源是不会自动执行并应用于当前文档的。其中 `as` 属性用于指定资源的类型，与 Preload 规范一致，[基本涵盖了所有资源类型](https://www.w3.org/TR/preload/#as-attribute)[2]。

      ```
      <link rel="prefetch" href="/prefetch.js" as="script">
      ```

      

   2. Prerender:Prerender 比 Prefetch 更进一步，可以粗略地理解不仅会预获取，还会预执行。如果你指定 Prerender 一个页面，那么它依赖的其他资源，像 `<script>`、`<link>` 等页面所需资源也可能会被下载与处理。但是预处理会基于当前机器、网络情况的不同而被不同程度地推迟。例如，会根据 CPU、GPU 和内存的使用情况，以及请求操作的幂等性而选择不同的策略或阻止该操作。

      ```
      <link rel="prerender" href="//sample.com/nextpage.html">
      ```

   3. Preload：在遇到需要 Preload 的资源时，浏览器会 **立刻** 进行预获取，并将结果放在内存中，资源的获取不会影响页面 parse 与 load 事件的触发。直到再次遇到该资源的使用标签时，才会执行。由于我们会将 `<script>` 标签置于 `<body>` 底部来保证性能，因此可以考虑在 `<head>` 标签中适当添加这些资源的 Preload 来加速页面的加载与渲染。

   ```
   <link rel="preload" href="./nextpage.js" as="script">
   ```

      


## 9, csrf和xss的网络攻击及防范

CSRF：跨站请求伪造，可以理解为攻击者盗用了用户的身份，以用户的名义发送了恶意请求，比如用户登录了一个网站后，立刻在另一个ｔａｂ页面访问量攻击者用来制造攻击的网站，这个网站要求访问刚刚登陆的网站，并发送了一个恶意请求，这时候CSRF就产生了，比如这个制造攻击的网站使用一张图片，但是这种图片的链接却是可以修改数据库的，这时候攻击者就可以以用户的名义操作这个数据库，防御方式的话：使用验证码，检查https头部的refer，使用token

csrf解决方案:防御CSRF 攻击主要有三种策略：验证 HTTP Referer 字段；在请求地址中添加 token 并验证；在 HTTP 头中自定义属性并验证。

XSS：跨站脚本攻击，是说攻击者通过注入恶意的脚本，在用户浏览网页的时候进行攻击，比如获取cookie，或者其他用户身份信息，可以分为存储型和反射型，存储型是攻击者输入一些数据并且存储到了数据库中，其他浏览者看到的时候进行攻击，反射型的话不存储在数据库中，往往表现为将攻击代码放在url地址的请求参数中，防御的话为cookie设置httpOnly属性，对用户的输入进行检查，进行特殊字符过滤

xss解决方案:

1、将能被转换为html的输入内容，在写代码时改为innerText而不用innerHTML

2、实在没有办法的情况下可用如下方法（js代码）

```
function safeStr(str){
return str.replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g, "&quot;").replace(/'/g, "&#039;");
}
```

## 10,get和post的区别

get参数通过url传递，post放在request body中。

get请求在url中传递的参数是有长度限制的，而post没有。(实际上HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对get请求参数的限制是来源与浏览器或web服务器，浏览器或web服务器限制了url的长度。)

get比post更不安全，因为参数直接暴露在url中，所以不能用来传递敏感信息。

get请求只能进行url编码，而post支持多种编码方式

get请求类似于查找的过程，用户获取数据，可以不用每次都与数据库连接，所以可以使用缓存。post不同，post做的一般是修改和删除的工作，所以必须与数据库交互，所以不能使用缓存。因此get请求适合于请求缓存。

get请求参数会被完整保留在浏览历史记录里，而post中的参数不会被保留。

GET和POST本质上就是TCP链接，并无差别。但是由于HTTP的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。

GET产生一个TCP数据包；POST产生两个TCP数据包:对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数

据）。

## 11,缓存

ajax解决缓存:

在ajax发送请求前加上 anyAjaxObj.setRequestHeader("If-Modified-Since","0")。

在ajax发送请求前加上 anyAjaxObj.setRequestHeader("Cache-Control","no-cache")。

在URL后面加上一个随机数： "fresh=" + Math.random()。

在URL后面加上时间搓："nowtime=" + new Date().getTime()。

如果是使用jQuery，直接这样就可以了 $.ajaxSetup({cache:false})。这样页面的所有ajax都会执行这条语句就是不需要保存缓存记录。

## 12,http版本

## 1、HTTP 0.9



HTTP 0.9是第一个版本的HTTP协议，已过时。它的组成极其简单，只允许客户端发送GET这一种请求，且不支持请求头。由于没有协议头，造成了HTTP 0.9协议只支持一种内容，即纯文本。不过网页仍然支持用HTML语言格式化，同时无法插入图片。



HTTP 0.9具有典型的无状态性，每个事务独立进行处理，事务结束时就释放这个连接。由此可见，HTTP协议的无状态特点在其第一个版本0.9中已经成型。一次HTTP 0.9的传输首先要建立一个由客户端到Web服务器的TCP连接，由客户端发起一个请求，然后由Web服务器返回页面内容，然后连接会关闭。如果请求的页面不存在，也不会返回任何错误码。



## 2、HTTP 1.0



HTTP协议的第二个版本，第一个在通讯中指定版本号的HTTP协议版本，至今仍被广泛采用。相对于HTTP 0.9 增加了如下主要特性：

- 请求与响应支持头域
- 响应对象以一个响应状态行开始
- 响应对象不只限于超文本
- 开始支持客户端通过POST方法向Web服务器提交数据，支持GET、HEAD、POST方法
- （短连接）每一个请求建立一个TCP连接，请求完成后立马断开连接。这将会导致2个问题：连接无法复用，head of line blocking。连接无法复用会导致每次请求都经历三次握手和慢启动。三次握手在高延迟的场景下影响较明显，慢启动则对文件类请求影响较大。head of line blocking会导致带宽无法被充分利用，以及后续健康请求被阻塞。



## 3、HTTP 1.1



HTTP协议的第三个版本是HTTP 1.1，是目前使用最广泛的协议版本 。HTTP 1.1是目前主流的HTTP协议版本，因此这里就多花一些笔墨介绍一下HTTP 1.1的特性。



HTTP 1.1引入了许多关键性能优化：keepalive连接，chunked编码传输，字节范围请求，请求流水线等



- Persistent Connection（keepalive连接）：允许HTTP设备在事务处理结束之后将TCP连接保持在打开的状态，以便未来的HTTP请求重用现在的连接，直到客户端或服务器端决定将其关闭为止。在HTTP1.0中使用长连接需要添加请求头 Connection: Keep-Alive，而在HTTP 1.1 所有的连接默认都是长连接，除非特殊声明不支持（ HTTP请求报文首部加上Connection: close ）。服务器端按照FIFO原则来处理不同的Request。



![img](https://pic3.zhimg.com/80/v2-0b7ec9d73c1f90ccae4f566baf4f2c7a_720w.jpg)





- chunked编码传输：该编码将实体分块传送并逐块标明长度，直到长度为0块表示传输结束，这在实体长度未知时特别有用(比如由数据库动态产生的数据)
- 字节范围请求：HTTP1.1支持传送内容的一部分。比方说，当客户端已经有内容的一部分，为了节省带宽，可以只向服务器请求一部分。该功能通过在请求消息中引入了range头域来实现，它允许只请求资源的某个部分。在响应消息中Content-Range头域声明了返回的这部分对象的偏移值和长度。如果服务器相应地返回了对象所请求范围的内容，则响应码206（Partial Content）
- Pipelining（请求流水线）



另外，HTTP 1.1还新增了如下特性：

- 请求消息和响应消息都支持Host头域：在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。因此，Host头的引入就很有必要了。

- 新增了一批Request method：HTTP1.1增加了OPTIONS,PUT, DELETE, TRACE, CONNECT方法

- 缓存处理：HTTP/1.1在1.0的基础上加入了一些cache的新特性，引入了实体标签，一般被称为e-tags，新增更为强大的Cache-Control头。

4、HTTP 2.0

  

  HTTP 2.0是下一代HTTP协议，目前应用还非常少。主要特点有：

  - 多路复用（二进制分帧）。HTTP 2.0最大的特点：不会改动HTTP 的语义，HTTP 方法、状态码、URI 及首部字段，等等这些核心概念上一如往常，却能致力于突破上一代标准的性能限制，改进传输性能，实现低延迟和高吞吐量。而之所以叫2.0，是在于新增的二进制分帧层。在二进制分帧层上， HTTP 2.0 会将所有传输的信息分割为更小的消息和帧，并对它们采用二进制格式的编码 ，其中HTTP1.x的首部信息会被封装到Headers帧，而我们的request body则封装到Data帧里面。

  

  ![img](https://pic4.zhimg.com/80/v2-d75bfb854399171eab9a056f93dd4953_720w.jpg)

  

  - HTTP 2.0 通信都在一个连接上完成，这个连接可以承载任意数量的双向数据流。相应地，每个数据流以消息的形式发送，而消息由一或多个帧组成，这些帧可以乱序发送，然后再根据每个帧首部的流标识符重新组装。
  - 头部压缩：当一个客户端向相同服务器请求许多资源时，像来自同一个网页的图像，将会有大量的请求看上去几乎同样的，这就需要压缩技术对付这种几乎相同的信息。
  - 随时复位：HTTP1.1一个缺点是当HTTP信息有一定长度大小数据传输时，你不能方便地随时停止它，中断TCP连接的代价是昂贵的。使用HTTP2的RST_STREAM将能方便停止一个信息传输，启动新的信息，在不中断连接的情况下提高带宽利用效率。
  - 服务器端推流：Server Push。客户端请求一个资源X，服务器端判断也许客户端还需要资源Z，在无需事先询问客户端情况下将资源Z推送到客户端，客户端接受到后，可以缓存起来以备后用。
  - 优先权和依赖：每个流都有自己的优先级别，会表明哪个流是最重要的，客户端会指定哪个流是最重要的，有一些依赖参数，这样一个流可以依赖另外一个流。优先级别可以在运行时动态改变，当用户滚动页面时，可以告诉浏览器哪个图像是最重要的，你也可以在一组流中进行优先筛选，能够突然抓住重点流。

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

.list>li:nth-child(n)  选中第n个子元素

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

![](D:\workSpace\noteBook\images\css01.png)

### 1.6 css3帧动画

![](D:\workSpace\noteBook\images\css02.png)

### 1.7 渐变（Gradients）

- **线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向**

  background-image: linear-gradient(direction, color-stop1, color-stop2, ...);

- **径向渐变（Radial Gradients）- 由它们的中心定义**

- background: radial-gradient(center, shape size, start-color, ..., last-color);

### 1.8 css3多列

column-count 属性指定了需要分割的列数

![](D:\workSpace\noteBook\images\css03.png)

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

## 6,清除浮动:

方法一：使用带clear属性的空元素

在浮动元素后使用一个空元素如<div class="clear"></div>，并在CSS中赋予.clear{clear:both;}属性即可清理浮动。亦可使用<br class="clear" />或<hr class="clear" />来进行清理。

方法二：使用CSS的overflow属性

给浮动元素的容器添加overflow:hidden;或overflow:auto;可以清除浮动，另外在 IE6 中还需要触发 hasLayout ，例如为父元素设置容器宽高或设置 zoom:1。

在添加overflow属性后，浮动元素又回到了容器层，把容器高度撑起，达到了清理浮动的效果。

方法三：给浮动的元素的容器添加浮动

给浮动元素的容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影响布局，不推荐使用。

方法四：使用邻接元素处理

什么都不做，给浮动元素后面的元素添加clear属性。

方法五：使用CSS的:after伪元素

结合:after 伪元素（注意这不是伪类，而是伪元素，代表一个元素之后最近的元素）和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。

给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。

## 7,为什么CSS放头部，JS放底部

CSS放头部，JS放底部，这样可以提高页面的性能。然而，为什么呢？原因如下：

CSS 不会阻塞 DOM 的解析，但会阻塞 DOM 渲染。
JS 阻塞 DOM 解析，但浏览器会"偷看"DOM，预先下载相关资源。
浏览器遇到 <script>且没有defer或async属性的 标签时，会触发页面渲染，因而如果前面CSS资源尚未加载完毕时，浏览器会等待它加载完毕在执行脚本。
这就是为何<script>最好放底部，<link>最好放头部，如果头部同时有<script>与<link>的情况下，最好将<script>放在<link>上面了吗？

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

## 3,对象常用方法

* charAt  :(1) 返回对应下标的字符
* ndexOf  返回对应字符的下标,如果找不到字符,就返回-1;如果有多个相同的目标字符,返回第一个匹配字符的下标
* lastIndexOf  返回对应的最后一个字符的下标
* concat 连接字符串
* replace()  替换指定的字符串
* Split()  将字符串按照分隔符拆成若干个元素,存入数组,并返回[数组]
* substr(index,count)  从指定下标复制取出count字符,并返回
* substring(beginIndex,endIndex)  截取范围:beginIndex  <=x  <endIndex
* toUpperCase() 将字符串中所有英文字母转成大写
* toLowerCase() 将字符串所有英文字母都转成小写

## 4,事件绑定和普通事件有什么区别

普通添加事件:

```
var btn = document.getElementById("hello");
btn.onclick = function(){
	alert(1);
}
btn.onclick = function(){
	alert(2);
}
//代码只会执行alert(2)
```

事件绑定:

```
var btn = document.getElementById("hello");
btn.addEventListener("click",function(){
	alert(1);
},false);
btn.addEventListener("click",function(){
	alert(2);
},false);
//结果:alert(1)之后,再alert(2)
```

普通添加事件的方法不支持添加多个事件，最下面的事件会覆盖上面的，而事件绑定（addEventListener）方式添加事件可以添加多个。

addEventListener不兼容低版本IE

普通事件无法取消

addEventLisntener还支持事件冒泡+事件捕获

## 5,构造函数new的执行原理

分为四个步骤:

A 创建空对象{}      

B  this指向这个对象:this={}

C 执行构造函数赋值代码  

D  自动返回这个对象

this的指向:谁调用我,我就指向谁; 全局函数:指向window;对象的方法:指向对象; 构造函数:指向new创建的空对象;this指向取决与函数是如何调用的,跟函数的声明是没有任何关系的

**如何修改this的指向**(上下文模式):

* call()  [语法]  函数名.call(要修改的this,arg1,arg2...)

* apply()  [语法]  函数名.apply(要修改的this,参数数组/伪数组)

  适用场景:函数原本有多个形参.

* bind()  [语法]  函数名.call(要修改的this,arg1,arg2...)

  特点:不会立即执行这个函数,而是返回一个修改this之后的新函数.适用场景:定时器,事件处理函数.

注意点:修改的this一定是引用类型(数组,函数,对象)

(1)指向基本数据类型 string boolean number(包装类型)

会自动帮我们转成对应的包装类型

New String()  new Boolean()  new Number()

(2) undefined null

修改无效,还是默认的window

**将伪数组转成数组**:

1)固定语法:数组.push.apply(数组,伪数组)

```
var weiArr = {
0:'alice',
1:'judy',
2:'linda',
3:'lisa',
length:4,
}
var arr1=[];
arr1.push.apply(arr1,weiArr);
console.log(arr1);
```

2)slice和call

数组.slice(start,end)  返回 start <= 范围 <end

如果传参0或者不传,返回数组自身

思路:如果伪数组也可以调用slice,不传参数.不久返回真数组了吗?

```
var arr = Array.prototype.slice.call(weiArr);//伪数组的原型没有slice方法.所以不能直接weiArr.slice()
console.log(arr);
```

详细过程:

![](D:\workSpace\noteBook\images\js03.png)

## 6,原型及原型链

原型出现的前提:发现构造函数的弊端:浪费内存资源;使用函数解决内存资源浪费  造成全局变量污染;引入对象:同时解决内存资源浪费 与 全局变量污染.

原型的三个属性:

* **prototype(原型)**:每一个函数在被创建的时候,系统会自动帮我们创建一个与之对应的对象,这个对象称之为原型.

   作用:同时解决内存资源浪费 与 全局变量污染

   如何获取原型对象:语法 构造函数.protoype

   谁可以访问原型总的数据

​      A,函数自身

​      B,这个构造函数 实例化(创建) 的每一个对象

* **\__proto__**:属于实例化对象,指向自身原型对象

​       作用 :可以让实例化对象访问原型中的成员(属性+方法). 

​       注意:开发中千万不要使用,因为不是W3C标准属性.

* **constructor**:属于原型对象,指向的是构造函数

​     作用 : 可以让实例化对象知道自己被哪个构造函数创建

​     注意点 :  原型重新赋值会丢失

**原型链**:

每一个对象都有\__proto__指向自身的原型,而原型也是对象,也有自己的原型,以此类推,形成一种链式结构,称之为原型链.

对象访问原型链成员规则:就近原则:

当对象访问原型的成员,先看看自己有没有,如果过有则访问(取值+赋值),没有找原型,如果过原型则访问原型,如果过原型没有则访问原型的原型,以此类推一直到原型链最顶端.如果过还没有.属性则返回undefined,方法则报错:XXX is not  a  function.

原型与构造函数关系:

* 只要是构造函数就有`prototype`属性指向自身的原型对象

* 只要是原型对象就有`constructor`属性指向对应的构造函数

* 只要是对象就有`_proto_`属性指向与之相应的构造函数的原型对象,特殊情况:Object.prototype的原型对象是null

* 函数本身也是对象

DOM原型链:

![](D:\workSpace\noteBook\images\js01.png)

**完整原型链**:

作用:了解 构造函数,原型对象,实例化对象三者的关系.

关系:js中所有的对象都是构造函数创建,不同的对象是不同的构造函数.

总结:不同的对象是不同的构造函数创建:

 1,函数对象是Function构造函数创建

 2,原型对象是Object构造函数创建

 3,实例对象是对应的构造函数创建.

![](D:\workSpace\noteBook\images\js02.png)

原型链中所有的对象最终的原型都会指向object的原型,这就意味着,所有的对象都能访问 Object.prototype

**Object.prototype**：

* hasOwnProperty:对象是否有某个成员

   [语法]  对象名.hasOwnProperty(‘属性名’)  true:有  false:没有

   作用:检查一个成员 是自己的 还是原型的

*  isPrototypeOf :检测一个对象是不是另一个对象的原型

   [语法]  A对象.isPrototypeOf(B对象)  A是不是B的原型  (A==B.__proto__)

* propertyIsEnumerable():检测对象的成员是否可以被枚举

     枚举必须满足两个条件:(1) 是自己的成员 (2) 可以被for-in遍历

     数组的length:无法被for-in循环遍历

**函数对象常用属性**：

* caller:获取调用这个函数的引用 (谁调用了我)

​      a. 如果在函数B中调用函数A，则函数A的caller就是函数B

​      b. 如果在全局window中调用函数，函数的caller就是null

* length:获取函数形参的数量

*  name:获取函数名

* arguments:获取所有的实参(伪数组->对象):

  arguments--两个属性:

     callee:返回函数自身

     位移的场景:匿名函数递归调用

     length:实参的数量

*请说出 call caller callee的区别*:

*call : 属于Function.prototype, 动态修改函数中的this指向*

*caller : 属于函数对象 ， 获取调用函数的引用*

*callee : 属于arguments，获取函数自身（匿名函数递归调用）*

## 7,**instanceof关键字**

Instanceof运算符:对象 instanceof 构造函数

作用:检测右边构造函数的原型在不在左边对象的原型链中.

```
  var arr = [10,20,30];
/* 
1.数组的原型链 
arr -> Array.prototype -> Object.prototype -> null
*/
console.log(arr instanceof Array);// true
console.log(arr instanceof Object);// true
2.Function函数对象的原型链
根据instanceof运算规则 ： 左边Function 对象 右边Function是构造函数
Function函数对象 -> Function.prototype -> Object.prototype ->null
*/
console.log(Function instanceof Function);// true
console.log(Function instanceof Object);// true
/* 
3. Object构造函数的原型链
根据instanceof运算规则 ： 左边Object函数对象 右边Object构造函数
Object函数对象 ——》 Function.prototype-> Object.prototype -> null
*/
console.log(Object instanceof Object);// true
console.log(Object instanceof Function);// true
```

## 8, 斐波纳契数列

## 9,闭包

闭包就是能够读取其他函数内部变量的函数，或者子函数在外调用，子函数所在的父函数的作用域不会被释放。jquery就是$的闭包

## 10,继承

```
下面来创建一个Animal类：
// 定义一个动物类
function Animal (name) {
// 属性
this.name = name || 'Animal';
// 实例方法
this.sleep = function(){
console.log(this.name + '正在睡觉！');
}
}
// 原型方法
Animal.prototype.eat = function(food) {
console.log(this.name + '正在吃：' + food);
};
```

* 原型链继承：	

```
function Cat(){ }
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';
//　Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.eat('fish'));
console.log(cat.sleep());
console.log(cat instanceof Animal); //true
console.log(cat instanceof Cat); //true
```

在这里我们可以看到new了一个空对象,这个空对象指向Animal并且Cat.prototype指向了这个空对象，这种就是基于原型链的继承。

特点：基于原型链，既是父类的实例，也是子类的实例

缺点：无法实现多继承

* 构造继承：使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）

```
function Cat(name){
Animal.call(this);
this.name = name || 'Tom';
}
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

* 实例继承和拷贝继承

实例继承：为父类实例添加新特性，作为子类实例返回

拷贝继承：拷贝父类元素上的属性和方法

上述两个实用性不强，不一一举例。

* 组合继承：相当于构造继承和原型链继承的组合体。通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

```
function Cat(name){
Animal.call(this);
this.name = name || 'Tom';
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // true
```

特点：可以继承实例属性/方法，也可以继承原型属性/方法

缺点：调用了两次父类构造函数，生成了两份实例

* 寄生组合继承：通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化两次实例方法/属性

```
//创建一个没有实例方法的类
var Super = function(){};
Super.prototype = Animal.prototype;
```

将实例作为子类的原型

```
Cat.prototype = new Super();
})();
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); //true
```

## 11,异步回调地狱

在使用JavaScript时，为了实现某些逻辑经常会写出层层嵌套的回调函数，如果嵌套过多，会极大影响代码可读性和逻辑，这种情况也被成为回调地狱

解决方案:Promise 对象、Generator 函数、async 函数

1,:Promise 对象:Promise 是一个对象，从其中可以获取异步操作的消息，可以说它更像是一个容器，保存着将来才会结束的事件（也就是一个异步操作）。

Promise 对象代理的值其实是未知的，状态是动态可变的，因此 Promise 对象的状态有三种：进行中、结束、失败，它运行的时候，只能从进行中到失败，或者是从进行中到成功。使用 Promise 对象只要是通过同步的表达形式来运行异步代码。

1. pending：初始状态，既不成功，也不失败；
2. fulfilled：操作成功结束；
3. rejected：操作失败。

```
function f1() {
   return new Promise((resolve, reject) => {
      setTimeout(() => resolve(11), 1000);
   }).then(data => console.log(data));
}
function f2() {
   return new Promise((resolve, reject) => {
      setTimeout(() => resolve(22), 2000);
   }).then(data => console.log(data));;
}
function f3() {
   return new Promise((resolve, reject) => {
      setTimeout(() => resolve(33), 3000);
   }).then(data => console.log(data));;
}
f1().then(f2).then(f3)
```

* #### Async/Await

  **async** 必须声明的是一个 **function** 函数，**await** 就必须是在 **async** 声明的函数内部使用，这是一个固定搭配，

```
let data = 'data'
a = async function () {
  const b = function () {
     await data
  }
}
```

调用 promise1，使用 promise1 返回的结果再去调用 promise2，然后使用两者的结果去调用 promise3。在没有使用 Async/Await 之前的写法，应该是这样的：

```
const request = () => {
  return promise1()
    .then(value1 => {
      return promise2(value1)
        .then(value2 => {        
          return promise3(value1, value2)
        })
    })
}
```

使用了 Async/Await 的写法之后，是这样的：

```
const request = async () => {
  const value1 = await promise1()
  const value2 = await promise2(value1)
  return promise3(value1, value2)
}
```

* ## Generator 函数

  ```
  // 用 co 模块自动执行
  var co = require('co');
  var sayhello = function (name, ms) {
    setTimeout(function (name,ms) {
      console.log(name);
    }, ms);
  }
  var gen = function* () {
    yield sayhello("xiaomi", 2000);
    console.log('frist');
    yield sayhello("huawei", 1000);
    console.log('second');
    yield sayhello("apple", 500);
    console.log('end');
  }
  co(gen());
  ```

  ## 12,JS的防抖和节流

  scroll 事件本身会触发页面的重新渲染，同时 scroll 事件的 handler 又会被高频度的触发, 因此事件的 handler 内部不应该有复杂操作，例如 DOM 操作就不应该放在事件处理中。

  针对此类高频度触发事件问题（例如页面 scroll ，屏幕 resize，监听用户输入等），下面介绍两种常用的解决方法，防抖和节流。

* 防抖:

  防抖技术即是可以把多个顺序地调用合并成一次，也就是在一定时间内，规定事件被触发的次数。

  ```
  // 简单的防抖动函数
  function debounce(func, wait, immediate) {
      // 定时器变量
      var timeout;
      return function() {
          // 每次触发 scroll handler 时先清除定时器
          clearTimeout(timeout);
          // 指定 xx ms 后触发真正想进行的操作 handler
          timeout = setTimeout(func, wait);
      };
  };
   
  // 实际想绑定在 scroll 事件上的 handler
  function realFunc(){
      console.log("Success");
  }
   
  // 采用了防抖动
  window.addEventListener('scroll',debounce(realFunc,500));
  // 没采用防抖动
  window.addEventListener('scroll',realFunc);
  ```

* 节流:

  防抖函数确实不错，但是也存在问题，譬如图片的懒加载，我希望在下滑过程中图片不断的被加载出来，而不是只有当我停止下滑时候，图片才被加载出来。又或者下滑时候的数据的 ajax 请求加载也是同理。

  这个时候，我们希望即使页面在不断被滚动，但是滚动 handler 也可以以一定的频率被触发（譬如 250ms 触发一次），这类场景，就要用到另一种技巧，称为节流函数（throttling）。

## 12,浅拷贝和深拷贝

- 浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以**如果其中一个对象改变了这个地址，就会影响到另一个对象**。

- 深拷贝是将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且**修改新对象不会影响原对象**。

 赋值和深/浅拷贝的区别:都是**针对引用类型**：

当我们把一个对象赋值给一个新的变量时，**赋的其实是该对象的在栈中的地址，而不是堆中的数据**。也就是两个对象指向的是同一个存储空间，无论哪个对象发生改变，其实都是改变的存储空间的内容，因此，两个对象是联动的。

浅拷贝：重新在堆中创建内存，拷贝前后对象的基本数据类型互不影响，但拷贝前后对象的引用类型因共享同一块内存，会相互影响。

深拷贝：从堆内存中开辟一个新的区域存放新对象，对对象中的子对象进行递归拷贝,拷贝前后的两个对象互不影响。

浅拷贝的实现方式:

1,.Object.assign()

```
let obj1 = { person: {name: "kobe", age: 41},sports:'basketball' };
let obj2 = Object.assign({}, obj1);
obj2.person.name = "wade";
obj2.sports = 'football'
console.log(obj1); // { person: { name: 'wade', age: 41 }, sports: 'basketball' }
```

2,函数库lodash的_.clone方法

```
var _ = require('lodash');
var obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
var obj2 = _.clone(obj1);
console.log(obj1.b.f === obj2.b.f);// true
```

3,...展开运算符

```
let obj1 = { name: 'Kobe', address:{x:100,y:100}}
let obj2= {... obj1}
obj1.address.x = 200;
obj1.name = 'wade'
console.log('obj2',obj2) // obj2 { name: 'Kobe', address: { x: 200, y: 100 } }
```

深拷贝:

1.JSON.parse(JSON.stringify())

```
let arr = [1, 3, {
    username: ' kobe'
}];
let arr4 = JSON.parse(JSON.stringify(arr));
arr4[2].username = 'duncan'; 
console.log(arr, arr4)
```

2.函数库lodash的_.cloneDeep方法

```
var _ = require('lodash');
var obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
var obj2 = _.cloneDeep(obj1);
console.log(obj1.b.f === obj2.b.f);// false
```

3.jQuery.extend()方法

```
$.extend(deepCopy, target, object1, [objectN])//第一个参数为true,就是深拷贝
```

4,递归

```
function deepClone(obj){
var newObj= obj instanceof Array ? []:{};
for(var item in obj){
var temple= typeof obj[item] == 'object' ? deepClone(obj[item]):obj[item];
newObj[item] = temple;
}
return newObj;
}
```

## 13,es6新特性

## 14,webPack

webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个bundle。

# angular JS框架

## 1,AngularJS双向绑定原理

采用了脏检查机制。

双向数据绑定是 AngularJS 的核心机制之一。当 view 中有任何一个数据变化时，都会更新到 model 中。如果 model 中的数据有变化时，view 也会同步更新，显然，这需要一个监控。

原理

Angular 在 scope 模型上设置了一个监听队列，这个监听队列可以用来监听数据变化并更新 view 。每次绑定一个东西到 view 上时， AngularJS 就会往 $watch 队列里插入一条 $watch ，用来检测它监视的 model 里是否有变化的东西。当浏览器接收到可以被 angular context 处理的事件时， $digest 循环就会触发，遍历所有的 $watch ，最后更新 dom。



## 2,生命周期

**ngOnChanges** 
 设置或重新设置数据绑定的输入属性时响应。 该方法接受当前和上一属性值的 SimpleChanges 对象 注意，这发生的非常频繁，所以你在这里执行的任何操作都会显著影响性能

**ngOnInit** 
 第一次显示数据绑定和设置指令/组件的输入属性之后，初始化指令/组件

**ngDoCheck** 
 检测，并在发生 Angular 无法或不愿意自己检测的变化时作出反应

**ngAfterContentInit** 
 外部内容投影进组件视图或指令所在的视图之后调用

**ngAfterContentChecked** 
 检查完被投影到组件或指令中的内容之后调用

**ngAfterViewInit** 
 初始化完组件视图及其子视图或包含该指令的视图之后调用

**ngAfterViewChecked** 
 做完组件视图和子视图或包含该指令的视图的变更检测之后调用

**ngOnDestroy** 
 每当 Angular 每次销毁指令/组件之前调用并清扫。 在这儿反订阅可观察对象和分离事件处理器，以防内存泄漏

## 3, 两个平级界面块 a 和 b，如果 a 中触发一个事件，有哪些方式能让 b 知道？详述原理

共用服务

在 Angular 中，通过 factory 可以生成一个单例对象，在需要通信的模块 a 和 b 中注入这个对象即可。

基于事件

这个又分两种方式

第一种是借助父 controller。在子 controller 中向父 controller 触发（`$emit`）一个事件，然后在父 controller 中监听（`$on`）事件，再广播（`$broadcast`）给子 controller ，这样通过事件携带的参数，实现了数据经过父 controller，在同级 controller 之间传播。

第二种是借助 `$rootScope`。每个 Angular 应用默认有一个根作用域 `$rootScope`， 根作用域位于最顶层，从它往下挂着各级作用域。所以，如果子控制器直接使用 `$rootScope` 广播和接收事件，那么就可实现同级之间的通信

## 4,angular 的缺点

##### 强约束

导致学习成本较高，对前端不友好。

但遵守 AngularJS 的约定时，生产力会很高，对 Java 程序员友好。

##### 不利于 SEO

因为所有内容都是动态获取并渲染生成的，搜索引擎没法爬取。

一种解决办法是，对于正常用户的访问，服务器响应 AngularJS 应用的内容；对于搜索引擎的访问，则响应专门针对 SEO 的HTML页面。

##### 性能问题

作为 MVVM 框架，因为实现了数据的双向绑定，对于大数组、复杂对象会存在性能问题。

可以用来 [优化 Angular 应用的性能](https://github.com/xufei/blog/issues/23) 的办法：

1. 减少监控项（比如对不会变化的数据采用单向绑定）
2. 主动设置索引（指定 `track by`，简单类型默认用自身当索引，对象默认使用 `$$hashKey`，比如改为 `track by item.id`）
3. 降低渲染数据量（比如分页，或者每次取一小部分数据，根据需要再取）
4. 数据扁平化（比如对于树状结构，使用扁平化结构，构建一个 map 和树状数据，对树操作时，由于跟扁平数据同一引用，树状数据变更会同步到原始的扁平数据）

另外，对于Angular1.x ，存在 脏检查 和 模块机制 的问题。

## 5,详述 angular 的 “依赖注入”

依赖注入是一种软件设计模式，目的是处理代码之间的依赖关系，减少组件间的耦合。

在 Angular App 运行的时候，调用 myCtrl，自动做了 `$scope` 和 `$http` 两个依赖性的注入

原理:AngularJS 是通过构造函数的参数名字来推断依赖服务名称的，通过 `toString()` 来找到这个定义的 function 对应的字符串，然后用正则解析出其中的参数（依赖项），再去依赖映射中取到对应的依赖，实例化之后传入。

## 6,.解释下什么是`$rootScrope`以及和`$scope`的区别？

通俗的说`$rootScrope` 页面所有`$scope`的`父亲`。

step1:Angular解析ng-app然后在内存中创建$rootScope。

step2:angular回继续解析，找到{{}}表达式，并解析成变量。

step3:接着会解析带有ng-controller的div然后指向到某个controller函数。这个时候在这个controller函数变成一个$scope对象实例。

## 7, Angular中的digest周期是什么？

每个digest周期中，angular总会对比scope上model的值，一般digest周期都是自动触发的

## 8, 如何取消 `$timeout`, 以及停止一个`$watch()`?

停止 $timeout我们可以用cancel：

```
var customTimeout = $timeout(function () {  
  // your code
}, 1000);
 
$timeout.cancel(customTimeout);
```

停掉一个`$watch`：

```

// .$watch() 会返回一个停止注册的函数
function that we store to a variable  
var deregisterWatchFn = $rootScope.$watch(‘someGloballyAvailableProperty’, function (newVal) {  
  if (newVal) {
    // we invoke that deregistration function, to disable the watch
    deregisterWatchFn();
    ...
  }
});
```

## 9,ng-if跟ng-show/hide的区别有哪些？

1、ng-if 在后面表达式为 true 的时候才创建dom 节点，而ng-show 是在初始时就创建了，可以用 display:block 和 display:none 来控制显示和不显示。

2、ng-if 会（隐式地）产生新作用域，ng-switch 、ng-include 等会动态创建一块界面的也是如此。

这样会导致，在 ng-if 中用基本变量绑定 ng-model，同事在外层的 div 中将 model 绑定给另一个显示区域后，在内层改变时，外层并不会随着内层改变，因为这已经两个不同的变量了。

而在 ng-show 中，却不存在此问题，因为它不自带一级作用域。

为了避免这类问题的出现，我们可以始终将页面中的元素绑定到对象的属性（data.x），而不是直接绑定到基本变量（x）上。

## 10,ng-click 中写的表达式，能使用 JS 原生对象上的方法吗？

不止是 ng-click 中，只要是在页面中，都是无法直接调用原生的 JS 方法的，因为这些并不存在于与页面对应的 Controller 的 $scope 中。

但是可以通过filter

```
<p>{{13.14 | parseIntFilter}}</p>

app.filter('parseIntFilter', function(){
    return function(item){
        return parseInt(item);
    }
})
```

有一席内置的api可以直接用

ng 内置的filter主要有九种：

1：date（日期）

2：currency（货币）

3：limitTo（限制数组或字符串长度）

4：orderBy（排序）

5：lowercase（小写）

6：uppercase（大写）

7：number（格式化数字，加上千位分隔符，并接收参数限定小数点位数）

8：filter（处理一个数组，过滤出含有某个子串的元素）

9：json（格式化 json 对象）

## 11,factory、service 和 provider 是什么关系？

factory

把 service 的方法和数据放在一个对象里，并返回这个对象。

```
app.factory('FooService', function(){
  return {
    target: 'factory',
    sayHello: function(){
      return 'hello ' + this.target;
    }
  }
});
```

service

通过构造函数的方式创建 service，然后返回一个实例化对象。

```
app.service('FooService', function(){
  var self = this;
  this.target = 'service';
  this.sayHello = function(){
    return 'hello ' + self.target;
  }
});
```

provider

创建一个可通过 config 配置的 service，$get 中返回的，就是用 factory 创建 service 的内容。

```
app.provider('FooService', function(){
  this.configData = 'init data';
  this.setConfigData = function(data){
    if(data){
      this.configData = data;
    }
  }
  this.$get = function(){
    var self = this;
    return {
      target: 'provider',
      sayHello: function(){
        return self.configData + ' hello ' + this.target;
      }
    }
  }
});
 
// 此处注入的是 FooService 的 provider
app.config(function(FooServiceProvider){
  FooServiceProvider.setConfigData('config data');
});
```

从底层实现上来看，三者的关系是：service 调用了 factory，返回其实例；factory 调用了 provider，返回其 $get 中定义的内容。factory 和 service 的功能类似，但是 factory 是普通 function，可以返回任何东西；service 是构造器，可以不返回（绑定到 this 的都可以被访问）；provider 是加强版 factory，返回一个可配置的 factory。

# Vue 框架

## 1,vue的生命周期

Vue实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模板、挂载Dom、渲染→更新→渲染、销毁等一系列过程，我们称这是Vue的生命周期。通俗说就是Vue实例从创建到销毁的过程，就是生命周期。

每一个组件或者实例都会经历一个完整的生命周期，总共分为三个阶段：初始化、运行中、销毁。

实例、组件通过new Vue() 创建出来之后会初始化事件和生命周期，然后就会执行beforeCreate钩子函数，这个时候，数据还没有挂载呢，只是一个空壳，无法访问到数据和真实的dom，一般不做操作

挂载数据，绑定事件等等，然后执行created函数，这个时候已经可以使用到数据，也可以更改数据,在这里更改数据不会触发updated函数，在这里可以在渲染前倒数第二次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取

接下来开始找实例或者组件对应的模板，编译模板为虚拟dom放入到render函数中准备渲染，然后执行beforeMount钩子函数，在这个函数中虚拟dom已经创建完成，马上就要渲染,在这里也可以更改数据，不会触发updated，在这里可以在渲染前最后一次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取

接下来开始render，渲染出真实dom，然后执行mounted钩子函数，此时，组件已经出现在页面中，数据、真实dom都已经处理好了,事件都已经挂载好了，可以在这里操作真实dom等事情...

当组件或实例的数据更改之后，会立即执行beforeUpdate，然后vue的虚拟dom机制会重新构建虚拟dom与上一次的虚拟dom树利用diff算法进行对比之后重新渲染，一般不做什么事儿

当更新完成后，执行updated，数据已经更改完成，dom也重新render完成，可以操作更新后的虚拟dom

当经过某种途径调用$destroy方法后，立即执行beforeDestroy，一般在这里做一些善后工作，例如清除计时器、清除非指令绑定的事件等等

组件的数据绑定、监听...去掉后只剩下dom空壳，这个时候，执行destroyed，在这里做善后工作也可以

![](D:\workSpace\noteBook\images\vue01.png)

## 2,Vue数据双向绑定原理

Vue实现数据双向绑定主要利用的就是: **数据劫持**和**发布订阅模式**。
所谓发布订阅模式就是，定义了对象间的一种**一对多的关系**，**让多个观察者对象同时监听某一个主题对象，当一个对象发生改变时，所有依赖于它的对象都将得到通知**。
所谓数据劫持，就是**利用JavaScript的访问器属性**，即**Object.defineProperty()方法**，当对对象的属性进行赋值时，Object.defineProperty就可以**通过set方法劫持到数据的变化**，然后**通知发布者(主题对象)去通知所有观察者**，观察者收到通知后，就会对视图进行更新。

1. 实现一个监听器 Observer，用来劫持并监听所有属性，如果发生变动，则通知订阅者。
2. 实现一个订阅者 Watcher，当接到属性变化的通知时，执行对应的函数，然后更新视图，使用 Dep 来收集这些 Watcher。
3. 实现一个解析器 Compile，用于扫描和解析的节点的相关指令，并根据初始化模板以及初始化相应的订阅器。

## 3,说说你对 SPA 单页面的理解，它的优缺点分别是什么

SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

**优点：**

- 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
- 基于上面一点，SPA 相对对服务器压力小；
- 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；

**缺点：**

- 初次加载耗时多：为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载；
- 前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理；
- SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势。

## 4,Vue 的单向数据流

所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。

额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。子组件想修改时，只能通过 $emit 派发一个自定义事件，父组件接收到后，由父组件修改。

## 5,computed 和 watch 的区别和运用的场景

**computed：** 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed  的值；

**watch：** 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；

**运用场景：**

- 当我们需要进行数值计算，并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；
- 当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许我们执行异步操作 ( 访问一个 API )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。

## 6,Vue 的父组件和子组件生命周期钩子函数执行顺序？

加载渲染过程

父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted

子组件更新过程

父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated

父组件更新过程

父 beforeUpdate -> 父 updated

销毁过程

父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed

## 9,哪个生命周期内调用异步请求？

可以在钩子函数 created、beforeMount、mounted 中进行调用，因为在这三个钩子函数中，data 已经创建，可以将服务端端返回的数据进行赋值。但是本人推荐在 created 钩子函数中调用异步请求，因为在 created 钩子函数中调用异步请求有以下优点：

- 能更快获取到服务端数据，减少页面 loading 时间；
- ssr 不支持 beforeMount 、mounted 钩子函数，所以放在 created 中有助于一致性；

##  10,在什么阶段才能访问操作DOM

在钩子函数 mounted 被调用前，Vue 已经将编译好的模板挂载到页面上，所以在 mounted 中可以访问操作 DOM

## 11,父组件可以监听到子组件的生命周期吗

比如有父组件 Parent 和子组件 Child，如果父组件监听到子组件挂载 mounted 就做一些逻辑处理，可以通过以下写法实现：

```
// Parent.vue
<Child @mounted="doSomething"/>
    
// Child.vue
mounted() {
  this.$emit("mounted");
}
```

以上需要手动通过 $emit 触发父组件的事件，更简单的方式可以在父组件引用子组件时通过 @hook 来监听即可，如下所示：

```
//  Parent.vue
<Child @hook:mounted="doSomething" ></Child>

doSomething() {
   console.log('父组件监听到 mounted 钩子函数 ...');
},
    
//  Child.vue
mounted(){
   console.log('子组件触发 mounted 钩子函数 ...');
},    
    
// 以上输出顺序为：
// 子组件触发 mounted 钩子函数 ...
// 父组件监听到 mounted 钩子函数 ...  
```

当然 @hook 方法不仅仅是可以监听 mounted，其它的生命周期事件，例如：created，updated 等都可以监听。

## 12,谈谈你对 keep-alive 的了解？

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，避免重新渲染 ，其有以下特性：

- 一般结合路由和动态组件一起使用，用于缓存组件；
- 提供 include 和 exclude 属性，两者都支持字符串或正则表达式， include 表示只有名称匹配的组件会被缓存，exclude 表示任何名称匹配的组件都不会被缓存 ，其中 exclude 的优先级比 include 高；
- 对应两个钩子函数 activated 和 deactivated ，当组件被激活时，触发钩子函数 activated，当组件被移除时，触发钩子函数 deactivated。

## 13,组件中 data 为什么是一个函数？

```
// data
data() {
  return {
	message: "子组件",
	childName:this.name
  }
}

// new Vue
new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: {App}
})
```

因为组件是用来复用的，且 JS 里对象是引用关系，如果组件中 data 是一个对象，那么这样作用域没有隔离，子组件中的 data 属性值会相互影响，如果组件中 data 选项是一个函数，那么每个实例可以维护一份被返回对象的独立的拷贝，组件实例之间的 data 属性值不会互相影响；而 new Vue 的实例，是不会被复用的，因此不存在引用对象的问题。

## 14,v-model 的原理

我们在 vue 项目中主要使用 v-model 指令在表单 input、textarea、select 等元素上创建双向数据绑定，我们知道 v-model 本质上不过是语法糖，v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

(1) v-bind:绑定响应式[数据](http://www.fly63.com/)
(2) 触发 input 事件 并传递数据 (重点)

- text 和 textarea 元素使用 value 属性和 input 事件；
- checkbox 和 radio 使用 checked 属性和 change 事件；
- select 字段将 value 作为 prop 并将 change 作为事件。

以 input 表单元素为例：

```
<input v-model='something'>
    
相当于

<input v-bind:value="something" v-on:input="something = $event.target.value">
```

如果在自定义组件中，v-model 默认会利用名为 value 的 prop 和名为 input 的事件，如下所示：

```
父组件：
<ModelChild v-model="message"></ModelChild>

子组件：
<div>{{value}}</div>

props:{
    value: String
},
methods: {
  test1(){
     this.$emit('input', '小红')
  },
},
```

## 15,Vue 组件间通信有哪几种方式？

Vue 组件间通信只要指以下 3 类通信：父子组件通信、隔代组件通信、兄弟组件通信

**（1）`props / $emit`  适用 父子组件通信**

这种方法是 Vue 组件的基础，相信大部分同学耳闻能详，所以此处就不举例展开介绍。

**（2）`ref` 与 `$parent / $children` 适用 父子组件通信**

- `ref`：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例
- `$parent` / `$children`：访问父 / 子实例

**（3）`EventBus （$emit / $on）`  适用于 父子、隔代、兄弟组件通信**

这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

**（4）`$attrs`/`$listeners` 适用于 隔代组件通信**

- `$attrs`：包含了父作用域中不被 prop 所识别 (且获取) 的特性绑定 ( class 和 style 除外 )。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 ( class 和 style 除外 )，并且可以通过 `v-bind="$attrs"` 传入内部组件。通常配合 inheritAttrs 选项一起使用。
- `$listeners`：包含了父作用域中的 (不含 .native 修饰器的)  v-on 事件监听器。它可以通过 `v-on="$listeners"` 传入内部组件

**（5）`provide / inject` 适用于 隔代组件通信**

祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 inject 来注入变量。 provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

**（6）Vuex  适用于 父子、隔代、兄弟组件通信**

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

- Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
- 改变 store 中的状态的唯一途径就是显式地提交  (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

## 16, Vuex

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

（1）Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

（2）改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

主要包括以下几个模块：

- State：定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation：是唯一更改 store 中状态的方法，且必须是同步函数。
- Action：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
- Module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。

## 17,Virtual DOM 作用是什么？

​	其实虚拟DOM在Vue.js主要做了两件事：

- 提供与真实DOM节点所对应的虚拟节点vnode
- 将虚拟节点vnode和旧虚拟节点oldVnode进行对比，然后更新视图

为何需要Virtual DOM？

- 具备跨平台的优势

由于 Virtual DOM 是以 JavaScript 对象为基础而不依赖真实平台环境，所以使它具有了跨平台的能力，比如说浏览器平台、Weex、Node 等。

- 操作 DOM 慢，js运行效率高。我们可以将DOM对比操作放在JS层，提高效率。

因为DOM操作的执行速度远不如Javascript的运算速度快，因此，把大量的DOM操作搬运到Javascript中，运用patching算法来计算出真正需要更新的节点，最大限度地减少DOM操作，从而显著提高性能。

Virtual DOM 本质上就是在 JS 和 DOM 之间做了一个缓存。可以类比 CPU 和硬盘，既然硬盘这么慢，我们就在它们之间加个缓存：既然 DOM 这么慢，我们就在它们 JS 和 DOM 之间加个缓存。CPU（JS）只操作内存（Virtual DOM），最后的时候再把变更写入硬盘（DOM）

- 提升渲染性能

Virtual DOM的优势不在于单次的操作，而是在大量、频繁的数据更新下，能够对视图进行合理、高效的更新。

为了实现高效的DOM操作，一套高效的虚拟DOM diff算法显得很有必要。**我们通过patch 的核心—-diff 算法，找出本次DOM需要更新的节点来更新，其他的不更新**。比如修改某个model 100次，从1加到100，那么有了Virtual DOM的缓存之后，只会把最后一次修改patch到view上。那diff 算法的实现过程是怎样的？

## 18,vue-router的两种模式的区别

**hash** —— 即地址栏 URL 中的 `#` 符号（此 hash 不是密码学里的散列运算）。
比如这个 URL：`http://www.abc.com/#/hello`，hash 的值为 `#/hello`。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。

**history** —— 利用了 HTML5 History Interface 中新增的 `pushState()` 和 `replaceState()` 方法。（需要特定浏览器支持）
这两个方法应用于浏览器的历史记录栈，在当前已有的 `back`、`forward`、`go` 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。

## 19,为什么vue中的data要用return返回

为什么vue中的data用return返回 1、为什么在项目中data需要使用return返回数据呢？ 不使用return包裹的数据会在项目的全局可见，会造成变量污染；使用return包裹后数据中变量只在当前组件中生效，不会影响其他组件。 #######当一个组件被定义， data 必须声明为返回一个初始数据对象的函数，因为组件可能被用来创建多个实例。如果 data 仍然是一个纯粹的对象，则所有的实例将共享引用同一个数据对象！通过提供 data 函数，每次创建一个新实例后，我们能够调用 data 函数，从而返回初始数据的一个全新副本数据对象。

## 20,vuex中mutation/action的传参方式

1、流程顺序

“相应视图—>修改State”拆分成两部分，视图触发Action，Action再触发Mutation。

2、角色定位

基于流程顺序，二者扮演不同的角色。

Mutation：专注于修改State，理论上是修改State的唯一途径。

Action：业务代码、异步请求。

3、限制

角色不同，二者有不同的限制。

Mutation：必须同步执行。

Action：可以异步，但不能直接操作State。

## 21,Vue中watch对象内属性的方法

1.深度监测 deep

里面的`deep`设为了`true`，这样的话，如果修改了监听对象中的任何一个属性，都会执行`handler`这个方法。不过这样会造成更多的性能开销，尤其是对象里面属性过多，结构嵌套过深的时候。而且有时候我们就只想关心这个对象中的某个特定属性，这个时候可以这样

2,computed

如果监听对象内的某一具体属性，可以通过computed做中间层来实现

## 22,vue-动态组件和异步组件

动态组件:Vue.js 提供了一个特殊的元素 <component> 用来动态地挂载不同的组件。如果我们打算在一个地方根据不同的状态引用不同的组件的话，比如tab页，就可以用到这一标签。

```
<template>
  <div id="app">
    <el-button-group>
      <el-button type="primary" size="small" v-for="item in btnGroup" :key="item.id" @click="handleBtn(item.name)">{{item.name}}</el-button>
    </el-button-group>
    <div>
      <keep-alive>
        <component :is="curComponent"></component>
      </keep-alive>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      curComponent: 'comA',
      btnGroup: [
        {
          id: 1,
          name: '组件一'
        },
        {
          id: 2,
          name: '组件二'
        }
      ]
    }
  },
  components: {
    comA: {
      template: `<input placeholder="请输入名字" type="text"/>`
    },
    comB: {
      template: `<p>2222222222</p>`
    }
  },
  methods: {
    handleBtn (name) {
      if (name === '组件一') {
        this.curComponent = 'comA'
      }
      if (name === '组件二') {
        this.curComponent = 'comB'
      }
    }
  }
}
</script>
```

异步组件:

在大型应用中，我们可能需要将应用分割成小一些的代码块，并且只在需要的时候才从服务器加载一个模块。为了简化，`Vue` 允许你以一个工厂函数的方式定义你的组件，这个工厂函数会异步解析你的组件定义。**`Vue` 只有在这个组件需要被渲染的时候才会触发该工厂函数，且会把结果缓存起来供未来重渲染。**

异步组件存在的意义在于加载一个体量很大的页面时，如果我们不设置加载的优先级的话，那么可能页面在加载视频等信息的时候会非常占用时间，然后主要信息就会阻塞在后面在加载。这对用户来说无疑不是一个很差的体验。但是如果我们设置加载的顺序，那么我们可以优先那些最重要的信息优先显示，优化了整个项目。

# webpack

## 1,打包原理

1. 识别入口文件
2. 通过逐层识别模块依赖(Commonjs、amd或者es6的import，webpack都会对其进行分析，来获取代码的依赖)
3. webpack做的就是分析代码，转换代码，编译代码，输出代码
4. 最终形成打包后的代码

## 2,loder

loader是文件加载器，能够加载资源文件，并对这些文件进行一些处理，诸如编译、压缩等，最终一起打包到指定的文件中

1. 处理一个文件可以使用多个loader，loader的执行顺序和配置中的顺序是相反的，即最后一个loader最先执行，第一个loader最后执行
2. 第一个执行的loader接收源文件内容作为参数，其它loader接收前一个执行的loader的返回值作为参数，最后执行的loader会返回此模块的JavaScript源码

## 3,plugin

在webpack运行的生命周期中会广播出许多事件，plugin可以监听这些事件，在合适的时机通过webpack提供的API改变输出结果。



**loader和plugin的区别**:对于loader，它是一个转换器，将A文件进行编译形成B文件，这里操作的是文件，比如将A.scss转换为A.css，单纯的文件转换过程

plugin是一个扩展器，它丰富了webpack本身，针对是loader结束后，webpack打包的整个过程，它并不直接操作文件，而是基于事件机制工作，会监听webpack打包过程中的某些节点，执行广泛的任务