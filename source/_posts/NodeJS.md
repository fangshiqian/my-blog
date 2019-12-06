---
title: Node-JS
date: 2019-12-04 09:47:42
top:
categories:
   - 学习
   - Node-JS
tags: Node-JS
---

## Node.js

通俗理解为就是可以脱离浏览器，运行js代码的一个环境

### Node.js基本概念

* 基于chrome v8引擎的javascript运行环境
* 浏览器中有一个可以解析js的解析器
  * 解析器（翻译官）
    * 把编程语言翻译成计算机可以是别的二进制
    * js……（翻译官）→计算机执行
* js运行环境
  * 通过node.js可以直接运行js代码

### Node.js-安装

下载地址：`http://nodejs.org/en/`

### js组成

* 浏览器端
  * ECMAScript:js语法
  * DOM：文档对象模型
    * 约定操作dom元素的语法
  * BOM：浏览器对象模型
    * 操纵浏览器语法
* 服务器端
  * ECMAScript:js基础语法
  * BOM一些常用的api
  * 模块：（类似之前的jQ，swiper……）
    * 内置模块
    * 第三方模块

### Node.js基本使用-REPL(了解)【cmd】

* read eval print loop

* 打开黑窗
* 输入node回车
* 写js代码回车运行
* 循环步骤3

### Node.js基本使用-执行js文件【git bash here】

* 写好一个js文件
* 内部有node.js支持的代码
* 打开黑窗（git bash here）支持的代码
* 输入`node 文件名 `回车
* 运行
* 注意：
  * 文件名不需要打全，写个开头+tab自动提示
  * 黑窗打开位置和js在一个文件夹下
  * 文件名不要叫node.js

### Node.js基本使用-在vscode中打开

* 右键文件→在终端中打开→输入命令运行(`node 文件名`)
* 关闭终端的快捷键 ctrl+~

### Node.js-内置模块

脱离浏览器的限制，通过内置模块可以实现很多在浏览器中干不了的事情

官方文档：`http://nodejs.cn/api/fs.html`

### Node.js-js内置模块基本使用-文件读写操作

文件基本读写会用即可

```js
const fs=require('fs');//导入fs模块
//readFile读取文件
//参数1：文件路径
//参数2：选项 可选参数
//参数3：回调函数
//err:如果读取失败，保存的是错误信息
//data:读取的结果，读取成功的话才有
fs.readFile(path,formdata,fn(err,data){
            if(err==null){
    			console.log(data);//如果没有错误err为null
			}        
 	
  })
  
  
  //writeFile写文件
  //参数1：文件路径
  //参数2：写入的内容
  //参数3：选项 可选参数
  //参数4：回调函数
  fs.writeFile(path,content,formdata,fn(err){
               if(err==null){
      				console.log('写入成功');//err为null,说明文件写入成功
  			}else{
      			console.log('写入失败');
  				}
             })

```

### 终端命令 cd

- 在终端中切换路径
- 可以用来切换路径
- `cd 路径` 切换到指定的目录
- `cd ../` 切换上一级目录
- `cd 文件夹 ` 切换到指定的文件夹
- 到在其他不同级的文件夹下开启终端，可能会引起路径问题
- **在读取文件时，node.js的相对路径，相对的是终端中的路径，小黑窗所处的路径**

### 绝对路径

- 综上所述，引出在读取或者是写入文件时，采用绝对路径定位到这个文件上

- 方式

  - 方式一：右键你要读的文件 复制路径 进行拷贝路径
    - 此方法换到另一个电脑上，还需要更改，因此不方便
  - 方式二：结合两个**全局变量**，可以动态生成绝对路径 避免写死
    - __dirname **js文件所处的文件夹**的绝对路径
    - __filename js文件的绝对路径

- 语法：

  ```js
  //导包
  
  const fs=require('fs');
  //动态获取文件的绝对路径
  const filePath=__dirname+'/novel/01.txt';//此处注意到后面的'./novel/01.txt'不可以这样写 或者不可以'\novel\01.txt',因为\是转义符，所以需要改成'\\novel\\01.txt'
  //读取文件
  fs.readFile(filePath,'utf-8',function(err,data){
      if(err==null){
          console.log(data);
      }
  })
  ```

  

  

  

### Path内置模块的基本使用

- 综上所述，虽然读取文件变得动态，但是书写格式方面，还是让人不省心，于是就有了此模块的作用

- 专门用来处理路径的模块

- 方法：

  - path.extname('info/novel.txt');获取文件的扩展名 .txt
  - path.dirname('info/novel.txt');获取文件夹的名字 info
  - **path.join(路径1，路径2，路径3……)；**//把多个路径拼接到一起，保证格式正确,**逗号分隔**

  ```js
  const filePath=path.join('info','./novel','01.txt')
  //此时，生成一个绝对路径
  path.join(__dirname,'./novel/01.txt');
  ```

### path与js结合获取文件

* 语法：

  ```js
  //导入js包
  const fs=require('fs');
  //导入path包
  const path=require('path');
  var filePath=path.join(__dirname,'./novel/01.txt');
  fs.readFile(filePath,'utf-8',function(err,data){
      if(err==null){
          console.log(data);
      }
  })
  ```

### http模块-创建服务器

* 使用步骤：

  ```js
  //导包
  const http=require('http');
  //调用createServer方法创建服务器对象
  var server=http.createServer(function(request,response){
      
      //❀响应❀返回内容为中文时，会出现乱码效果，需要设置格式
      //content-type 内容类型
      //text/plain 是普通文本
      //charset=utf-8 编码格式
      response.setHeader('content-type','text/plain;charset=utf-8');
      //返回内容
      response.end('欢迎访问服务器');
  })
  //开启服务器（监听端口） listen
  //参数1 端口号
  //参数2 监听地址省略的话就是本机 该处已省略
  //参数3 开启之后的回调函数
  server.listen(1888,function(res){
      if(err==null){
          console.log('服务器开启成功');
      }else{
          console.log('服务器开启失败');
      }
  })
  ```

* 让电脑成为服务器

* `http://192.168.156.91:1888`

* 协议：ip地址:端口号

* 端口：

  * 电脑和外部通讯的一个通道
  * 物理端口
    * usb口
    * 网线口
    * 耳机口
    * hdmi(显示器，投影仪)
    * ……
  * 虚拟端口：电脑中的软件和外部通讯的通道
    * 只要和外部通讯的软件，都会使用某一个虚拟端口
    * 一个号位移 0开始递增
    * 虚拟端口很多
    * 但是前10000很多被用了
    * 自己使用时用10000以后，靠后一般都可以使用 一些比较另类
    * 6.8848 8888 4399 3000
    * 端口一次只能被一个程序使用

### http模块-服务器的交互流程

* 语法：

  ```js
  const http=require('http');
  const server=http.createServer(function(request,response){
      //request.url获取请求的地址
      //decodeURI对❀请求地址❀ url进行中文解码
      //console.log(decodeURI(request.url))；
      //response.end('笑');
      response.setHeader('content-type','text/plain;charset=utf-8');
      const requestUrl=decodeURI(request.url);
      if(requestUrl=='/hello'){
          response.end('吃了没')
      }else if(requestUrl=='/饿了么'){
          response.end('知道了');
      }else if(requestUrl=='login'){
          response.end('<h1 style="background:orange;color:skyblue;">我在</h1>');
      }
  });
  server.listen(1888,function(err){
      if(err==null){
          console.log('成功！');
      }
  })
  
  
  
  ```

### http模块-根据不同的url响应html文件

* 语法：

  ```js
  //导包 http
  const http=require('http');
  //导包 fs
  const fs=require('fs');
  //导包 path
  const path=require('path');
  //创建服务器
  const server=http.createServer((request,response){
  	const filePath=path.join(__dirname,'./web/index.html');
  fs.readFile(filePath,'utf-8',(err,data)=>{
      if(err==null){
          response.end(data);
      }
  })
  })
  //开启监听
  server.listen(1888,err=>{
      if(err==null){
          console.log('成功');
      }else{
          console.log('失败');
      }
  })
  ```



### http模块-根据不同的url响应不同的文件

* 语法：

  ```js
  const http=require('http');
  const fs=require('fs');
  const path=require('path');
  //创建一个叫静态资源服务器
  http.createServer((request,response)=>{
      var requestUrl=decodeURI(request.url);
     
      var fullPath=path.join(__dirname,'./web'+requestUrl);
      //fs.readFile(fullPath,'utf-8',(err,data)=>{
      //浏览器可以自动识别绝大多数的文件格式，不需要人为设置编码
      fs.readFile(fullPath,(err,data)=>{
          if(err==null){
              response.end(data);
          }else{
              response.setHeader('content-type','text/plain;charset=utf-8');
              response.end('<h1>404</h1>');
          }
      })
  })
  ```


###  http模块-get和post请求

* `request.method`获取请求的方法

* 语法：

  ```js
  //导包
  const http=require('http');
  //创建服务器
  const server=http.createServer((request,response)=>{
      if(request.method=='GET'){
          if(request.url=='/list'){
              //list相关逻辑代码
          }else if(request.url=='/search'){
              //search相关逻辑代码
          }else{
          	response.end('为get请求')
              
          }
      }else if(request.method=='POST'){
          if(request.url=='/add'){
              //add相关逻辑代码
              
          }else{
          response.end('为post请求');
              
          }
      }
  })
  server.listen(8848,err=>{
      if(!err){
          console.log('开启成功');
      }
  })
  
  ```

  



###　Node.js-第三方模块（npm网站）

* 步骤：一顿ctrl+c/ctrl+v

  * 官方网站（包管家搜索界面）`http://www.npmjs.com`

  * 找包 官方的包检索网站 npm

  * 下包 模板的网页中有命令

    * 在终端中输入npm i szhmqd23_yu

    * 当前文件夹中会出现如下图所示

    ![1572008813226](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1572008813226.png)

  * 导包 文档中也有

  * 用包

  ```js
  // 导包
  const szhmqd23_yu = require('szhmqd23_yu');
  // 用包
  // const res=szhmqd23_yu.add(998,2);
  
  const res=szhmqd23_yu.mul(998,2);
  console.log(res);
  
  // console.log(szhmqd23_yu.mul(1,2))
  // console.log(szhmqd23_yu.sub(1,2))
  
  ```

* 第三方插件使用步骤

  * 新建文件夹（不要写中文）
  * 初始化(打开终端输`pm init -y`或`pm init 自行输入`
    * 生成一个package.json文件
    * 保存项目的信息，比如版本，名字，使用的第三方模块
    * `npm init 自行输入每一项`(初期用的不多)
  * 去npm网站找包
  * 根据提示下包`npm i 包名`
    * package.json中增加一个dependencies把下载的包名，记录进去，和版本信息
    * 文件夹下多
      * node_modules所有下载的第三方模块都会在里面
      * package-lock.json:模块名，版本号，在线地址等
        * 为了让我们第二次下载的时候速度更快
  * 根据提示导包
  * 根据提示用包

* 第二次下载

  * 保证package.json及package-lock.json中有之前下载的模块名
  * 直接输入npm i 自动读取用到的模块并下载

### express模块基本使用

相比于原生http木块 开发速度更快的web开发框架

很多模板框架都是基于express

* 使用步骤

  * 新建文件夹，非中文

  * 初始化`npm init -y`

  * 找包

  * 根据提示下包`npm i express`

  * 导入express

    ```js
    //导包 express
    const express=require('express');
    //创建服务器对象 http.createServer类似
    const app=express();
    //如果请求的是/ (url为空)
    app.get('/',(request,response)=>{
        //原生方法也支持
        response.send('hello world');
    })
    //开启服务器
    app.listen(3000,err=>{
        if(!err){
            console.log('success');
        }
    })
    
    ```

    

  * 根据提示用包

    * http模块的方法都可以使用，更建议用express

### express-托管静态资源

* 语法:

  ```js
  //导包
  const express=require('express');
  //创建服务器
  const app=express();
  //实现静态资源服务器的功能
  app.use(express.static('./public'));//相当于原生中的根据不同的url地址访问不同的文件
  //开启服务器
  app.listen(3000,err=>{
      if(!err){
          console.log('success');
      }
  })
  
  ```

### express模块-get路由

* get请求时，url地址和后台函数（逻辑）的对应关系
* 接口调用：浏览器调用定义在服务器的函数
* 写接口：
  * 根据接口文档注册路由
  * 实现逻辑
  * 返回结果

### 一条笑话接口

* 语法:

  ```js
  //导包
  const express=require('express');
  //创建服务器
  const app=express();
  //注册路由
  app.get('/joke',(request,response)=>{
      //一条笑话
      response.send('我是一条笑话');
  })
  //开启服务器
  app.listen(8848,err=>{
      if(!err){
          console.log('成功');
      }
  })
  
  ```

  



### 随机笑话接口

* 语法：

  ```js
  const express=require('express');
  const app=express();
  app.get('/randomJoke',(request,response)=>{
      const jokes=['笑话1','笑话2'];
      const randomIndex=parseInt(Math.random()*jokes.length);
  })
  app.listen(3000)
  
  ```

### 高级版随机笑话接口

* 语法：

  ```js
  const express=require('express');
  const fs=require('fs');
  const path=require('path');
  const app=express();
  //注册路由
  app.get('/randomJokePro',(request,response)=>{
      const fullPath=path.join(__dirname,+'./data/jokes.json');
      fs.readFile(fullPath,(err,data)=>{
          if(err==null){
              const jokesArr=JSON.parse(data);
              const randomIndex=parseInt(Math.random()*jokesArr.length);
              response.send(jokesArr[randomIndex]);
          }else{
              response.setHeader('content-type','text/plain;charset=utf-8');
              response.send('404 服务器崩溃');
          }
      })
  })
  app.listen(3000);
  
  ```




### get请求参数获取

* 通过`request.query`属性进行获取

* 语法：

  ```js
  const express=require('express');
  const app=express();
  app.get('/search',(request,response)=>{
      console.log(request.query)；
      console.log(request.query.name);//获取name属性
      response.send('/search');
  })
  app.listen(3000,err=>{
      if(!err)
      {
          console.log('success');
      }
  })
  
  ```

### 笑话接口带参数

* 语法：

  ```js
  const express=require('express');
  const fs=require('fs');
  const path=require('path');
  const app=express();
  app.get('/getSomeJoke',(request,response)=>{
      const num=request.query.num;
      const jokeArr=[];
      const fullPath=path.join(__dirname,'./data/jokes.json');
      if(num<=490){
          	fs.readFile(fullPath,(err,data)=>{
          if(err==null){
              const jokes=JSON.parse(data);
          	for(let i=0;i<num;i++){
          	const randomIndex=parseInt(Math.random()*jokes.length);
             	jokeArr.push(jokes[randomIndex]);
      		}
              response.send({
                  num,
                  msg:'获取成功',
                  jokes:jokeArr
              });
          }else{
              //读取失败
              response.send({
                  msg:'文件读取失败'
              })
          }
      })
      
     
      } else{
          response.send('没有那么多');
      }
      
  })
  app.listen(3000,err=>{
      if(!err){
          console.log('success');
      }
  });
  
  ```



### post路由

* post请求，url和后台函数的对应关系

* 注册的方法和get类似

* 直接通过浏览器的url访问发送时get

* 可以通过postman发请求

  * 注意
    * get
      * 参数写在param
    * post
      * 参数写在body中
      * 有文件上传选中form-data,没有文件上传选中x-form-urlencoded

* 自己写ajax设置请求的type为post

* 默认注册的post路由中，无法获取到提交过来的参数

* 语法：

  ```js
  const express=require('express');
  const app=express();
  app.post('/add',(request,response)=>{
      response.send('我是post请求');
  })
  app.listen(3000)
  
  ```



### post数据获取（普通文本）

* `中间件`获取post提交的文本数据`request.body`

* 中间件是一个特殊第三方模块

* 必须结合express才可以使用

* `http://www.npmjs.com/package/body-parser`

* 语法：

  ```js
  const express=require('express');
  const bodyParser=require('body-parser');
  const app=express();
  app.use(bodyParser.urlencoded({extended:false}));
  app.post('/checkUsername',(request,response)=>{
      const username=request.body.name;
      const userArr=['黑寡妇','绿巨人','金刚','葫芦娃'];
      //判断是否注册过
    //indexof判断数组中元素的索引，存在返回索引，不存在返回-1
      if(userArr.indexof(username)==-1){
          response.send({
              msg:'恭喜你，可以注册',
              code:200
          })
      }else{
          response.send({
              msg:'很遗憾，已被注册',
              code:400
          })
      }
      //some传入一个回调函数
      //参数1：数组中的每一项
      //参数2：索引
      //内部返回一个布尔值，任意一个为true,
  })
  app.listen(3000)
  
  ```




### post数据获取（文件上传）

* 需要中间件`request.files`

* `http://npmjs.com/package/express-fileupload`

* `request.files` 保存所有文件信息

* `request.files.xxx`获取key为xxx的文件信息

* `request.files.xxx.mv(路径，回调函数)把文件移动到某个地方`

* 语法：

  ```js
  const express=require('express');
  const path=require('path');
  const fileUpload=require('express-fileUpload');
  const app=express();
  app.use(fileUpload());
  app.post('/upload',(request,response)=>{
      //icon属性的文件名
      const filename=request.files.icon.name;
      const filePath=path.join(__dirname,'./files',filename);
      request.files.icon.mv(filePath,err=>{
          if(!err){
              console.log('上传成功');
          }
      })
      response.send('/upload');
  })
  app.listen(3000)
  
  ```

  

  

  

  

  

### 中间件

* 就是一个特殊的第三方插件
* 依赖于express
* 中间件是请求和响应之间额外注册的毁掉含糊
* request和response是`共享`的
* 中间件中为request对象额外添加属性
* 在后续的回调函数中可以获取到
* 中间件可以增加任意个
* next如果不调用，卡住，浏览器接收不到数据
* 请求---回调函数1（中间件）--回调函数2（中间件）-->响应
* 执行的顺寻从上到下依次执行
* 编写的位置`路由的前面`



### node.js模块化-自己写第三方模块

* http://commonjs.org

* 导入模块`require()`

* 导出模块module.exports()

* 语法：

  ```js
  //自己写的第三方模块
  const name='niubi',
        module.exports={
            name,
            sayHi(){
                console.log('nice to meet you')；
            }
        }
  
  //使用自己写的第三方模块
  const useniubiModule=require('./niubi.js');
  console.log(useniubiModule);
  useniubiModule.sayHi();
  
  ```

* 注意：

  * 导入模块require
  * 自己的模块写路径
  * `js可以省略`
  * 模块暴露module.exports
  * 类似自调用函数底部window.xxx=值
  * 暴露多个，用对象方式
  * 重复module.exports赋值会把前面的覆盖掉
  * 抽取模块不需要运行
  * 导入的时候内部代码会自动解析
  * module是关键字，全局变量
  * 要用哪个属性，就点哪个属性

### 自己写的计算器模块

* 语法：

  ```js
  //自己写的模块
  function add (num1,num2){
      return num1+num2;
  }
  function sub(num1,num2){
      return num1-num2;
  }
  function mul(num1,num2){
      return num1*num2
  }
  function divi(num1,num2){
      return num1/num2;
  }
  module.exports={
      add,
      sub,
      mul,
      divi,
  }
  //调用自己写的第三方模块
  const computer=require('./commputer');
  const res=computer.add(5,5);
  console.log(res);
  
  ```

### 通过自己写中间件设置跨域

* 语法：

  ```js
  //自己写模块实现设置允许跨域
  module.exports=(request,response,next)=>{
      response.header('Access-Control-Allow-Origin','*');
      next();
  }
  
  //使用中间件设置允许跨域
  const express=require('express');
  const myModule=require('./myModule');
  const app=express();
  
  app.use(myModule);
  
  ```



### 常见文件夹名

* utils自己抽取功能模块
* libs下载的第三方模块（自己手动下载的）
* node_modules:npm i模块名 自己手动下载的文件夹 内部保存了第三方模块
* static:静态资源 html css js
* public公共文件（静态资源）
* web页面（静态）



### 跨域

* `ajax`请求`不同源`的接口时候出现
* 浏览器为了保护我们帮我们做的一件事情
* 当`浏览器`打开页面，和调用的`接口`需要同源才可以调用



### 浏览器的同源

* url地址的组成：http://127.0.0.1:3000/list
  * 协议：http://
  * 地址：127.0.0.1
  * 端口：3000
* 同源：
  * 浏览器打开的页面地址`http://127.0.0.1:5500/02-cross-origin/index.html`
  * 页面ajax调用接口请求的地址`http://127.0.0.1:3000/list`
  * 协议：地址，端口全部相同，称之为`同源`
    * 如果页面的地址和接口地址同源，浏览器就不会做任何的限制
    * 可以自由访问
  * 协议，地址，端口任何一个不相同，称之为`不同源`
    * 浏览器是禁止访问的
  * 实际工作中，不可避免的页面地址和接口地址绝对同源
    * 常用的两种解决方案
      * jsonp:曾经最多，现在越来越少，面试经常问
      * cors：目前用的最多的
  * 往不同源的接口发送请求：跨域

### 跨域方案-jsonp

* 民间的解决方案

* 实验一方式：

  * 前端：

    ```js
    $.ajax({
        url:,
        type:'get',//必须是get
        dataType:'jsonp',//需要设置
        success:function(backData){},
    })
    
    ```

  * 后端

    ```js
    response.jsonp({key:value,key1:value1})
    
    ```

* 语法：

  ```js
  const express=require('express');
  const app=express();
  app.get('/list',(request,response)=>{
      response.jsonp({
          msg:'jsonp测试',
          
      })
  })
  app.listen(3000)
  
  
  
  ```

  ![1572269989348](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1572269989348.png)

* jsonp原理：

  * script标签的src属性可以发送请求，同时没有同源限制
  * 和Ajax一点关系没有
    * 到netWork中选中xhr分类，什么都看不到
  * 本质是动态创建了一个script标签添加到页面的顶部
    * src设置的：接口地址+发送的数据+callback=xxx
  * 请求成功之后会被自动移除
  * 服务器返回：函数的调用，函数名({对象})
  * 内容返回到浏览器会被解析为js,调用定义好的函数，传入参数jquery的jsonp

* 自己模拟的jsonp实现过程

  ```html
  <script>
      function doSomething(backData){
          console.log(backData);
      }
  </script>
  <script src="http://192.168.156.91:3000/jsonpApi?callback=doSomething">
  	//函数的调用
     
  </script>
  
  ```

  

* 缺点：

  * 不支持post请求
  * 数据大的话，搞不定，文件上传也搞不定

* 优点：

  * 兼容性超级好

### 跨域方案-CORS

* CORS：

  * cross :跨
  * origin:域
  * resource:资源
  * sharing:共享

* html5中推出的新标准，低版本浏览器不支持ie

* 前端：什么事情也不用做

* 后端：设置允许跨域

  * 在响应数据之前设置允许header
  * `response.header('Access-Control-Allow-Origin','*')`

* CORS原理：

  * 浏览器能够识别('Access-Control-Allow-Origin','*')这个header
  * 请求发给服务器之后
  * 服务器翻译的响应头中有一个允许标记
  * 浏览器人为服务器运行跨域访问，没有了跨域错误

* 缺点：

  * 兼容性较jsonp差
  * 微软已经放弃了xp,ie5,ie6基本没人使用

* 优点：

  * get和post都支持
  * 前端什么也不用干

  ```js
  const express=require('express');
  const app=express();
  app.post('/add',(request,response)=>{
      response.header('Access-Control-Allow-Origin','*');
      response.send('/add');
  })
  app.listen(3000)
  
  ```

### 中间件设置跨域

* 请求和响应之间额外注册的一个回调函数

* 在这个回调函数中统一设置允许跨域的那个头

* 每次进行ajax请求接口，会先request,然后执行中间件的会调函数，最后执行response

* 语法：

  ```js
  app.use((request,response,next)=>{
      //设置允许跨域
      response.header('Acccess-Control-Allow-Origin','*');
      //调用next
      next();
  })
  
  ```

  





### -补充vscode主题变色

* 下载扩展Dark-Material

### nodemon-自动重新运行

* node的一个全局模块
* 当做一个没有图像化界面的软件
* 安装之后可以自动检测文件修改，自动重新运行
* 任意位置执行 `npm i nodemon -g`
* 安装完毕之后
  * node xxx 换成nodemon xxx





## ES6-基本概念

* 2015年推出新的语法规范ECMAScript

### ES6-let

* 变量声明

* 与var比较：

  * 没有变量提升
  * 有块级作用域
  * 不能重复声明（但是可以重新赋值）
  * 替代var
  * 别再写var 用let

* 语法：

  ```js
  let 变量名=值
  
  //基本使用
  let name='jack';
  console.log(name);//jack
  
  //重新赋值
  name='rose';//可以的
  
  //变量声明不能提升
  console.log(name);//报错
  let name='jack'
  
  //块级作用域
  {
      let skill='跳舞';
  }
  console.log(skill);//报错
  
  
  //不能重新声明
  let skill='不如跳舞';
  let skill='跳什么';
  console.log(skill);//报错
  
  
  
  ```

### ES6-const

* 常量声明

* 与var比较：

  * 没有变量提升
  * 有块级作用域
  * 不能重复声明（一般不能重复赋值）
  * 必须声明时赋值
  * 能用const 不用let 能用let不用var
  * 声明之后不能改

* 语法：

  ```js
  //基本使用
  const friend='乌索普';
  console.log(friend);//乌索普
  
  //变量不能提升
  console.log(friend);
  const friend='jack';
  
  //有块级作用域
  {
      const friend='jack';
  }
  console.log(friend);//报错
  
  //不能重复	声明
  const vegetable='西兰花';
  const vegetable='westblueflower';//报错
  
  //不能修改
  const vegetable='西兰花';
  vegetable='westblueflower';
  
  //必须声明时赋值
  const vegetable;//报错
  
  
  
  ```

### ES6-对象的属性和方法简化写法

* 更简单的属性赋值：

* 前提：`属性名和值的名字相同`

  ```js
  const name='jack';
  const person={
      //属性名和值的名字相同
      //name:name 原来的写法
      name,//ES6写法
      //jump:function(){
          
      //}
      //ES6写法
      jump(){
          
      }
  }
  
  ```

### ES-6-模板字符串

* 轻量级的模板引擎，原生支持，不用导包

* 定义的时候使用`

* 挖坑的语法${表达式}

* 坑中必须有东西

* 可以换行 简单模板生成直接使用 模板字符串即可

* 复杂的还是模板引擎

* 语法：

  ```js
  const smoke='黑烟';
  const data={
      name:'李白',
      dynasty:'唐'
  };
  const temStr=`
  	望庐山瀑布 ${data.name} 来自于{data.dynasty}
  日照香炉生${smoke}
  遥看瀑布挂前川
  `;
  console.log(temStr);
  
  
  ```

* 与模板引擎区别是：对象调用省略对象(分情况，有时候嵌套的内部也是对象还是需要对象.属性名)

  ```html
  <div>
      {{$value}}
  </div>
  
  ```

### 知识点一

* 输入node回车 按两次ctrl+c，退出
* 对象的属性和方法获取语法：还是对象.属性或者对象.方法()
* 模板字符串的使用

### ES6-函数默认值

* 早期函数不传递参数，参数有一个默认值是undefined

* 早期通过短路运算，实现默认值的设置

  ```js
  function sayHi(name,skill)
  {
      name=name||'路飞';
      skill=skill||'橡胶果实';
  }
  sayHi();
  
  ```

  

* ES6中的默认值

* 语法：

  ```js
  function sayHi(name='路飞',skill='橡胶果实')
  {
      console.log(name,skill);
  }
  sayHi();//路飞 橡胶果实
  sayHi('索隆','迷路');//索隆 迷路
  
  ```

### ES6-对象解构

* 更方便的对象属性取值

* 语法：

  ```js
  const person={
      name:'时间之灵',
      desc:'美食',
      spec:'食物好吃'
  };
  //之前获取方式
  const name=person.name;
  const desc=person.desc;
  const spec=person.spec;	
  
  //ES6简写
  //快速获取对象的属性
  //需要和对象的属性名相同
  const {name,desc,spec}=person;
  //没有返回undefined
  const {skill}=person;
  
  ```

  

  

### ES6-对象解构实际应用

#### 结合函数用

* 函数的参数进行结构

* 提示

* 实际调用时会更多的提示

* 语法：

  ```js
  function getFoods(food1,food2,food3,food4){
      
  }
  //ES6写法：
  function getFoods({food1,food2,food3,food4}){
      
  }
  getFoods({
      food1:'西兰花炒蛋',
      food2:'西红柿炒蛋',
      food3:'猪肉炒蛋',
      food4:'蛋炒西兰花'
  });
  
  ```

  

#### 函数参数解构结合默认值

* 结合默认值

* 语法：

  ```js
  function getFoods({food1='西兰花炒蛋',food2='蛋炒饭'}){
      
  }
  getFoods({});//不传使用默认值
  getFoods({
      food2:'黄瓜炒鸡蛋'
  });
  
  ```

### ES6-数组解构

* 获取顺序和数组元素对应关系一致

* 数组大部分时候都是通过下标获取某一个

* 数组的结果用的不多，了解即可

* 语法：

  ```js
  const cartoonArr=['喜羊羊','葫芦娃','灰太狼','天线宝宝'];
  //取值
  const c1=cartoonArr[0];
  const c2=cartoonArr[1];
  console.log(c1,c2);
  
  //ES6取值
  const [c1,c2,c3,c4]=cartoonArr;
  
  
  ```

### ES6-对象展开

* 结合对象使用

* `写在前面的同名的属性会被覆盖`

* 语法：

  ```js
  const person={
      skill:'跳水',
      hobby:'抗冻'
  };
  const student={
      skill:'学习',
      hobby:'学习使我快乐',
      sleep:'呼噜噜'
  };
  const son={
      //写在前面的同名的属性会被覆盖
      skill:'游泳',
      ...person,
  };
  console.log(son.skill);//跳水
  
  
  ```

### ES6-数组展开

* 结合数组使用

* `一直在后面追加`

* `数组不会出现覆盖问题，索引依次靠后`

* 语法：

  ```js
  const vegetable=['西兰花','西红柿','苦瓜','黄瓜'];
  const meats=['牛肉','羊肉','冷鲜肉'];
  const foods=[...vegetable,...meats];
  
  ```

### ES6-箭头函数

* 箭头函数书写步骤：

  * 省略function 变为=>
  * 如果形参只有一个，可以省略小括号
  * 如果函数体只有一行，可以省略大括号
  * 如果函数体只有一行，并且有返回值
    * 省略大括号的同时，必须省略return

* 语法：

  ```js
  //函数 无参数 无返回值的函数
  const func1=function(){
      console.log('函数');
  }
  //ES6写法:
  const func1=()=>console.log('函数');
  
  //有一个参数 无返回值的函数
  const func2=function(name){
      console.log(name+'你好吗');
  }
  func2('刘晓慧');;
  //ES6写法：
  const func2=name=>console.log(name+'你好吗');
  
  //有一个参数 有一个返回值
  const func3=function(name){
      return name+'奥哈有';
  }
  //ES6写法：
  const func3=name=>name+'奥哈有';
  var res=func3('我是');
  console.log(res);
  
  //参数有多个 函数体有多行的函数
  const func4=function(name,age){
      console.log('孤独的天才');
      console.log(name+'是吗'+age);
  }
  
  //ES6写法
  const func4=(name,age)=>{
      console.log('孤独的天才');
      console.log(name+'是吗'+age);
  }
  
  ```

### ES6-箭头函数中的this

* 箭头函数中的this，在创建时就确定了，是上下文（和他平级的环境中）的this

* 可以通过babel的工具把高级的js代码翻译成低版本的js,查看内部的代码实现的细节

* babel传送门（babeljs.cn）

* 语法：

  ```js
  const person={
      name:'海尔兄弟',
      skill:'抗冻',
      jump(){
          console.log(this);//调用者是谁this就是谁
          const _this=this;
          //window.setTimeout(function(){
            //  console.log(this);//window
            //  console.log(_this);//老方法 _this的jump方法当前调用者是谁_this就是谁
         // })
          
          window.setTimeout(()=>{
              console.log(this);//是当前调用jump的调用者
          })
      }
  };
  person.jump();
  
  ```

  

## 终端

* 多个终端区别：
  * 终端可以理解为是一个没有界面的软件
  * 通过输入内容让他干什么事
  * cmd 微软 早期推出 功能最少 不太好用
  * git bash here 安装git之后 自带 功能强大 支持很多cmd没有命令 linux的命令也基本上都支持
  * power shell微软后续推出的一个终端，功能牛逼很多，但是还是比git bash here支持的命令少一些



## Mysql-数据库

* 分类
  * 关系型数据库
    * 类似于table表格的形式保存数据
    * 使用sql的语句操纵数据
    * 常见的有mysql,oracle,mssql……
  * 非关系型数据库
    * 类似于js对象的形式保存数据
    * 操纵对象的形式操纵数据
    * 常见的有：Mongodb,Redis……
* 数据库管理员：DBA
* 数据库服务器



### 数据库-基本使用

* 建库
* 建表
* 建字段

### sql语句-增

```sql
insert into 表名(字段1，字段2……) values(值1，值2，……)


```



### sql语句-删

```sql
delete from 表名 where 条件
delete from 表名 where id=3 删除一条
delete from 表名 where id>3 删除一定范围
delete from 表名 where 不跟条件全部删除
必须给条件，否则全部删除

```



### sql语句-改

```sql
update 表名 set 字段1=值1，字段2=值2…… where条件
update 表名 set username='赵四',skill='跳舞' where id=2;
update 表名 set username='赵四',skill='跳跳舞' where id>3
update 表名 set username='赵四',skill='跳舞'
条件不给 全部更改

```



### sql语句-查

```sql
select * from 表名 where 条件
//精确查询
select * from user where id=2;
//范围查询
select * from user where id>2
//全部查询
select * from user

```



### mysql模块使用

* `http://www.npmjs.com/package/mysql`

* 语法：

  ```js
  //导包
  const mysql=require('mysql');
  //设置数据库的连接信息
  const connection=mysql.createConnection({
      //地址
      host:'localhost',
      //用户名
      user:'root',
      //密码
      password:'root',
      //库的名字
      database:'db88'
  })
  //链接数据库
  connection.connect();
  //参数1：执行的sql语句
  //参数2 执行完毕的回调函数
  connection.query('select * from user',function(error,results,fields){
      //错误信息 如果有的话
      //执行的结果
      //表示的字段信息 用的不多
  })
  //关闭数据库连接
  connection.end();
  
  ```





### mysql-ithm模块使用

* `http://www.npmjs.com/package/mysql-ithm`

* 语法：

  ```js
  //导入模块
  const mysql=require('mysql');
  const hm=require('mysql-ithm');
  //连接数据库
  //如果数据库存在则连接，不存在则自动创建数据库
  hm.connect({
      host:'localhost',
      port:'3306',
      user:'root',
      password:'root',
      database:'hm',
  })
  //创建Model(表格模型，负责增删改查)
  //表格名字叫student
  let studentModel = hm.model('student',{
      // 字段
      name:String,
      age:Number,
      // 技能
      skill:String,
  });
  
  //4.调用API 添加数据
  studentModel.insert({name:'面向对象'，age:18,skill:'创建对象'},(err,results)=>{
      console.log(err);//错误信息
      console.log(results)//结果
  })
  //数据查询
  studentModel.find((err,results)=>{
      console.log(results);
  })
  //数据修改
  studentModel.update({name:'李四'},(err,results)=>{
      console.log(results);
  })
  //数据删除
  studentModel.delete((err,results)=>{
      console.log(results);
  })
  
  
  
  
  ```

  > 小知识：截图神器：传送门 http://www.snipaste.com
  >
  > * 取色：F1截取 按c取色 按shift切换颜色格式
  > * 改粗细 滚轮 1,2
  > * 还原截图：f3
  > * 订图：开始普及

## chrome允许跨域

详情请参考网址：https://www.cnblogs.com/laden666666/p/5544572.html



## 英雄管理项目

### 项目说明

* 开发方式：
  * 后端：
    * 照着接口文档
    * 写接口，接收数据，接收文件，增删改查数据库，翻译结果
  * 前端：
    * 写静态
    * 照着接口文档
    * 调接口

### 接口文档

* 基地址：http://127.0.0.1:3000
* 状态码：
  * 200 请求成功
  * 401 用户名已存在或用户名错误
  * 402 密码错误或验证码错误
  * 500 服务器内部错误
  * 302 服务器重定向

### 项目初始化

步骤:

> 1.新建文件夹：heroManage
>
> 2.在文件夹中打开终端 `npm init -y`
>
> 3.创建index.js
>
> 4.下包 `npm i express`  `npm i mysql-ithm mysql`
>
> 5.c+v express的基本结构
>
> 6.c+v 今天要写的路由
>
> 7.为了后续观察数据，此处英雄列表采用随机数据生成，后面一一介绍
>
> 8.创建两个表，分别是hero和user两张表



```js
const express = require('express')
const app = express()
//1.导入模块
const mysql = require('mysql');
const hm = require('mysql-ithm');
const Mock = require('mockjs')
const bodyParser = require('body-parser')
const fileUpload = require('express-fileupload');
const path = require('path');
const svgCaptcha = require('svg-captcha');
var session = require('express-session')

app.use(express.static('./web'));
app.use(express.static('./uploads'));
app.use(bodyParser.urlencoded({ extended: false }));
app.use(fileUpload());
app.use(session({
    secret: 'keyboard cat',
    resave: false,
    saveUninitialized: true,
  }))
app.use('/hero/*',(req,res,next)=>{
    if(!req.session.userInfo)
    {
        res.send({
            code:500,
            msg:'没有凭证'
        })
    }else{
        next();
    }
})
//2.连接数据库
//如果数据库存在则连接，不存在则会自动创建数据库
hm.connect({
    host: 'localhost',//数据库地址
    port: '3306',
    user: 'root',//用户名，没有可不填
    password: 'root',//密码，没有可不填
    database: 'herolast'//数据库名称
});

//3.创建Model(表格模型：负责增删改查)
//如果table表格存在则连接，不存在则自动创建
let heroModel = hm.model('hero', {
    name: String,
    skill: String,
    icon: String
});
let userModel = hm.model('user', {
    username: String,
    password: String,
});
let captchaText='';
app.get('/user/captcha', function (req, res) {
    const captcha = svgCaptcha.create();
    // req.session.captcha = captcha.text;
    captchaText=captcha.text;
    console.log(captchaText);
    
    
    res.type('svg');
    res.status(200).send(captcha.data);
});





app.listen(3000, err => {
    if (!err) {
        console.log('success');
    }
})

```



### 英雄列表

| 接口名称   | 接口类型 | 接口参数 | 返回数据          |
| :--------- | :------: | -------- | ----------------- |
| /hero/list |   get    | 无       | {hero:[英雄列表]} |

* 查询所有数据 heroModel.find()，查询完毕之后返回的是数组

* 通过判断查询过来的数据，进行渲染到页面上

  ```js
  app.get('/hero/list', (req, res) => {
  
      heroModel.find((err, results) => {
          // console.log(results);
          if (!err) {
              if (results.length == 0) {
                  res.send({
                      msg: '目前没有什么消息，等待更新',
                  })
              } else {
                  res.send({
                      code: 200,
                      hero: results,
                  })
              }
          } else {
              res.send({
                  code: 500,
                  msg: '服务器内部错误',
              })
          }
      });
  
      // res.send('/hero/lis');
  });
  
  ```

  

### 查询英雄详情

* 点击详情按钮进行显示获取该英雄的详细信息

  

| 接口名称   | 接口类型 | 接口参数 | 返回数据          |
| :--------- | :------: | -------- | ----------------- |
| /hero/info |          | 无       | {hero:[英雄列表]} |



* 通过点击编辑按钮，进行跳转到编辑页面，为了获取指定英雄的详细信息，进行设置`url传递参数?id=id值`
* 接口中获取get传递的参数，通过`req.query.id`进行获取传递的参数
* 前端：进入编辑页面，因为后面的编辑接口还需要传递当前修改的英雄信息的id,所以还需要把id存在一个隐藏域里，作为参数进行上传，以免报错

```js
// 指定英雄详情
app.get('/hero/info', (req, res) => {
    const id = req.query.id;
    console.log(id);
    heroModel.find(`id=${id}`, (err, results) => {
        if (!err) {

            if (results.length != 0) {
                res.send({
                    code: 200,
                    data: results[0],
                })
            } else {
                res.send({
                    msg: '你这输入的是啥，完全不懂！'
                })
            }

        } else {
            res.send({
                code: 500,
                msg: '不是我的错'
            })
        }
    })

})

```



### 新增英雄

步骤：

> 1.因为涉及到数据主动提交及文件的上传，需要进行下包
>
> 2.终端输入`npm i body-parser express-fileupload`
>
> 3.对应代码进行c+v
>
> 4.因为涉及到文件的上传，所以需要定义一个文件夹用来存储你上传的文件`uploads`
>
> 5.数据库更新heroModel.insert()



| 接口名称  | 接口类型 | 接口参数 | 返回数据                  |
| :-------- | :------: | -------- | ------------------------- |
| /hero/add |   post   | formdata | {code:200,msg:'新增成功'} |

* post获取数据

  * 文本通过req.body.username
  * 文件通过req.files.icon.name

* 前端：注意调用接口的时候，设置`processData:false,contentType:false`

* 前端：注意上传的表单的name属性和接口接收的参数的名称一致，以免造成错误

* 文件上传成功后进行移动`req.files.icon.mv(path.join(__dirname,icon),(err))`

  

```js
// 新增英雄
app.post('/hero/add', (req, res) => {
    const name = req.body.name;
    const skill = req.body.skill;
    console.log(req.files);

    const icon = req.files.icon.name;
    console.log(icon);

    req.files.icon.mv(path.join(__dirname, './uploads', icon), err => {
        if (!err) {
            console.log('上传成功！');

        }
    })
    heroModel.insert({ name, skill, icon }, (err, results) => {
        if (!err) {
            res.send({
                code: 200,
                msg: '新增成功！'
            })
        } else {
            res.send({
                code: 500,
                msg: '不是我的错'
            })
        }
    })


})




```



### 英雄删除



| 接口名称     | 接口类型 | 接口参数 | 返回数据                  |
| :----------- | :------: | -------- | ------------------------- |
| /hero/delete |   post   | id       | {code:200,msg:'删除成功'} |

* 传递的参数id,在一开始渲染英雄列表的时候，作为自定义属性放在td父元素身上

* 前端：点击删除按钮，采用事件委托注册点击事件

  ```js
  // 删除英雄
  app.post('/hero/delete', (req, res) => {
      const id = req.body.id;
      heroModel.delete(`id=${id}`, (err, results) => {
          if (!err) {
              res.send({
                  code: 200,
                  msg: '这就删了'
              })
  
          } else {
              res.send({
                  code: 500,
                  msg: '不是我的错'
              })
          }
      })
  })
  
  
  
  
  ```

### 编辑英雄



| 接口名称     | 接口类型 | 接口参数 | 返回数据                  |
| :----------- | :------: | -------- | ------------------------- |
| /hero/update |   post   | formdata | {code:200,msg:'编辑成功'} |



* 此处和添加差不多
* 更新数据库heroModel.update(`id=${id}`,{name……},(err,results))
* 前端：注意调用接口时设置`contentType:false,processData:false`
* 前端：注意上传的表单的name属性和接口接收的参数名称保持一致，以免产生错误
* 前端：点击编辑按钮，采用事件委托进行注册
* 在接口中自己添加了，当用户不更改文件的时候，仍然为一开始的文件，在内部做了一个判断，进行实现逻辑
  * 因为用户不更改文件，也就意味着`document.querySelector('fileInput').files[0]`不存在，所以当点击上传的时候，后端接收req.files.icon.name也就不存在，所以就会导致服务器内部出错，所以做出了处理

```js
// 编辑英雄
app.post('/hero/update', (req, res) => {
    // 直接图片上传，如果不改则会报错 因为默认打开编辑页面 文件域是没有东西的
    // 设置不改有默认值 
    // 只要修改就没问题
    const name = req.body.name;
    const skill = req.body.skill;
    const id = req.body.id;
    if (req.files) {
        const icon = req.files.icon.name;
        req.files.icon.mv(path.join(__dirname, './uploads', icon), err => {
            if (!err) {
                console.log('上传成功！');

            }
        })
        // icon='http://localhost:3000/'+icon;
        heroModel.update(`id=${id}`, { name, skill, icon }, (err, results) => {
            if (!err) {
                res.send({
                    code: 200,
                    msg: '说改就改'
                })
            } else {
                res.send({
                    code: 500,
                    msg: '不是我的错'
                })
            }
        })

    } else {
        // icon='http://localhost:3000/'+icon;
        heroModel.update(`id=${id}`, { name, skill }, (err, results) => {
            if (!err) {
                res.send({
                    code: 200,
                    msg: '说改就改'
                })
            } else {
                res.send({
                    code: 500,
                    msg: '不是我的错'
                })
            }
        })
    }




})


```

### 用户注册

| 接口名称       | 接口类型 | 接口参数            | 返回数据                  |
| :------------- | :------: | ------------------- | ------------------------- |
| /user/register |   post   | {username,password} | {code:200,msg:'注册成功'} |



* 注册时候需要考虑：
  * 是否已被注册
  * 没有被注册就存储到数据库
  * 通过提交的username作为条件，进入数据库查找，如果results的长度不为0，说明之前注册过
* 前端：判断非空，两次输入的密码不一致，密码上传之前，可以采用加密方式进行上传`password=md5(password,'lxh')`，后面具体讲
* 后端：要进行非空判断，以免高级用户采用非法手段进行破坏

```js
// 用户注册
app.post('/user/register', (req, res) => {
    // res.send('/user'); 
    const username = req.body.username;
    const password = req.body.password;
    if (username == '' || password == '') {
        res.send({
            msg: '干啥呢你！',
        })
    }
    userModel.find(`username="${username}"`, (err, results) => {
        // console.log(results);
        if (!err) {
            if (results.length != 0) {
                res.send({
                    code: 401,
                    msg: '该用户名，已经被注册过了，重新注册吧！'

                })
            } else {
               userModel.insert({username,password},(err,results)=>{
                   if(!err)
                   {
                    res.send({
                        code:200,
                        msg:'恭喜你，注册成功！'
                    })
                   }else{
                       res.send({
                           code:500,
                           msg:'不是我的问题'
                       })
                   }
               })
            }
        } else {
            res.send({
                code: 500,
                msg: '不是我的错'
            })
        }

    })

})



```



### 用户登录

| 接口名称    | 接口类型 | 接口参数                    | 返回数据                  |
| :---------- | :------: | --------------------------- | ------------------------- |
| /user/login |   post   | {username,password,captcha} | {code:200,msg:'登录成功'} |

* 此处涉及到随机验证码的使用，后面详细介绍
* 验证码可以允许忽略大小写，采用str.toUpperCase()|str.toLowerCase()
* 前端：非空判断，上传密码参数之前也是通过加密转换`password=md5(password,'lxh')`
* 后端：非空判断，验证码输入是否正确，通过查询条件为username,password,进行查询条件，如果results的长度不为0，说明输入密码和用户名都正确，可以登录
* 当登陆成功，设置会话机制`req.session.userInfo=results[0]`，进行记录用户登录成功，并设置中间件，判断在进行调用`/hero/*`相关接口时，是否存在此会话机制，然后允许接下来操作
* 前端：验证码是设置的img的src属性进行调用接口
* 前端：实现点击图片切换验证码，会存在缓存问题，解决：设置不同的请求地址`/user/captcha?id=${Date.now()}`

### 退出登录

| 接口名称     | 接口类型 | 接口参数 | 返回数据                  |
| :----------- | :------: | -------- | ------------------------- |
| /user/logout |   get    | 无       | {code:200,msg:'退出成功'} |

* 点击退出，删除用户的登录状态

* 前端不用干任何事情

  ```js
   
  
  //  用户退出
  app.get('/user/logout',(req,res)=>{
      req.session.userInfo=undefined;
      res.send({
          code:200,
          msg:'退出成功！'
      })
  })
  
  
  
  ```

* 面试可能会问到的问题：

  * localStorage和sessionStorage的区别：
    * 前者关闭浏览器还在
    * 后者关闭浏览器消失
    * 只能存字符串，如果要存复杂类型可以结合json.stringify
  * localStorage和sessionStorage和cookie和session的区别：
    * cookie保存位置是浏览 自动保存 自动携带 容量小4kb
    * session保存的位置是服务器 浏览器用cookie存了一个 标记 钥匙
    * 服务器根据cookie携带而来的标记获取详细信息
    * session消耗服务器的性能我之前的项目用的是token
    * 我和你说说token吧
    * .……
    * axios中可以用拦截器统一设置token
    * 在vue中用导航守卫统一判断是否有token
    * 我们聊一聊vue吧

### 整合静态资源服务器

* 添加代码`app.use(express.static('./web'))`,其中web文件存放的是所有前端静态资源，为了列表渲染的时候，可以看到之前的随机生成的网页的图片，需要设置代码`appp.use(express.static('./uploads'))`
* 调用接口的时候，无需输入完整的接口地址，eg:`/hero/list`即可调用接口成功









### Mockjs-模拟数据生成

1.Mockjs的js库，可以生成随机的测试数据

2.网址：`http://mockjs.com`

3.输入`npm install mockjs`

```js
var Mock = require('mockjs')
for(let i=0;i<1000;i++){
    const name=Mock.Random.cname;
    const skill=Mock.Random.cparagraph(3,10);
    const icon=Mock.Random.image('200x200',Mock.Random.color(),name);
    heroModel.insert({name,skill,icon},(err,results)=>{})
}

```



### 验证码

1.网址：`http://npmjs.com/package/svg-captcha`

2.下包：`npm i svg-captcha`

3.导包

4.用包

```js
var svgCaptcha = require('svg-captcha');
 //必须是get请求
app.get('/captcha', function (req, res) {
    var captcha = svgCaptcha.create();
    req.session.captcha = captcha.text;
    
    res.type('svg');
    res.status(200).send(captcha.data);
});

```



后端：将验证码captcha.text通过全局变量captchaText保存起来方便后续使用

### 密码加密

* 通过某些算法，把某个值计算出一个新的结果
* 这个新的结果，无算反算回去
* 对称加密，非对称加密ASE……
* md5:最初设计摘要算法，从一个数据中算出一些特征值，计算结果无法反算
* 网址：`http://www.github.com/blueimp/javaScript-MD5`
* md5加密可以解出来，所以额外增加一个值，加盐`md5(加密的值,盐（额外的值）)`
* 黑客网址：`https://www.sec-wiki.com/skill/2`



### 会话技术

#### cookie(甜饼，曲奇)

* http是无状态的

* cookie的作用：解决http不会记录客户端（用户信息）这个缺点

* 注意：

* > 1.cookie是由服务器设置Set-Cookie
  >
  > 2.浏览器保存
  >
  > 3.浏览器会偷偷的携带到服务器Cookie
  >
  > 4.容量4kb大数据存不了



#### session

> 1.session保存的位置是服务器
>
> 2.格式是：key:value
>
> 3.浏览器中保存了一个cookie(标记，钥匙)
>
> 4.浏览器再次请求服务器时，会携带标记去服务器，服务器就可以根据标记获取对应的详细信息
>
> 5.session理论上来说，可以存很多东西

#### token

* cookie和session会占用服务器内存，性能消耗
* cookie和session必须依赖于浏览器
* 应用程序也需要保存状态，但是不支持cookie session
* token是由服务器生成，基于某种加密算法生成
* 在计算时会用到用户的一些信息，不同的用户算出来的值不同
* 计算完毕之后，服务器直接返回给浏览器，什么也不存
* 好处：
  * 网站可以用
  * app可以用
  * 服务器不需要存东西

### 登录状态维持(session的使用)

* 下包：`npm i express-session`

* 导包

* 用包

  ```js
  var session = require('express-session')
  app.use(session({
    secret: 'keyboard cat',
    resave: false,
    saveUninitialized: true,
    cookie: { secure: true }
  }))
  //保存信息
  req.session.userInfo=result[0]
  
  ```

### 同步和异步

* fs.readFile()异步
* hmModel.find('',(err,result)=>{})异步

### -echarts基本使用

* 数据可视化 数据编程图表

* 网址`https://www.echartsjs.com/zh/index.html`

  

### 快捷键

> 1.home end 行头 行尾
>
> 2.shift+home或end 选中一行
>
> 3.ctrl+左右 识别词组跳跃
>
> 4.vscode中快捷键
>
> ​	ctrl+enter:光标换行，文字不换行
>
> ​	ctrl+shift+enter 光标去上一行，文字不动
>
> 5.vscode相关快捷键的使用:`http://go.microsoft.com/fwlink/?linkid=832145`



### 补充typora主题

vue主题：

打开文件，选中偏好设置，点击获取主题进行下载，然后解压，把文件拷贝到打开主题文件夹中