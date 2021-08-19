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
  
  
  