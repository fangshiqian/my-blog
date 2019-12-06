---
title: JavaScript
date: 2019-12-04 09:46:51
top:
categories:
   - 学习
   - JavaScript
tags: JavaScript
---

## js介绍

* 脚本编程语言
* 作用：与用户进行交流互动

### 引入方式

* 行内式：

  ``` js
  <div onclick='alert('哈哈');'></div>
  ```

* 内嵌式

  ```js
  <script>
      document.getElementById('box')=function(){
      
  }    
  </script>
  ```

* 外链式

  <script src="demo.js"></script>


### 注释

* ctr+/  单行注释
* shift+alt+/ 多行注释

### 输入输出

* 输入：
  * prompt()
* 输出：
  * alert();用`+`进行连接
  * confirm()
  * console.log(),其中console.log(a,b);多个输出用`逗号`隔开
    * 转义字符 console.log('我说：\'我是'')；
    * 单双引号嵌套
    * es6解决 \`${num}`
  * document.write();可以识别html标签(页面上显示输出)

### 变量声明

* var a;

### 变量赋值

* var a=10;

* var a;

  a=10;

* var a=10;

  a=20;

* var a=10;

  a=a+10;

### 变量命名

* 使用范围是：字母，数字，下划线，$

* 不能以数字开头
* 不能以关键字命名
* 区分大小写
* 驼峰式命名
* 没有定义的变量名不能直接使用

### 交换值

* 取第三方变量

### 补充

* 声明多个变量

  ```js
  var a,b,c;
  ```

* 声明多个变量且赋值

  var a=10,b=20;

* 声明变量，赋值为另一个变量

  ```js
  var a=10;
  var b=a;
  ```

### 五种简单的数据类型

#### number	

* 数字
* NaN 不是某个数

#### String

* ``` js
  var str='abc';
  ```

#### boolean

* 存在即成立

* true
* false

#### null值

#### undefined

* 变量进行初始化，未赋值

#### 查看数据类型

* typeof(a)或者typeof a
* 其中null显示的数据类型是`object`
* prompt()存储的数据类型是字符串类型
* String类型遇到`+`,把其他类型转换为String类型，形成字符串拼接

#### 转数字

* Number()：
  * 转为数字：true=1,false=0,null=0,字符串里面的内容`**完全**`为数字
  * NaN:undefined,string
* parseInt()
  * `只有字符串能转成功`
  * 以数字开头的字符串也可以成功
  * 转整数，不会进行四舍五入，直接去掉小数部分
* parseFloat()
  * `只有字符串能转成功`
  * 以数字开头的字符串也可以成功
  * 转小数

#### 转字符串

* String()
  * 全部转为字符串
  * String(a)
* toString()
  * `null`和`undefined`不能
  * a.toString();

####  转布尔

* 结果：存在或者不存在
* 字符串 true
* 数字类型 true
* 六个false：
  * 0
  * 空字符串''
  * NaN
  * undefined
  * false
  * null

### 运算符

#### 算数运算符

* \+  - * % /
* 字符串遇见+，把左右数据类型 转换为字符串（字符串拼接）
* 其他类型的数据进行遇到算术运算符时，会先做隐式转换Number()
* 字符串遇到其他除了+的运算符将做隐式转换，转换为Number()
* ++a,a++
  * ++a先进行自加，在进行运算
  * a++先进行运算，在进行自加

#### 比较运算符

* < > = < =
* 结果是Boolean
* 优先于赋值运算符
* 非Number和Number类型比较，非Number类型要进行隐式转换
* **注意**：这里说的是非Number和Number类型进比较的时候会进行隐式转换，当两个非Number类型数据进行比较的时候，转换规则就不一定了
* ===和==
  * ==先比较类型，类型同比较值；类型不同进行隐式转换转为Number类型
    * NaN==NaN为false
    * null==0 false
    * undefined==0
    * null==undefined true
  * ===只有相同类型才进行比较值

#### 逻辑运算符

* &&与||
  * &&且全部满足，有一个不能满足false（此时的true或fale根据当前左右两边的值内容，进行输出结果，你懂得)）
  * ||有一个满足就是true(此时的true或fale根据当前左右两边的值内容，进行输出结果，你懂得)
* !取反

### 赋值运算符

- +=  -=  *=  /=
- a=a+2------a+=2

### 优先级

- 有括号先算括号内部
- 自增 自减 ！
- 乘除取余
- 加减
- 比较运算> >= <= <
- 比较运算== === != !==
- 逻辑运算 &&
- 逻辑运算||
- 赋值运算

### 分支结构

* 语法：

  ```js
  if(a=='female'){//
      
  }else if(a=='male'){
           
  }else{
      
  }
  
  
  switch(info){//固定值
         	case '1':
         	console.log();
      	break;
      	case '2':
      	break;
      	default:
      	break;
         }
  //三元表达式：
  var a=a<10?'0'+a:a;
  	
  ```

* 对于字符串与字符串进行比较的时候，注意并不是转换为数字类型，而是转换为Ascii码

### 循环结构

* while循环 注意退出条件

* for循环

  ```js
  for(var i=0;i<10;i++)
  {
      
  }
  ```

* do-while循环，至少执行一次

* break和continue

  * break直接跳出循环
  * continue 结束当前循环 执行下一次循环

### 数组

* 有长度，有顺序的数据集合

* 声明

  * 字面量 var arr=[] 空数组 类型是object
  * 构造函数 var arr=new Array()
    * 注意var arr=new Array(90)其中90表示数组的长度

* 存值

  * 存值 arr[0]=94 通过索引进行存值，下标从0开始
  * var arr=[10,20,40,null,undefined]

* 取值：

  * 通过下标进行取数据

  * 遍历：

    ```js
    for(var i=0;i<){
        
    }
    ```

* 清空数组：arr.length

* 小娜案例

  * Math.random()0-1随机数
  * Math.floor()向下取整
  * var date=new Date()
  * date.getfullYear()
  * date.getMonth()
  * date.getDate()
  * date.getHours()
  * date.getMinutes()
  * date.getSeconds()

### 函数

* 声明函数

  

  ```js
      function tell_story(){
  
      }
      //函数表达式
      var fn_1=function(){
  
      }；
      //匿名函数 不能单独使用
  ```

* 调用函数

* ```js
  tell_story();
  ```

* 参数

  * 形参
  * 实参：不传入实参，默认为undefined

* `形参和实参互相不影响 实参是简单数据类型`

* 返回值 return  函数内部没有返回值时，接收为undefined

  * 修改函数的返回值只能返回一个值
  * 终止函数return后面的代码的执行

* arguments 函数内部隐藏变量 伪数组 

  * 有长度 有顺序 可遍历
  * 之所以是伪数组是因为，其不可以调用数组的一些方法

* 函数的类型是function

* 回调函数

  ```js
  function demo_1（demo）{
      demo();
  }
  demo_1(function (){
      concole.log('我是回调函数');
  })
  
  ```

  

  

* 作用域

  * 全局作用域：在script内部声明的变量 包括函数function作用域
  * 局部作用域：函数内部

* 预解析：把你声明的变量和函数function fn(){}提前到当前作用域最顶端

  ```js
  var num=10;
  fn();
  console.log(num);//10
  function fn(){
      console.log(num);//undefined
      var num=20;
  }
  
  
  var num=10;
  fn();
  console.log(num);//20
  function fn(){
      console.log(num);//10
      num=20;
  }
  
  
  
  ```

  

  

### 对象

* 声明对象

  * 字面量 var obj={};
  * 构造函数 var obj=new Object();

* 添加属性

  * 点方式：

    * obj.name='狗蛋'
    * obj.sayName=function(){}

  * 在声明对象时设置

    var obj={

    name:'张三',

    age:18,

    say:function(){

    },

    }	

  * 键值对

    ```js
    obj['height']=20
    ```

* 获取属性和遍历属性

  * 点方式 obj.name obj.say()

  * 键值对方式 obj['name'] 注意括号内部是字符串 obj['say']（）

  * 遍历

    ```js
    for(var key in obj)
    {
        console.log(key,obj[key]);//必须是键值对方式获取
    }
    ```

### 小娜

* arr.concat()；

### Math拓展

* Math.random()输出0-1的随机数
* Math.floor()浮点数向下取整

### 数组的拼接

* arr.concat([3,5]),注意此与push的区别，push返回的是数组的长度，它返回的是新的拼接的数组，需要接收

### 简单类型和复杂类型

* 简单类型传递值

* 复杂类型传递地址

  ```js
  var a=10;
  var b=10;
  console.log(a==b)；//true
  var b={};
  var c={};
  console.log(b==c);//false
  
  
  var num=10;
  fn(num);
  console.log(num);//10
  function fn(num){
      num=20;
  }
  
  
  var obj={
      a:10,
  }
  fn(obj.a);
  console.log(obj.a);//20
  function obj(obj){
      obj.a=20;
  }
  
  ```

### Math

* Math.random()；随机数，获取[0,1)的随机数
* Math.floor();向下取整
* Math.ceil()；向上取整
* Math.round()；将浮点数四舍五入
* Math.abs();绝对值
* Math.max();可以传入多个参数，获取这些数的最大值

### Date

* 特定格式 输入一个字符串

  ```js
  var date=new Date('2019-09-15');
  var month=date.getMonth()+1;
  console.log(month)；
  
  ```

* 获取毫秒数 时间戳

  ```js
  var date=new Date();
  console.log(date.valueof());
  console.log(date.getTime())；
  console.log(1*date);
  console.log(Date.now());
  ```

* 绝对的唯一的数值

  ```js
  Math.random()*date.valueof();
  ```

### Array

* push 把一个元素或多个元素 从数组的后面

  * 参数：传入一个或者多个数据
  * 返回值：新的数组的长度

* pop 删除数组的最后一个元素

  * 参数：无
  * 返回值：被删除的元素

* unshift 在数组前面添加一个或者多个元素

  * 参数：一个或者多个数据
  * 返回值：新数组的长度

* shift:删除一个数组的前面的第一个元素

  * 参数：无
  * 返回值：被删除的元素

* splice 替换（增删改）

  * 增加

    * 参数 
      * 第一个参数：元素的开始下标
      * 第二个参数：移除元素的个数
      * 第三个元素：添加的元素
    * 返回值：返回空数组

    ```js
    var arr=[1,2,3,4,5,6];
    arr.splice(3,0,7,8);//在索引为3的位置上，不移除元素，添加7,8数据
    
    ```

  * 删除

    * 参数

      * 第一个参数：元素开始下标
      * 第二个参数：元素删除的个数

    * 返回值：返回删除数据组成的数组

      ```js
      var arr=[1,2,3,5,6,7];
      arr.splice(3,1);
      
      ```

  * 改正

    * 参数

      * 第一个参数：元素开始下标
      * 第二个参数：修改元素的个数
      * 第三个参数：修改之后的元素

    * 返回值：被删除的元素组成的数组

      ```js
      var arr=[1,2,3,5,6,7];
      arr.splice(3,1,'a');
      ```

* 与字符串进行互转

  * 数组转换字符串join

    ```js
    var arr=[1,2,3,4];
    var str=arr.join('|');
    console.log(str);//1|2|3|4
    ```

  * 字符串转换数组split

    ```js
    var str='1-2-3-4-5';
    var arr=str.split('-');
    console.log(arr);
    
    ```

* 查找元素

  * indexOf 查找指定数据的索引

    * 参数：传入一个数据元素

    * 返回值：返回索引，如果数组中没有此元素，返回-1

      ```js
      var arr=[1,2,3,4];
      var res=arr.indexOf(1);//返回0
      ```

  * findIndex 查找满足条件的第一个元素的索引 

    * 参数：传入一个函数

    * 返回值：返回索引 如果没有此元素，返回-1

      ```js
      var arr=[1,2,3,4,5,7];
      var res=arr.findIndex(function(item){
          return item>10;
      })
      ```

* 遍历

  * for循环

  * forEach循环

    * 参数：传入回调函数

      * 第一个参数：每个元素
      * 第二个参数：索引
      * 第三个参数：当前循环的数组

      ```js
      arr.forEach(function(item,index,arr){
          console.log(item);
      })
      ```

  * 伪数组不能使用数组的方法

  * filter筛选

    * 参数：传入回调函数

      * 第一个参数：每个元素
      * 第二个参数：索引
      * 第三个参数：当前循环的数组

      ```js
      arr.filter(function(item,index,arr){
        
          return item>10;
      })
      
      ```

* 拼接和截取 f返回的是新数组 不会对原数组进行操作

  * concat 拼接

    * 参数：传入一个或者多个数据

    * 返回值：新的数组

      ```js
      arr=arr.concat([4,5],[7,8]);
      
      ```

  * slice 截取

    * 参数：

      * 第一个参数：开始截取的下标 包括
      * 第二个参数：结束截取的下标 不包括

    * 返回值：返回新的数组

      ```js
      arr.slice(1,3);//从1索引开始截取到索引3，其中不包括3
      arr.slice(1);//从索引1开始截取截取到最后
      arr.slice();//从头截取到尾
      ```

* 复制

  * forEach

    ```js
    arr.forEach(function(item,index){
        new_arr.push(item);
    })
    ```

  * slice

    ```js
    var new_arr=arr.slice();
    ```

  * filter

    ```js
    arr.filter(function(item,index){
        return arr.indexOf(item)!=-1;
    })
    ```

  * concat

    ```js
    var new_arr=arr.concat();
    ```

  * 不是复制

    ```js
    var arr=[1,2];
    var new_arr=arr;//错误
    console.log(new_arr==arr);//true
    ```

* Object复制

  ```js
  var obj={
      name:1,
  };
  var obj1={};
  for(var key in obj){
      obj1[key]=obj[key];
  }
  ```

### String

* 不可变性：新组成的字符串，它会放在内存上的空间，但是原来的字符串不会被覆盖，而是处于游离状态
* 如何提升前端性能
* 查找：
  * indexOf()
    * 参数：传入字符串
    * 返回值：索引 如果在字符串上 就返回查找字符串所在的索引，没有返回-1
  * lastIndexof() 从后往前查找 但是返回正常的索引
    * 参数：传入字符串 
    * 返回值：索引 如果在字符串上 就返回查找字符串所在的索引 没有返回就-1
  * charAt()
    * 参数：索引值
    * 返回值:输出索引位置的字符
  * charCodeAt()
    * 参数：索引值
    * 返回值：输出索引位置的字符的ASCII码
* 字符串转数组split
* 字符串拼接与截取
  * concat
  * +
  * slice()与下面的区别，参数可以是负值（负值与字符串长度相加）
  * substring(2，5)从索引2开始截取到索引5，不包括5
  * substr(2,2);从索引2开始截取，总共截取两个















