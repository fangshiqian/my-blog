---
title: 异步编程--Promise与Async
date: 2019-11-28 19:50:14
top:
categories: 学习
tags: 异步编程、Promise、Async函数
---

## 1. 什么是异步编程

```js
<body>
    <button id="Button">展示异步操作</button>
    <script>
        var Button = document.getElementById('Button');
        console.log(Button);
        Button.onclick = function () {
            console.log('展示异步操作--a');
            
        }
        console.log('展示异步操作--b');
    </script>
</body>
```

​																						↓↓

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/3234)

> 如上图所示,代码会先执行 '展示异步操作--b' 然后点击按钮后悔再执行 '展示异步操作--a'
>
> 简单的理解就是: 
>
> ​		同步是指：当程序1调用程序2时，程序1停下不动，直到程序2完成回到程序1来，程序1才继续执行下去。 
> ​		异步是指：当程序1调用程序2时，程序1径自继续自己的下一个动作，不受程序2的的影响。 
>
> ​		异步函数的特点就是不等待

## 2. 在JavaScript中常见的异步代码是什么

> ​	浏览器中的定时器
>
> ​	Ajax请求
>
> ​	node.js的文件操作
>
> ​	网络操作

定时器:

```js
<body>
  <script>
    console.log('a')

    // 定时器
    // 在 JavaScript 中，记住一件事儿：所有的异步回调函数执行一定在普通代码执行之后
    // 把该任务先分配下去
    setTimeout(function () {
      console.log('b')
    }, 0)
    // 输出 c
    console.log('c')

    for (var i = 0; i < 100; i++) {
      console.log(i)
    }
  </script>
</body>
```

请求:

```js
<body>
  <script>
    console.log(1)

    // 创建请求对象
    var oReq = new XMLHttpRequest();

    // 添加请求回调函数
    // 请求成功，就会自动执行该回调函数
    oReq.addEventListener("load", function () {
      console.log(2)
      // 获取输出响应结果
      console.log(this.responseText);
    });

    // 设置请求方法和请求路径
    oReq.open("GET", "http://jsonplaceholder.typicode.com/posts");

    // 发出请求
    oReq.send();

    console.log(3)
  </script>
</body>

// jsonplaceholder为免费的在线请求接口
// 输出结果 1 3 2
```

## 3. 异步控制

异步并行: 输出结果 不确定

异步串行: 输出结果 1-5-2-3-4

```js
<body>
  <script src="request.js"></script>
  <script>
    /**
     * 异步并行
     */

    // 异步的
    request('http://jsonplaceholder.typicode.com/posts', function (data) {
      console.log('posts 的响应结果')
    })

    // 异步的
    request('http://jsonplaceholder.typicode.com/comments', function (data) {
      console.log('comments 的响应结果')
    })

    // 异步的
    request('http://jsonplaceholder.typicode.com/users', function (data) {
      console.log('users 的响应结果')
    })

    /**
     * 异步串行
     */
    console.log(1)

    request('http://jsonplaceholder.typicode.com/posts', function (data) {
      console.log('2 posts 的响应结果')

      // 请求下一个
      request('http://jsonplaceholder.typicode.com/users', function (data) {
        console.log('3 users 的响应结果')

         request('http://jsonplaceholder.typicode.com/comments', function (data) {
          console.log('4 comments 的响应结果')
         })
      })
    })

    console.log(5)
  </script>
```



## 4. 回调地狱(异步函数会出现的问题)

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E5%9B%9E%E8%B0%83%E5%9C%B0%E7%8B%B1)

异步串行就会出现上述问题

不影响功能,只是不利于阅读和维护

## 5. `Promise`(解决回调地狱)

> ​	为了更好的学习 Promise，建议参考 http://es6.ruanyifeng.com/#docs/promise 

我们一直使用axios,其实就是`封装`的`Promise`

```js
axios({
	method: 'xxx',
	url:''
}).then(res => {
	console.log(res)
})
```

```js

```

使用axios解决回调地狱问题的时候

```js
<body>
  <script src="node_modules/axios/dist/axios.js"></script>
  <script>
    console.log(1)

    // 一切的一切都是：Promise
	// 正确的使用
    axios({
      method: 'GET',
      url: 'http://jsonplaceholder.typicode.com/posts'
    })
    .then(res => {
      console.log('2 posts 的响应结果')
      return axios({
        method: 'GET',
        url: 'http://jsonplaceholder.typicode.com/users'
      })
    })
    .then(res => {
      console.log('3 users 的响应结果')
      return axios({
        method: 'GET',
        url: 'http://jsonplaceholder.typicode.com/comments'
      })
    })
    .then(res => {
      console.log('4 comments 的响应结果')
    })
	// 不好的使用
    axios({
      method: 'GET',
      url: 'http://jsonplaceholder.typicode.com/posts'
    }).then(res => {
      console.log('2 posts 的响应结果')
      axios({
        method: 'GET',
        url: 'http://jsonplaceholder.typicode.com/users'
      }).then(res => {
        console.log('3 users 的响应结果')
        axios({
          method: 'GET',
          url: 'http://jsonplaceholder.typicode.com/comments'
        }).then(res => {
          console.log('4 comments 的响应结果')
        })
      })
    })

    console.log(5)
  </script>
</body>
```

### 5.1. 基本概念

> Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。 它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了 Promise 对象。 
>
> 所谓 Promise ，简单说就是一个容器，里面保存着异步操作。从语法上说，Promise 是一个对象，从 它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。
>
> 有了 Promise 对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此 外， Promise 对象提供统一的接口，使得控制异步操作更加容易。 
>
>  Promise 也有一些缺点。首先，无法取消 Promise ，一旦新建它就会立即执行，无法中途取消。其 次，如果不设置回调函数， Promise 内部抛出的错误，不会反应到外部。第三，当处于 pending 状态 时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

### 5.2. 基本用法

 ES6 规定， Promise 对象是一个构造函数，用来生成 Promise 实例。 
 下面代码创造了一个 Promise 实例

```js
const promise = new Promise(function(resolve, reject) {  
// ... some code
 if (/* 异步操作成功 */){   
 	resolve(value);  
 } else {
 	reject(error);  
 }
});
```

Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject 。它们是两个 函数，由 JavaScript 引擎提供，不用自己部署。 

resolve 函数的作用是，将 Promise 对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去； reject 函数的作用 是，将 Promise 对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时 调用，并将异步操作报出的错误，作为参数传递出去。

Promise 实例生成以后，可以用 then 方法分别指定 resolved 状态和 rejected 状态的回调函数

```js
promise.then(function(value) {
	// success 
}, function(error) {
	// failure
});

```

then 方法可以接受两个回调函数作为参数。第一个回调函数是 Promise 对象的状态变为 resolved 时 调用，第二个回调函数是 Promise 对象的状态变为 rejected 时调用。其中，第二个函数是可选的，不 一定要提供。这两个函数都接受 Promise 对象传出的值作为参数。
下面是一个 Promise 对象的简单例子。

```js
function timeout(ms) {
	return new Promise((resolve, reject) => {
    	setTimeout(resolve, ms, 'done');
   }); 
}
timeout(100).then((value) => {
	console.log(value); 
});

```

上面代码中， timeout 方法返回一个 Promise 实例，表示一段时间以后才会发生的结果。过了指定的 时间（ ms 参数）以后， Promise 实例的状态变为 resolved ，就会触发 then 方法绑定的回调函数。 

### 5.3. then 方法

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <script>
    // 将一个异步代码包装到 Promise 中
    // 1、定义一个函数
    function request(url) {
      // 2、在函数中 return 出一个 Promise 对象
      return new Promise((resolve, reject) => {
        // 3、在 Promise 容器中执行异步操作
        // 4、异步操作
        //    成功：resolve
        //    失败：reject
        // 创建请求对象
        var oReq = new XMLHttpRequest();

        // 添加请求回调函数
        // 请求成功，就会自动执行该回调函数
        oReq.addEventListener("load", function () {
          // 获取输出响应结果
          // console.log(this.responseText);

          // 当请求成功了，也就是异步执行结束了，callback 被调用了
          // 我调用的时候，给 callback 传递了一个参数
          // callback(this.responseText)

          // 如果没有数据
          // resolve()

          // 如果有数据
          resolve(this.responseText)

          // 只有这里才能拿到正确的响应结果 responseText
          // return this.responseText
        });

        oReq.addEventListener("error", function (err) {
          // 失败 reject
          reject(err)
        });

        // 设置请求方法和请求路径
        oReq.open("GET", url);

        // 发出请求
        oReq.send();
      })
    }

    // 执行获取结果
    // p.then(成功, 失败)

    // Promise 都是通过 .then 方法来获取成功或者失败的结果
    // request('http://jsonplaceholder.typicode.com/posts')
    //   .then(data => { // 参数1：resolve
    //     console.log('成功了', data)
    //   }, err => { // 参数2：reject
    //     console.log('失败了', err)
    //   })

    // then 方法之后可以继续 then
    // 原因是 then 方法执行完以后会返回一个新的 Promise 对象
    request('http://jsonplaceholder.typicode.com/posts')
      .then(data => {
        console.log(1)
        // return new Promise((resolve) => {
        //  resolve()
        // })

        // 如果是普通数据，那么它会把该数据包装为那个返回的 Promise 的 resolve 结果
        // return new Promise((resolve) => {
        //   resolve('hello')
        // })
        // return 'hello'

        // 因为每个 then 始终返回 promise 对象
        // 所以我才可以在后面继续 .then
        // 每一个后续的 .then 都是在给上一个 then 中返回的 Promise 对象注册：resolve、reject

        // 如果你返回的数据就是一个 Promise 对象，那它就不做任何处理了
        return new Promise((resolve) => {
          setTimeout(() => {
            resolve('hello')
          }, 2000)
        })
      })
      .then((data) => {
        console.log(2, data)
        // return new Promise((resolve) => {
        //   setTimeout(() => {
        //     resolve('hello')
        //   }, 1000)
        // })

        // ptimeout(1000) 返回一个 promise 对象
        // const p = ptimeout(1000)
        // return p

        return ptimeout(1000)
      })
      .then(() => {
        console.log(3)
      })
      .then(() => {
        console.log(4)
      })

    function ptimeout(time) {
      return new Promise((resolve) => {
        setTimeout(function () {
          resolve()
        }, time)
      })
    }

    // Async 函数，简化了 Promise 的结果获取而已
  </script>
</body>
</html>

```

### 5.4. 使用 Promise 的方式封装异步操作

操作步骤:

```bash
1、定义一个函数 
2、在函数中返回一个 Promise 对象 
3、在 Promise 容器中执行异步操作 
4、成功：resolve；失败 reject；

```

例如：

```js
function request(url) {
      // 2、在函数中 return 出一个 Promise 对象
      return new Promise((resolve, reject) => {
        // 3、在 Promise 容器中执行异步操作
        // 4、异步操作
        //    成功：resolve
        //    失败：reject
        // 创建请求对象
        var oReq = new XMLHttpRequest();

        // 添加请求回调函数
        // 请求成功，就会自动执行该回调函数
        oReq.addEventListener("load", function () {
          // 获取输出响应结果
          // console.log(this.responseText);

          // 当请求成功了，也就是异步执行结束了，callback 被调用了
          // 我调用的时候，给 callback 传递了一个参数
          // callback(this.responseText)

          // 如果没有数据
          // resolve()

          // 如果有数据
          resolve(this.responseText)

          // 只有这里才能拿到正确的响应结果 responseText
          // return this.responseText
        });

        oReq.addEventListener("error", function (err) {
          // 失败 reject
          reject(err)
        });

        // 设置请求方法和请求路径
        oReq.open("GET", url);

        // 发出请求
        oReq.send();
      })
    }

```

使用:

```js
request('请求路径')  
	.then(data => {
    	// 其它逻辑
       }, err => {
       // 处理异常
      })
```

尤其是当你想要控制多个异步代码的时候，这个时候才能真正发挥 Promise 的价值：

```js
request('请求路径')
	.then(data => {
		console.log(data)
		return promise 包装了定时器
	})
	.then(() => {
		// 定时器时间到了
		return promise 对象 (异步操作)
	})
	then(() => { })
```

### 5.5. 异常处理

处理promise 中的异常有两种方式:

* then 方法的第二个参数
* 或者.catch 方法

```js
  <script>
    // 失败 then 方法的第2个参数来接收处理异常
    // request('dbsjabdjsabjdsa')
    //   .then(data => {
    //     console.log('请求成功', data)
    //   }, err => {
    //     console.log('请求失败', err)
    //   })

    // 使用 .catch 方法接收处理异常
    // request('dbsjabdjsabjdsa')
    //   .then(data => {
    //     console.log('请求成功', data)
    //   })
    //   .catch(err => {
    //     console.log('请求失败', err)
    //   })

    request('http://jsonplaceholder.typicode.com/posts')
      .then(data => {
        console.log('请求成功', data)
      })
      .catch(err => {
        console.log('请求失败', err)
      })
      .finally(() => {
        console.log('无论成功或是失败都会执行')
      })
```

## 6. `Async`函数解决回调地狱)

> ​	为了更好的学习 Async 函数，建议参考  http://es6.ruanyifeng.com/#docs/async 

 ES2017 标准引入了 async 函数，使得异步操作变得更加方便。 

### 6.1. 基本用法

我们可以使用 Async-await 来简化获取 Promise 的结果

```js
async function main () {
	// 等待
	const 成员 = await prmose 对象
	// 继续往后执行
}
```

### 6.2. 任何函数都可以使用async

```bash
具名函数
async function main () {}
匿名函数
async function () {}
箭头函数
async () => {}
对象成员函数简写
async hello () {}
```

### 6.3. 返回值 Promise

```html
<body>
  <script>
    // function main() {
    //   return 123
    // }

    // console.log(main())

    async function main () {

      // async 函数始终返回 Promise
      // async 函数的返回值
      // 如果是普通数据，则直接把它包装到 promise 对象中
      // 数据就是 resolve 的结果
      return 123

      // 如果你返回的直接就是一个 promise 对象，则不作任何处理
      // return new Promise((resolve) => {
      //   setTimeout(() => {
      //     resolve(123)
      //   }, 2000)
      // })
    }

    // 通过 then 方法来获取 async 函数的返回值
    // const ret = main()
    // ret.then(data => {
    //   console.log(data)
    // })

    // 获取在另一个 async 中使用 await 来获取
    async function main2() {
      const data = await main()
      console.log(data)
    }

    main2()
  </script>
</body>
```

### 6.4. 异常处理

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <script>
    async function main() {
      // 还是使用 .catch 来处理异常
      // const data = await request('dsanlksas')
      //   .catch(err => {
      //     console.log('请求失败了')
      //   })
      // console.log(data)
      console.log(1)

      // 更推荐使用 try-catch 来捕获异常
      try {
        // try 捕获不到它的异常
        // request('dsabjdsdsa').then(data => {
        //   console.log(data)
        // })
        // JSON.parse('dnsakdnsa')

        console.log(2)
        const data = await request('http://jsonplaceholder.typicode.com/posts')
        console.log(3)
        const data2 = await request('dnsandlksa')
        console.log(4)
      } catch (err) {
        console.log('请求失败了', err)
      }

      console.log(5)
    }


    main()

    function request(url) {
      // 2、在函数中 return 出一个 Promise 对象
      return new Promise((resolve, reject) => {
        // 3、在 Promise 容器中执行异步操作
        // 4、异步操作
        //    成功：resolve
        //    失败：reject
        // 创建请求对象
        var oReq = new XMLHttpRequest();

        // 添加请求回调函数
        // 请求成功，就会自动执行该回调函数
        oReq.addEventListener("load", function () {
          // 获取输出响应结果
          // console.log(this.responseText);

          // 当请求成功了，也就是异步执行结束了，callback 被调用了
          // 我调用的时候，给 callback 传递了一个参数
          // callback(this.responseText)

          // 如果没有数据
          // resolve()

          // 如果有数据
          resolve(this.responseText)

          // 只有这里才能拿到正确的响应结果 responseText
          // return this.responseText
        });

        oReq.addEventListener("error", function (err) {
          // 失败 reject
          reject(err)
        });

        // 设置请求方法和请求路径
        oReq.open("GET", url);

        // 发出请求
        oReq.send();
      })
    }
  </script>
</body>
</html>

```



