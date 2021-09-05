# React设计理念
  在开发中什么样的原因制约了快速响应？
  1.计算能力
  2.网络延迟

  cpu瓶颈 io瓶颈  异步可中断的更新
  主流浏览器的刷新频率为60hz，每16.6毫秒刷新一次，在这16.6毫秒中 会依次执行javaScript脚本，样式布局，样式绘制，
  如果js脚本执行时间超过了16.6毫秒 那么这一帧就没有时间留给样式布局和样式绘制，浏览器就会掉帧，表现形式就是浏览器滚动不流畅，
  在输入框输入的内容不能及时响应在页面上，
  一般的解决办法就是做防抖或者节流
  防抖就是利用settimeout在我们一段时间内的多次触发限制为一次触发
  节流就是限制我们的触发频率
  本质上来说这两个办法都是限制我们触发的频率来减少掉帧的可能性
  
  但是随着我们输入的内容越来越多，我们每一次更新所需要的时间都超过浏览器一帧的时间，那么使用节流与防抖也会造成浏览器掉帧

  所以React给出的答案是，将同步跟新改为异步可中断的更新。
  react跟浏览器做了个约定，浏览器将一帧中的时间预留给react，react利用这部分预留的时间来完成工作，
  如果某一个工作需要的时间特别长，超出了这部分预留的时间，
  react会中断自己的工作，并将控制权交给浏览器，等待下一帧自己预留的时间到来以后，react再继续之前被中断的工作
  这样浏览器在每一帧都会有时间执行样式布局与样式绘制，这样就会减少掉帧的可能性
  采用了异步更新这种形式，即使是更新了大量的节点，这种cpu密集型的操作，react也能有效的减少掉帧的可能性；

# React15架构
  Reconciler 协调器 ->1. 负责决定本次更新有哪些组建需要被渲染 ，会调用diff算法，2.在diff算法中会将上次更新的组建与本次更新的组建做对比，最终只有变化的部分会被渲染到试图中。
    diff算法官方名称：Reconcile :协调
  Renderer   渲染器 -> 3.经过diff算法判定为本次需要更新的组建会被交给渲染器渲染到视图中，不同的渲染器会将组建渲染到不同的宿主环境的视图中，
  比如ReactDom渲染器会将组建渲染到浏览器或者SSR中；
  ReactNative渲染器会将组建渲染为aap的原生组建；

# React16新架构
  每个更新会被赋予一个优先级，高优先级的更新会更快的被调度
  Scheduler 调度器-> 
  1.新架构中 更新首先会被调度器Schuduler处理，调度器会更新这些更新组建的优先级，最高优先级的更新会首先进入协调器Reconciler，2。在协调器正在执行diff算法时，如果此时产生了一个跟高优先级的更新，
  那么正在协调的更新会被中断，由于调度器与协调器都是在内存中工作，不会执行具体的视图操作，所以即使有中断发生，用户也不会看到更新不完全的视图，3.当某次更新在协调器中完成时，协调器会通知渲染器，
  本次更新有哪些组建需要执行对应的视图操作，由渲染器来分别执行这些视图操作，对于我们常见的ReactDom来说 这些视图操作就包含了 dom节点的增删改查，
  当高优先级的更新完成时 调度器又会开始新一轮的调度；

  调度接受到更新时会查看是否有更高优先级的更新，如果没有会把更新交给协调器，协调器接收到更新后会调用diff算法，调用diff算法目的是创建一颗虚拟dom树，
  每一个视图上真实存在的节点都有一个虚拟dom节点与其对应，那么diff算法会查看哪些节点发生了改变，会在改变的节点上打一个update标签。
  最终协调器会将打了标记的虚拟com交给渲染器，渲染器接收到通知后会查看有哪些被打了标记的虚拟dom，于是渲染器对这些虚拟dom打了update标签的真实dom进行更新dom的操作，这样就完成了一次更新流程；
  通过调度器-》协调器-》渲染器的相互配合，react新架构就实现了异步可中断的更新
# React新架构 Fiber 数据结构
  fiber就是一个数据结构 
  为了实现fiber这个数据结构 才有了Fiber的结构 单线程调度算法.
  虚拟dom是对真实dom的一种简化

  react fiber架构从始至终都做着三样事情
  当我们调用ReactDo在FiberRootNode节点下创建m.rander时会创建一个FiberRootNode节点。
  1。  RootFiber节点， 是整个应用的根节点 用current属性指向current树
  2。 current树 树上的每一个节点都是fiber 并且每个fiber节点都对应着一个jsx节点  保存的是上一次的状态
  3。 workInProgress树 树上的每一个节点都是fiber 并且每个fiber对应着一个jsx节点  保存的是本次的新状态


  <!-- 初次渲染的时候如果没有对应的current树 那么会创建一个uninitialFiber 然后再去创建workInProgress树 -->

  react中主要分两个阶段
  rander阶段（指的是创建fiber的过程）

  1用深度优先遍历模拟递归的方式为每个节点创建新的fiber（workInProgress） 也可能是复用
  递阶段调用了beginWork方法，归阶段调用了completeWork方法
   ，生成一颗有新状态的workInProgress树
  2.初次渲染的时候会将这个fiber 创建真实的dom节点，并且对当前节点的子节点进行插入 
  3.如果不会初次渲染的话就对比新旧的fiber状态，将产生了更新的fiber节点最终通过链表的形式挂载到新的RootFiber


  commit阶段 才是真正要操作页面的阶段
  1.执行生命周期
  2.会从RootFiber上获取到那条链表updateQueue 根据链表上的标识，状态来合成一个最终需要渲染到页面上的状态， 

  child、return、sibling

 # setState更新同步还是异步
  先给出答案: 有时表现出异步,有时表现出同步
  setState只在合成事件和钩子函数中是“异步”的，在原生事件和setTimeout 中都是同步的。
  但也不是真正的异步，只是把即将要更新的state挂载到当前组建的RootFiber的更新链中了，等当前事件中内部的回调函数执行后才会更新state

  使用Concurrent才是真正的异步更新，同样的没法立即获取最新状态，并且在执行react的更新和渲染的过程中使用了postMessage方法，会把更新fiber的过程放到eventloop中去执行，
  这个才是真正的异步

  flushSync这个api的时候，react的更新和渲染完全是同步的
  会立即触发更新state以及渲染的过程 ，这种情况才是真正的同步

# jsx与fiber有什么关系
  创建fiber节点的依据就是组建返回的jsx对象，
  而在更新时已经存在了一颗currentFiber树，所以在生成WorkInProgressFiber节点时会将组建返回的jsx对象与这个组建对应的current节点做对比
  根据对比的结果生成这个组建的workInProgressFiber 这就是jsx与fiber的关系 
# jsx 虚拟dom
  jsx是React中的虚拟dom，
  jsx会被Babel编译为React.createElement( type , null, "1")
  第一个参数是标签，第二个参数是属性，第三个参数是子节点这种形式

#  什么是diff算法
  diff算法就是 currentFiber与jsx对象，将对比的结果用来生成wordInProgressFiber,这个对比的过程就是diff算法
   在render阶段更新Fiber节点时，我们会调用reconcileChildFibers对比current Fiber和jsx对象构建workInProgress Fiber，
   <!-- 这里current Fiber是指当前dom对应的fiber树 -->
  diff分为单一节点的diff与多节点的diff
  ​在reconcileChildFibers中会根据newChild的类型来进入单节点的diff或者多节点diff
  单一节点的diff会判断上次更新时的fiber节点是否存在 如果存在可以复用 ，否则生成新Fiber节点并返回
  在源码中多节点diff会经历三次遍历，第一次遍历处理节点的更新（包括props更新和type更新和删除），第二次遍历处理其他的情况（节点新增），其原因在于在大多数的应用中，节点更新的频率更加频繁，第三次处理位节点置改变
# this.setState流程
  通过component.prototype找到setstate方法，执行this.updeter.enqueueSetState,
  然后这个方法会把当前this，partialState就是要更新的state，还有callback传入
  执行enqueueSetState通过实例获取到当前的fiber，然后拿到当前事件的eventTime,然后创建update，update.payload就会赋值为partialState 就是当前传入的要更新的state
  创建更新
  把fiber挂载到updateQueue

# 虚拟dom的优势
  性能有下限：通过diff算法找出最小的差异 统一patch
  跨平台：jsx本质上就是jsx对象

# react的生命周期
  - constructor 构造函数
  - componentwillmount 更新前
  - rander 更新
  - componentdidmount 更新后
  - componentWillReceiveProps 这个生命周期可以将props转换成自己的state
  - shouldcomponentupdate （nextProps, nextState） 是否更新， 两个参数标识新的props和旧的state 可以通过这个生命周期做优化
  - componentWillupdate 
  - rander
  - componentDidupdate
  - componentUpMount 卸载
  
  # redux的工作流程
  1. 创建一个store用来存在数据
  2. 触发view层更新，发出一个dispatch，用来更改或计算state
  3. reducer函数接收 action和state(View要发送多少种消息，就会有多少种Action),return 一个新的state

  # react-redux是如何工作的?
  1. Provider: Provider的作用是从最外部封装了整个应用，并向connect模块传递store
  2. connect: 负责连接React和Redux


  
   




































   