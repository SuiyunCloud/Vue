**This document record ES6~ES9 new features**


# ES6(2015)
1. class
    ```js
      class Animal {
        // 构造函数，实例化的时候将会被调用，如果不指定，那么会有一个不带参数的默认构造函数.
        constructor(name,color) {
        this.name = name;
        this.color = color;
        }
        // toString 是原型对象上的属性
        toString() {
        console.log('name:' + this.name + ',color:' + this.color);

        }
    }

    var animal = new Animal('dog','white');//实例化Animal
    animal.toString();

    console.log(animal.hasOwnProperty('name')); //true
    console.log(animal.hasOwnProperty('toString')); // false
    console.log(animal.__proto__.hasOwnProperty('toString')); // true

    class Cat extends Animal {
    constructor(action) {
        // 子类必须要在constructor中指定super 函数，否则在新建实例的时候会报错.
        // 如果没有置顶consructor,默认带super函数的constructor将会被添加、
        super('cat','white');
        this.action = action;
    }
    toString() {
        console.log(super.toString());
    }
    }

    var cat = new Cat('catch')
    cat.toString();

    // 实例cat 是 Cat 和 Animal 的实例，和Es5完全一致。
    console.log(cat instanceof Cat); // true
    console.log(cat instanceof Animal); // true

2. Module
Use `export` to define exposed interface to outside. Use `import` to refer other module's object.

    ```js
        export var name = 'Hello'
        export {name, age}
        export function myModule(someArg){
            return someArg;
        }

        import {myModule} from 'myModule';

    ```

3. Arrow function
`=>` is short for `function`.箭头函数与包围它的代码共享同一个this,能帮你很好的解决this的指向问题。有经验的JavaScript开发者都熟悉诸如var self = this;或var that = this这种引用外围this的模式。但借助=>，就不需要这种模式了。

    ```js
    // 箭头函数的例子
    ()=>1
    v=>v+1
    (a,b)=>a+b
    ()=>{
        alert("foo");
    }
    e=>{
        if (e == 0){
            return 0;
        }
        return 1000/e;
    }
    ```

4. default value for parameter in function

    ```js
    function foo(height = 50, color = 'red')
    {
        // ...
    }
    ```

5. template string with `{}`

    var name = `Your name is ${first} ${last}.`  //first and last is variable

6. unpackage

    ```js
    var foo = ["one", "two", "three", "four"];

    var [one, two, three] = foo;
    var [first, , , last] = foo;

    [a, b] = [1, 2];


    //set default value
    [a=5, b=7] = [1];
    console.log(a); // 1
    console.log(b); // 7

    //exchage value
    [a, b] = [b, a];

    const student = {
    name:'Ming',
    age:'18',
    city:'Shanghai'  
    };

    const {name,age,city} = student;
    ```

7. Spread operator(...)
可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造对象时, 将对象表达式按key-value的方式展开

    ```js
    function sum(x, y, z) {
    return x + y + z;
    }
    const numbers = [1, 2, 3];
    console.log(sum(...numbers));//6

    const stuendts = ['Jine','Tom']; 
    const persons = ['Tony',... stuendts,'Aaron','Anna'];

    var arr = [1, 2, 3];
    var arr2 = [...arr]; // 等同于 arr.slice()
    arr2.push(4); 
    console.log(arr2)//[1, 2, 3, 4]

    var arr1 = [0, 1, 2];
    var arr2 = [3, 4, 5];
    var arr3 = [...arr1, ...arr2];// 将 arr2 中所有元素附加到 arr1 后面并返回
    //等同于
    var arr4 = arr1.concat(arr2);

    var obj1 = { foo: 'bar', x: 42 };
    var obj2 = { foo: 'baz', y: 13 };

    var clonedObj = { ...obj1 };
    // 克隆后的对象: { foo: "bar", x: 42 }

    var mergedObj = { ...obj1, ...obj2 };
    // 合并后的对象: { foo: "baz", x: 42, y: 13 }
    ```

8. Object attribute simplification

    ```js
    //Old way
    const name='Ming',age='18',city='Shanghai';
    const student = {
        name:name,
        age:age,
        city:city
    };
    console.log(student);//{name: "Ming", age: "18", city: "Shanghai"}

    //New way
    const name='Ming',age='18',city='Shanghai';
  
    const student = {
        name,
        age,
        city
    };
    ```
9. Promise

10. let, const
在之前JS是没有块级作用域的，const与let填补了这方便的空白，const与let都是块级作用域。

    ```js
    //使用var定义的变量为global作用域：
    {
    var a = 10;
    }

    console.log(a); // 输出10

    //使用let与const定义的变量为块级作用域：
    {
    let a = 10;
    }

    console.log(a); //-1 or Error“ReferenceError: a is not defined”
    ```
11. Iterators

    ```js
    for (var n of ['a','b','c'])

    
    ```


# ES7(2016)
1. Array.prototype.includes()
includes() 函数用来判断一个数组是否包含一个指定的值，如果包含则返回 true，否则返回false。

    ```js
    let arr = ['react', 'angular', 'vue'];

    if (arr.includes('react'))
    {
        console.log('react存在');
    }
    ```

2. `**`

    2**10 == Math.pow(2, 10)

# ES8(2017)

1. async/await
异步迭代器（asynchronous iterators），这就像常规迭代器，除了next()方法返回一个Promise。因此await可以和for...of循环一起使用，以串行的方式运行异步操作。
```js
async function process(array) {
  for await (let i of array) {
    doSomething(i);
  }
}
```

2. Object.values()
Object.values()是一个与Object.keys()类似的新函数, used to get value of object

3. Object.entries()

    ```js
    let obj = { one: 1, two: 2 };
    for (let [k,v] of Object.entries(obj)) {
    console.log(`${JSON.stringify(k)}: ${JSON.stringify(v)}`);
    }
    ```


# ES9(2018)
一个Promise调用链要么成功到达最后一个.then()，要么失败触发.catch()。在某些情况下，你想要在无论Promise运行成功还是失败，运行相同的代码，例如清除，删除对话，关闭数据库连接等。

```js
function doSomething() {
  doSomething1()
  .then(doSomething2)
  .then(doSomething3)
  .catch(err => {
    console.log(err);
  })
  .finally(() => {
    // finish here!
  });
}
```


