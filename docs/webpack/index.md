# module chunk bundle区别?
  - module是各个源码文件，webpack中一切皆是模块
  - chunk是多个模块的合并
  - bundle是最终的输出文件

# loader 和 plugin的区别
  - loader是模块转换器
  - plugin是扩展插件

# babel和 webpack的区别 
  - babel 是js新语法的编译工具，不关心模块化
  - webpack 是打包构建工具 是多个loader与plugin的集合

# 有哪些常见的Loader？他们是解决什么问题的？
  - file-loader：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
  - url-loader : 与file-loader类似，但是只能对比较小的文件把文件通过base64的方式注入到代码中
  - image-loader： 加载并且压缩图片文件
  - babel-loader：把es6转换为es5
  - css-loader：加载css 支持模块化 压缩 文件倒入的形式
  - style-loader：把css注入到javascript中 通过dom操作的方式去加载css
  - eslint-lint：通过eslint检查js代码
  - source-map-loader：加载额外的source-map,以方便断点调试

# 常见的plugin？他们是解决很么问题的
  - commons-chunk-plugin ：提供公共代码
  - define-blugin：定义环境变量

# webpack的构建流
  - 首先初始化参数，用初始化的参数得到complier对象，执行对象的run方法开始编译；
  - 根据配置中的entry找出所有文件的入口， 从入口文件出发调用所有配置的loader，通过loader开始编译b
  - 编译完后得到每个模块被编译后的最终内容以及他们之间的依赖关系；
  - 根据得到的内容组装成包含多个模块的chunk 再把chunk转换成一个单独的文件加入到输出列表，
  - 确定好输出内容后 根据配置确定输出的路径与文件名，把文件打包

# webpack如何配置热更新？热更新的原理是什么
  1. - webpack-dev-server - 用 new webpack.HotModuleReplacementPlugin();
     - 把devserver中的hot字段改为true 
  2. - 使用webpack-dev-middleware 需要创建一个node的server，通常是用express或koa，
      - webpack-dev-middleware  可以将webpack输出的文件传输给服务器，适用于灵活订制场景，可以对webpack配置控制的更多

  官方文档 使应用在运行状态下，不重载刷新就能更新、增加、移除模块的机制；
  原理：热更新有两个过程 
  1 启动阶段，在文件系统中进行编译，将初始代码经过webpack。complier把js编译问bundle，打包好后把编译好的文件传输给
    bundle server（服务器），bundel server就会以server的方式让浏览器访问到，
  2 更新阶段，有文件变化 还是会经过webpack.complier编译，编译好后会将代码发送给hmr server，hrm server就会知道哪些资源模块
    发生了改变，然后hrm server(服务端)会通知hmr runtime(浏览器端)哪些文件发生了变化，发生变化后通常以json数据传输，hmr就会更新代码
    最终代码会进行改变，并且不需要刷新
    
  