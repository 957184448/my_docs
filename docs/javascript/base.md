  # typeof可以判断哪些类型？

  # call 和 apply的区别事什么？
  - call和apply都是function原型上的方法，
  两个方法执行的目的都是改变this指向的，
  唯一区别 call传递方式是一个一个传递，
  apply传递方式是一个数字，
  bind没有把函数立即执行，只是预先把函数中的this进行处理
  
  # 箭头函数与普通函数的区别是什么 构造函数可以使用new生成实例 那么箭头函数可以吗 为什么
  - 箭头函数语法上比普通函数简介
  - 箭头函数中没有自己的this，this从属于函数所处上下文 call，apply等方式无法改变this指向 
  - 箭头函数中没有arguments类数组，只能基于...arg获取传递的参数集合(数组)
  - 箭头函数不能被new执行 因为箭头函数没有this，也没有prototype(没有原型，所以也没有constructor)
  
  # HTML5 新特性
  - 语义化标签 header footer section nav
  - 媒体标签 audio video
  - web存储 localStorage sessionStorage

  # 行内元素 块元素有哪些
  * 行内元素
    a span img input
  * 块元素
    div ul li p 

  # js有哪些数据类型
   - 基本数据类型
    null undefined boolean string number symbol BigInt 最大安全整数
   - 引用数据类型
    object array function
  
  # iframe 优缺点？
    * 优点
      - 原封不动的嵌入其他页面
      - 用来加载比较慢的内容
    * 缺点
      - 网页内容无法被搜索引擎识别，对SEO不友好
      - iframe阻塞onload事件加载
  # css3新特性
    * 特效： text-shadow box-shadow
    * 渐变： gradient 
    * 过度动画 transform
    * 动画：animation
  # 标准盒模型和ie盒模型区别
   - 盒模型都是有四个部分组成 content padding margin border
    标准盒子模型和ie盒子模型的区别在于 设置width 和 height 时 对应的范围不同
    * 标准盒子模型的width 和 height 只包含了content区域
    * ie盒子模型width 和 height 包含了border margin padding 
  - 通过修改元素的box-sizing属性来改变元素的盒子模型
    box-sizing ： content-box 标准盒子模型
    box-sizing ： border-box ie盒子模型

  # transform和animation的区别
  - transform是过度动画 强调过度 需要一个事件来触发
  - animation是动画属性 它不需要事件触发，设定好后自动执行

  # 元素水平居中
  - 绝对定位 父级元素
  ```css
    .parent{
      position: relative
    }
    .child{
      position : absolute;
      top:50%;
      left :50%;
      transform:translate(-50% , -50%);//translate 元素的中心点到页面的中心点的距离
    }
  ``` 
  - flex布局
  ```css
    .parent{
      display:'flex';
    }
    .child{
      justify-content :'center';
      align-item :'center';
    }
  ```
  # px,em,rem 的区别
    * px是固定像素
    * em是相对于父级元素的单位，会随着父级元素变化而变化
    * rem是相对于根元素html，它会随着html元素的变化而变化
  
  # 如何解决1px问题？
    - 直接写0.5px
    - 利用伪元素，先放大后缩小

   # CSS选择器优先级
    - @important
    - 内联样式
    - ID选择器
    - 类选择器/属性选择器/伪类选择器
    - 元素选择器/伪元素选择器
    - 关系选择器/通配符选择器

  # 什么是闭包？
    - 闭包就是一个函数内的私有函数，内部的函数可以访问整个闭包内的私有变量，相当于创建了一个私有作用域；

  # new操作符都做了什么
    - 创建了一个控对象，将这个对象的原型设置到prototype上，new执行就是创建了一个构造函数 把这构造函数放到对象原型的prototype上。

  # 原型 原型链
    - 每个对象初始化的时候都会初始化一个prototype原型属性，而对象的__proto__属性会指向它的原型对象
    - 访问原型有两种方式 一种是实例的foo.__proto__ 另一种是构造函数 foo.prototype的方式
    - __proto__是系统内置的方式 不推荐，
    - 当我们访问对象的属性时，如果这个属性不存在，那么就会去他原型对象上进行查找。而这个原型对象有会有自己的原型，就会这样一直查找，直到查找到顶级对象object上为止， 这就是原型链


  # 继承
    - 原型链继承 利用原型链，将子类prototype指向父类的构造函数创建出来的实例对象
    ```javascript 
      function person (){};
      function son (){};
      son.prototype = new Person();
    ```
    - 构造函数继承 利用call()或apply()方法，在子类中借用父类的构造函数，初始化父类的构造函数
    ```javascript 
      function person(){}
      function son (name){
        person.apply(this,name)
      }
    ```
    - 组合继承 将原型链继承与构造函数融合在一起 先让子类的prorotype = 父类的new执行， 再让子类的constructor = 子类
    - 原型继承 
    - 寄生组合继承  

  # 浏览器的渲染原理
    - 首先从上解析html 生成DOM tree
    - 解析css 生成cssom 
    - 根据dom tree 与 cssom 生成rander tree 
    - 引发回流 根据生成的rander tree 计算在当前设备视口内的位置与大小
    - 引发重绘 根据rander tree 与回流后的信息 计算节点上的像素与颜色
    - 将最终得到的像素交给gpu 渲染在页面上

  # 事件冒泡，事件捕获（事件委托）
    - 事件冒泡就是当一个对象上触发了某类事件，如果这个对象绑定了事件，就执行，如果没绑定，就会向父级元素传播，最终通过父级触发了事件；
    - 事件委托本质上就是利用了事件冒泡的原理，因为事件冒泡最终会传播到父级节点上，并且父级节点可以通过事件对象来获取到当前节点，所以可以
    - 把子节点的监听函数定义在父节点上，由父节点统一处理多个子元素的事件，这种方式叫做事件委托

  # es6新特性
    - let const 
    - 增加symbol 标识独一无二的值，用来定义唯一的对象属性名
    - 解构赋值 
    - 模版字符串 "${data}"
    - 箭头函数
    - set和map
    - promise 
    - async await 
  
  # http与https的区别
    - http是不安全的，https是安全的
    - http标准端口是80， https是433
    - http无法加密，https对传输的数据进行加密
    - http无需证书，https需要ssl证书

  # get和post的区别
    - get请求会被浏览器主动缓存，post不会，需要手动设置，
    - get请求是有长度限制的，post没有限制
    - get参数通过url传递，post放在Request body中
    - get请求报漏在地址栏，post放在报文中，相对来说更安全
    - get产生一个tcp数据包，post产生两个

  # xss攻击，csrf攻击，doos攻击
    - xss是代码注入的形式
    - csrf是诱导受害者进入第三方网站
    - ddos原理就是利用大量请求造成资源过载，导致服务不可用

  # http状态码
    - 200相应成功
    - 301永久重定向
    - 302临时重定向
    - 304资源缓存
    - 403服务器禁止访问
    - 404服务器资源未找到
    - 500 502服务器内部错误
    - 504服务器繁忙
  
  # http三次握手 四次挥手
    - 1. 客户端发送syn报文到服务器发起握手。发送完后客户端处于syn_send状态
    - 2. 服务端收到syn报文之后回复syn和ack报文给客户端
    - 3. 客户端收到syn和ack，向服务端发送一个ack报文，客户端转为established（确定）状态，此时服务端收到ack报文后也处于确定状态，此时双方已建立链接
    - 4. 
  
  # 强缓存和协商缓存
    - 强缓存用的是Expires和cache-control两个字段来控制
    - 协商缓存是由服务器来确定缓存资源是否可用的
  
  # cookie sessionStorage localStorage区别
    1. cookie数据之中在http请求中携带，同时每次http请求都会携带cookie，
        而sessionstorage和localstorage不会自动把数据发送给服务器，仅在本地保存
    2. 存储大小不同，cookie数据不能超过4k，sessionstorage和localstorage大小可以达到5M
    3. cookie有过期时间，sessionstorage在浏览器窗口关闭前有效，localstorage浏览器关闭也有效

  
  # MVVM 
    - 是一种架构模式 m标识module数据模型。v代表视图 vm代表视图模型 它是module与view是桥梁，数据会绑定到viewmodal层并自动将数据渲染到页面层，
    - 视图变化会通知viewmodal更新数据

