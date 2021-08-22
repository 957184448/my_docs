## 防抖与节流
 - 防抖:利用setTimeout定时器的方式，来设置在规定时间内，将多次触发限制为一次触发;
 ```javascript
  addEventListener('click',debounce(submit,1000),false);
  function submit(e){
    console.log(e);
  }
  function debounce (func,timer){
    //标记是否点击
    let t = null;
    return function (){
      //判断是否为第一次点击
      let first = !t;
      if(t){ clearTimeout(t);}
      if(first){ fn.apply(this.arguments);}
      //清除定时器
      t = setTimeout(()=>{t = null},(timer))
    }
  }
 ```

 - 节流:减少一段时间的触发频率
  <iframe height="510" style="width: 100%;" scrolling="no" title="节流" src="https://codepen.io/yutianchanggong/embed/yLgMJKe?height=510&theme-id=dark&default-tab=html,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/yutianchanggong/pen/yLgMJKe'>节流</a> by leilei
  (<a href='https://codepen.io/yutianchanggong'>@yutianchanggong</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>