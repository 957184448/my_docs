# 有效的括号
```javascript
  var isValid = function(s) {
    let stack = [];
    if(s.length % 2 === 1){return false;}
    for(let i = 0;i<s.length;i++){
        if(s[i] === '(' || s[i] === '{' || s[i]==="["){
            stack.push(s[i])
        }else{
            let t = stack[stack.length - 1];
            if( 
                (t === '(' && s[i] ===")") ||
                (t === '{' && s[i] === "}")||
                (t === '[' && s[i] === "]")
            ){
                stack.pop()
            }else{
                return false;
            }
        }
    }
    return stack.length === 0;
};
```

# 二叉树的前序遍历
```javascript
  var preorderTraversal = function(root) {
    const res = [];
    const stack = [];
    if(root)stack.push(root);
    while(stack.length){
       const n = stack.pop();
      res.push(n.val);
      if(n.right) stack.push(n.right);
      if(n.left) stack.push(n.left);
    }
    return res;
};

```