# void 0 和undefined的区别

先在一个[js在线压缩的网站](https://skalman.github.io/UglifyJS-online/)操作如下：

```javascript
console.log(a === undefined); // source code
console.log(void 0===a); // minified output code
```

在压缩后的代码中void 0替换了undefined，我们先看看void的用法，然后再看看为何用void 0来代替。

```javascript
void 0 // undefined
void(0) // undefined
void("hello supershy") // undefined
void(console.log(1)) // 打印1，并返回undefined
void 0 = 1 // 报错
```

void(anything)都将**返回undefined**，并且**不能被修改**。

那undefined可以被修改么？

```javascript
var undefined = 1;
console.log(undefined); // 在一些低版本浏览器比如IE8会输出1，天哪
(function(){
  var undefined = 1;
  console.log(undefined); // 仅在chrome中测试过，自执行函数中undefined会被重定义
})()
```

现在看来undefined会在某种情况（低版本浏览器或者自执行函数中）可以被重新定义。

那为何要用void 0呢，用void('supershy')可以么？

```javascript
void 0 // undefined
void('supershy'); // undefined
都会返回undefined，但不论从长度，从名字的含义是不是void 0都好呢，因为谁知道supershy是啥咧^_^
```

总结一下使用void 0代替undefined的原因

1. **undefined在某些情况会被重定义而void 0不会**
2. **void 0更有意义**
3. **void 0字节数少**

ps:一些优秀的库比如underscore源码中就是用void 0来表示undefined

