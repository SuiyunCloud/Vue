# 异步转同步

借助Promise
```js
var p = Promise.resolve(that.changeApplicationValue(parent_application_id))  //that.changeApplicationValue(parent_application_id)中有多层异步操作
p.then(()=>{
  that.setRepository(val.repository_id)
})
```

* Promise.resolve 方法，Promise.reject 方法

有时需要将现有对象转为Promise对象，Promise.resolve方法就起到这个作用。

var jsPromise = Promise.resolve($.ajax('/whatever.json'));
上面代码将 jQuery 生成 deferred 对象，转为一个新的 ES6 的 Promise 对象。

如果 Promise.resolve 方法的参数，不是具有 then 方法的对象（又称 thenable 对象），则返回一个新的 Promise 对象，且它的状态为fulfilled。

```js
var p = Promise.resolve('Hello');
 
p.then(function (s){
  console.log(s)
});
// Hello
```

上面代码生成一个新的Promise对象的实例p，它的状态为fulfilled，所以回调函数会立即执行，Promise.resolve方法的参数就是回调函数的参数。

如果Promise.resolve方法的参数是一个Promise对象的实例，则会被原封不动地返回。

```js
Promise.reject(reason)方法也会返回一个新的Promise实例，该实例的状态为rejected。Promise.reject方法的参数reason，会被传递给实例的回调函数。

var p = Promise.reject('出错了');
 
p.then(null, function (s){
  console.log(s)
});
// 出错了
```

上面代码生成一个Promise对象的实例p，状态为rejected，回调函数会立即执行。
