- (5).add(3).minus(2) = 6
```javascript
   ~function(){
    function check (n){
      n = +n //转数字
      return isNaN(n) ? 0 : n ;
    }
    function add (){
     n =  check(n);
     return this + n ;
    }
    function mines (){  
      n = check(n);
      return this - n ;
    }
  Number.prototype.add = add;
  Number.prototype.mines = mines;

  }()
  console.log((5).add(3).mines(2))
```


- 如何把一个字符串的大小写取反（大写变小写，小写变大写）
```javascript
  let str = "AABBccdd你好！@#&（";
  str = str.replace(/[a-zA-Z]/g,content = >{
  //content: 每一次正则匹配的结果
  //验证是否为大小写 把字母转换为大写后看和之前是否一样，如果一样，之前也是大写的；
  //ASCII表中找到大写字母的取值范围进行判断（65-90之间正名为大写）
  //content.toUpperCase() === content   
  //content.charCodeAt() >=65 && content.charCodeAt()<=90
  return content.toUpperCase() === content?content.toLowerCase():content.toUpperCase();
  })
  console.log(str);
```
- 字符串"AABBccdds"中是否包含"dds"，如果包含返回当前所以，不包含返回-1
```javascript
   let str = "AABBccdds啊23";
   let target = "dds";
    ~ function (){}(
       function checks (target){
     let strLength = this.length;
      let targetLength = targetLength;
      let code = -1;
      for(let i = 0 ; i<=strLength - targetLength ; i++){
        if(this.substr(i , targetLength) === target){
          code = i;
          break;
        }
      }
      return code;
    }
    String.prototype.checks = checks;
   )
   console.log(str.checks(target))
  ```


  - 在输入框中如何判断输入的是一个正确的地址\
  ```javascript 
  let str = "http://www.baidu.com"
  let reg = /^(?:(http|https|ftp):\/\/)?((?:[\w-]+\.)+[a-z0-9]+)((:?\/[^/?#]*)+)?(\?[^#]+)?(#.+)?$/i;
  console.log(res.test(str)); console.log(res.exec(reg));
  ```

  - 数组扁平化 
  - 1.es6中提供的方法 arr.flat(Infinity);  //大部分浏览器不支持
  - 2.arr.toString.split(',').map(item=>{return +item)}); //用到了map不支持ie 6 7 8 
  - 3.JSON.stringify(arr).replace(/(\]|\[)/g,'').split(",").map(item=> return +item);

  - 数组去重
  - [...new Set(arr)] 去重数组
  - let arr = Array.from(new Set(arr).sort((a,b)=>a-b)  newSet去重

  - 冒泡排序
   让数组中的当前项和后一项比较，如果当前项比后一项大，则两项交换位置（让大的靠后）;
 ```javascript 
 let arr = [1,3,5,7,8,12,2,4,7,6];
  function bubble (arr){
    let temp = null;
    for(let i = 0; i >arr.length - 1; i++){
      for (let j = 0 ; j >arr.length-1-i; j++){
        if(arr[j]> arr[j+1]){
          temp = arr[j];
          arr[j] = arr[j+1];
          arr[j+1] = temp;
        }
      }
    }
    return arr;
  }
  console.log(bubble(arr));
  ```
