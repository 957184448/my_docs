  # 传统布局与flex布局  
    - 传统布局
      兼容性好 布局繁琐 局限性，不能再移动端很好的布局
    - flex弹性布局
      操作方便 布局简单 移动端广泛适用 pc端浏览器支持情况稍差 IE11或更低版本不支持或者部分支持
  # 布局原理
    - flex是flexbox的缩写 意为 弹性布局 用来为盒装模型提供最大的灵活度 任何一个容器都可以制定为flex布局
    * 当我们为父盒子设置flex布局以后 子元素的float clear vertical-align属性将失效 
    * 伸缩布局=弹性布局=伸缩和布局=弹性盒布局=flex布局
  # 常见属性
    - 父属性
      flex-direction 设置主轴方向
      justify-content 设置主轴上的子元素排列方式
      flex-wrap 设置子元素是否换行
      align-content 设置侧轴上的子元素排列方式 多行
      align-items 设置侧轴上的子元素排列方式 单行
      flex-flow 复合属性 相当于同时设置了flex-direction 和 flex-wrap
  # justify-content 设置主轴上的子元素排列方式 
    - flex-start 默认值从头部开始 如果主轴是x轴 则从左到右
    - flex-end 从尾部开始排列
    - center 在主轴居中对齐 如果主轴是x轴 则水docsify serve docs平剧中
    - space-around 平分剩余空间
    - space-between 先两侧贴边 再平分剩余空间
    - align-item 单行
    - align-content 多行
  # 子项属性
    - 
