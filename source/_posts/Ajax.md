---
title: Ajax
date: 2019-12-04 09:47:05
top:
categories:
   - 学习
   - Ajax
tags: Ajax
---

# Ajax

## 上网过程

1.打开浏览器

2.地址栏，输入网址

3.回车

4.最终，看到页面

![1571047321929](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1571047321929.png)

## 关键词

* 客户端：client 一般指浏览器
* 服务端：server 电脑 （存储网页，响应客户端）
* 请求 : request
* 响应：response
* 资源：source

## 搭建Web服务器

用vs打开ajax文件，右击app.js,在终端打开，输入命令node app.js

注意：

​	1.服务不能重复开启，即不能多次执行

​	2.ctrl+~快速打开和关闭终端

​	3.关闭终端面板，不代表关闭服务器

将文件放到ajax/public文件夹内

通过ip或者域名访问自己的服务器http://192.168.156.65:4000/index.html

通过回环地址或者localhost访问



## Ajax初始

使用Ajax不会刷新页面

* 接口介绍
  * 网址
  * 接口文档

ajax通过执行一段js代码来发送和接收响应结果

语法：

```js
$.ajax({
    type:'请求方式',//GET【默认】 POST
    url:'接口地址',//接口或者完整的文件路径【必填】
    data:'请求参数',
    dataType:'响应数据格式',//默认text
    success:function(result){
        //result 表示服务器返回的结果
    }
})
```



### data请求参数写法

* 字符串

  ```js
  data:'参数=值&参数=值……'
  ```

* 对象

  ```js
  data:{
      参数：值,
      参数：值
      ……
  }
  ```

## ajax方法详解

* type:表示请求的方式或方法

  * 常见的两种请求方式
    * GET:获取，向服务器请求资源，不会改变服务器的数据【地址栏】
    * POST:获取+提交数据，可能会修改服务器上的数据

* data:请求参数（接口文档的请求参数）

  * 写法
    * 对象：{name:name,content:content}
    * 字符串：‘name=name&content=content’
  * 字符串形式，GET请求时候，接口和请求参数？隔开

* dataType:服务器响应的数据格式，自动将服务器响应的数据处理成js数据

  * json:将原来的json字符串转换成对象
  * text
  * xml
  * jsonp,script,html

* beforeSend:发生ajax请求之前，执行的操作

  * 语法:

    ```js
    $.ajax({
        beforeSend:function(){}
    })
    ```

* complete:ajax请求结束之后，执行的操作

  * 语法：

    ```js
    $.ajax({
        complete:function(){}
    })
    ```

## 进度条插件NProgress

引入NProgress.js和NProgress.css

```js
beforeSend:function(){
    NProgress.start();
}
complete:function(){
    NProgress.done();
}
```









## 原生ajax请求

基本语法：

GET:

```JS
//1.实例化 XMLHttpRequest对象
var xhr=new XMLHttpRequest();
//2.调用open方法，设置请求方式和url
xhr.open('GET','/common/time');
//3.调用send方法，发生请求
xhr.send();
//4.请求响应过程结束，接收服务器响应的结果
xhr.onload=function(){
    console.log(xhr.response);
    console.log(xhr.responseText);//接收文本类型结果
}

//如果有请求参数：
//请求参数拼接到url后面即可
xhr.open('GET','/common/checkUser?username=lisi');

```



POST:

```JS
//1.创建xhr对象
var xhr=new XMLHttpRequest();
//2.调用open方法，设置请求方式和url
xhr.open('POST','/message/addMsg');
//3.设置请求头，固定
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
//4.调用send，发送请求
xhr.send('name="张三"&content="今天真好"');//必须用字符串
//5.设置onload事件，接收服务器响应的结果
xhr.onload=function(){
    console.log(this.response);
}
```



GET和POST区别：

* GET:请求一般用于获取服务器上的资源，这种请求不会改变服务器数据
* POST：一般用于提交数据给服务器，这种请求有可能会改变服务器上的资源
* 请求参数位置不同
* POST请求多了一行代码

## 三级联动

获取省市县

接口中的请求参数id,和文件名一个意思

id=0,表示获取所有省

id=105,表示获取河北省下属的市

id=105001,表示获取石家庄下属的县

## 浏览器问题

### 兼容

onreadystatechange事件配合readyState,完成获取响应结果的任务，代替onload事件，只不过使用onreadystatechange事件需要添加判断

onload事件属于xhr对象新增的一个属性，ie678不支持，所以采用onreadystatechange

* onreadystatechange事件：
  * 会触发多次
  * 触发时机：
    * 当readyState属性值（ajax状态）发生改变（0-->1,1--->2……）的时候，会触发事件
    * 接收数据量发生变化，也会触发
* readyState属性：
  * 表示ajax请求到哪个阶段，表示ajax执行状态，值分别为0,1,2,3,4，共计5个值
    * 0   unsent xhr未创建 未调用open()
    * 1 opened open方法调用 建立连接
    * 2 headers_received send()方法调用 已经获取状态行和响应头
    * 3 loading 响应体下载中 并不表示完成
    * 4 done 响应体下载完成 完全接收

### ie缓存问题

产生原因：两次或多次请求ajax(GET方式)，url地址一样导致访问缓存，获取数据相同

解决办法：每次请求的url不一致

## 其他API

### 创建xhr对象的兼容写法

var xhr=new XMLHttpRequest();//不兼容ie67

var xhr=new ActiveXObject('Microsoft.XMLHTTP');

兼容代码：var xhr=window.XMLHttpRequest?new XMLHttpRequest():new ActiveXObject('Microsoft.XMLHTTP');

### responseType属性

不支持ie678

类似$.ajax中的dataType,指定该属性会把JSON格式的数据转成js数据（对象、数组）

### API小结

XHR1.0版本

​	open

​	send

​	onreadystatechange

​	readyState

​	responseText

XHR2.0版本

​	onload  相当于readyState=4

​	responseType 

​	response

​	onprogress 正在接收结果 readyState=3

​	onloadstart beforeSend

​	onloadend complete



## 同步和异步

异步：同一时间，有多个操作同时执行。耗时操作，不会影响后续代码执行，不会阻塞后续代码执行。eg:定时器，ajax请求默认



同步：同一时间，只能做一个操作。耗时操作，会影响后续代码执行，会阻塞后续代码执行

xhr.open(type,url,true)//true默认异步

## 封装

回调函数是处理异步的结果的最佳方案

```js
/*type:请求方式
data:请求接口地址
data:请求参数
callback:用于处理服务器响应结果的回调函数
function ajax(type,url,data,callback){
	type=type==undefined?'GET':type;
	data=data==undefined?'':data;
	var xhr=new XMLHttpRequest();
	var params='';
    if(type==='GET'){
    url+=url+'?'+data;
    }
    xhr.open(type,url);
    if(type==='POST'){
    xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
    params=data;
    }
    xhr.send(params);
    xhr.onload=function(){
    callback&&callback(this.response);
    }
    
}
*/

```



​	



## FormData

使用步骤：

有form标签：（注意此时form内部的表单控件，需要上传的需要设置name属性，否则接收失败）

* 找到form表单，找表单的DOM对象

  ```js
  var fm=document.getElementById('fm');//form对象
  
  
  ```

* 实例化FormData对象，并传递表单即可，得到对象包含所有表单信息

  ```js
  var formdata=new FormData(fm);
  
  ```

* 接收到的数据应该发送到服务器

  ```js
  var xhr=new XMLHttpRequest();
  xhr.open('POST','/common/fd');
  //xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');//不写
  xhr.send(formdata);
  xhr.onload=function(){
      console.log(this.response);
  }
  
  ```

没有form表单：

* 需要自己手动添加

  ```js
  var formdata=new FormData();
  formdata.append('user',document.getElementById('user').value);
  
  ```

**请求头设置**

* 提交数据时纯文本，没有文件上传，需要设置请求头
* 使用FormData时候，不需要自己设置请求头

**注意事项**

* 不能让表单提交【input:submit input:image button等都会自动提交】
  * 设置按钮为input中type为button
  * js代码中，通过事件对象阻止表单提交默认行为
* 表单中各项必须有name属性，因为FormData收集表单数据时候，就是根据name属性获取的

## 获取文件对象

语法:

```html
<input type='file' id='pic' multiple accept='image/*'><!--multiple表示可以多选，accept设置选择文件的类型，可以写为image/* .jpg,.png,.gif image/png-->
<input type='button' value='获取文件对象' id='btn'>
<script>
    document.getElementById('#btn').onlclick=function(){
        var pic=document.getElementById('pic');//也是获取DOM对象
        var fileobj=pic.files[0];//找到文件对象
    }
</script>


```



## ajax综合案例

知识点：

* 获取地址栏参数部分：

  ```js
  location.search.replace(/\D/g,'')//获取参数的值
  
  ```

* 为文件对象创建一个临时url,url用于访问该图像

  ```js
  var fileobj=this.file[0];//DOM对象获取文件对象
  var url=URL.createObjectURL(fileobj);//URL是js内置对象
  
  ```

* 调用接口传递表单信息

  ```js
  $.ajax({
      type:'POST',
      url:'/memeber/add',
      data:formdata,
      dataType:'json',
      contentType:false,//表示不设置请求头Content-Type
      processData:false,//表示不需要将formdata转成字符串
      
      success:function(res){
          location.href='index.html';
      }
  })
  
  ```

* 注册事件必须使用事件委托

* 超链接跳转属于GET请求，传递参数，需要在url后面拼接'detail.html?id=12'





## jQuery中的ajax补充

* $.ajax()

  ```js
  $.ajax({
      type:'请求方式',
      url:'接口地址',
      data:'请求参数',
      dataType:'响应数据格式',
      contentType:application/x-www-form-urlencoded(默认)，//设置请求头
      processData:'是否设置处理请求参数',
      success:function(res){
      //res就是服务器返回的结果
  },
      beforeSend:function(){
          
      },
          complete:function(){}
  })
  
  ```

* $.get([url],[data],[fn],[dataType])

  ```js
  $.get('接口地址','请求参数','请求成功后的回调函数','服务器返回数据的类型')
  
  ```

* $.post([url],[data],[fn],[dataType])

  ```js
  $.post('接口地址','请求参数','请求成功后的回调函数','服务器返回的数据类型');
  
  ```

## 封装库axios(别人封装的ajax)（了解）

* 语法

  ```js
  axios.get('/common/time').then(function(res){
      console.log(res);
  })
  
  ```



## template模板引擎

* 字符串拼接，降低性能，使用模板引擎，使html和js分离

* 渲染页面

  ```html
  <script src="./assets/template-web.js"></script><!--引入模板引擎js文件-->
  <script type="text/html" id='test'>
  <h2>{{title}}</h2>
  <p>
  	{{if age>18}}
  	欢迎来玩~
  	{{else}}
  	禁止未成年人进入
  	{{/if}}
  </p>
  <ul>
  	<li>{{heros[0]}}</li>
  	<li>{{heros[1]}}</li>
  	<li>{{heros[2]}}</li>
  	
  	第二种
  	{{each heroes}}
  	<li>{{$index}}--{{$value}}</li>
  	{{/each}}
  </ul>
  </script>
  <script>
      var data={
          title:'模板引擎练习',
          age:20,
          heroes:['曹操','刘备','李逵','张飞']
      }
      var str=template('test',data);//数据必须是js对象格式
      
  </script>
  
  
  ```

  

