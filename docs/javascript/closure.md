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

 # 节流:减少一段时间的触发频率
```javascript
addEventListener('click',throttle(submit,1500),false);
function submit(e){
  console.log('节流')
}
function throttle (fn,time){
  //设置初始值
  let t = 0;
  return function (){
   //拿到当前点击时间戳
  let cur = new Date().getTime();
  console.log(cur-t);
    //如果当前时间 - 初始时间 > 预设时间 就执行fn
  if(cur - t > time){
    fn.apply(this,arguments);
    t = cur;
    }
  }
}

```