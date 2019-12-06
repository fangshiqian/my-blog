---
title: js高级
date: 2018-12-03 09:33:09
top:
categories:
   - 学习
   - js高级
tags: js高级
---

# js高级

## 面向对象

三大特性：封装性、继承性、多态性

类：泛指一类

对象：类中的具体某个实例【属性和方法的集合】

属性：特征 对象.属性

方法：行为 对象.方法

## ES6

### 创建类

类名首字母大写

语法：

```js
class Star{
    
}

```

### 实例化对象

语法：

```js
var n=new Star();
//对象 instanceof 构造函数
//判断对象是否属于该类
console.log(n instanceof Object);

```



### 构造函数

属性放到构造函数constructor中，当自己没有定义构造器，系统会自动创建一个构造函数

作用：传递参数，返回实例对象，new的时候自动执行构造函数，放一些公共属性

语法：

```js
class Star{
    constructor(name,age){
        //属性 对象.属性
        //this 当前实例对象
        //this.属性名字=属性值
        //构造函数中的this,代表的是当前实例对象
        this.name=name;
        this.age=age;
    }
}
var obj=new Star('二柱子',22);//随着实例化对象，构造函数自动执行
```



### 添加方法

定义与构造函数一样，方法之间不需要写逗号进行分隔，注意类里面的函不加function

语法：

```js
class Star{
    constructor(){
        
    }
    sing(){
        
    }
    dance(){
        
    }
}
//方法： 对象.方法()
```



### 类的继承

通过extends关键字

```js
class Father{
    constructor(name,age){
        this.name=name;
        this.age=age;
    }
    qian(){
        
    }
}
//子类继承父类
class Son extends Father{
    
}
```



### super关键字



当子类有需要的自己的属性或者方法时，如何继承？

```js
class Son extends Father{
    constructor(name,age,scole){
        //super调用父类的构造函数和方法
        super(name,age);
        this.scole=scole;
    }
    say(){
        
    }
    qian(){
        //调用父类的方法
        //super.qian();
    }
}
var obj=new Son('李寻欢',22,100);
obj.qian();//自己有的方法先执行自己的方法，没有则调用父类的方法
```



### 注意事项

* 必须先定义类，在进行实例化对象
* 类里面的属性和方法加this[对象.属性   对象.方法()]
* this指向问题：
  * 构造函数：this执行实例对象
  * 方法：this指向调用者【谁调用这个方法，这个方法里面的this就指向谁】

### tab栏切换

思路：

* 定义一个tab栏类，构造函数中获取相关（标签）属性

* 定义一个初始化init方法，用来添加事件【li点击事件+添加tab栏的添加点击事件】

* 定义tab栏切换方法，使下面的内容对应切换以及样式进行改变

* 定义一个清除类样式的方法，用来实现排他思想

* 定义点击实现添加tab栏的方法

  * 将指定文本解析为html或者xml，并将结果添加到dom树上

    ```js
    that.ul.insertAdjacentHTML(position,text);
    //position:
    	//beforebegin:在元素的前面添加
    	//afterbegin:在元素内部的第一个元素前添加
    	//beforeend:在元素内部的最后一个元素前添加
    	//afterend:在元素的后面添加
    //text:要添加的文本
    ```

### 自定义属性

之前webapi学过添加自定义属性

将属性添加到标签上：

```js
img.setAttribute('index',i)
```



还有一种是从DOM树上添加：

```js
img.index=i;

```



## ES5

### 创建对象

* 字面量方式

  ```js
  var obj={
      name:'张三',
      age:22,
      sex:'男',
      taiji:function(){
          console.log('哇哈哈');
      }
  }
  
  ```

* 通过构造函数创建对象【Object】

  ```js
  var obj=new Object();
  obj.name='张三';
  obj.taiji=function(){}
  
  ```

* 自定义构造函数

  ```js
  //构造函数名字首字母大写
  //构造函数和new一起使用
  function Star(name,age){
      this.name=name;
      this.age=age;
      this.taiji=function(){}
  }
  var zxc=new Star('张三',22);
  
  ```

* 工厂模式

  ```js
  function Star(name,age){
      var obj=new Object();
      obj.name=name;
      obj.age=age;
      return obj;
  }
  var str=new Star('张三',22);
  
  ```

### 区别普通函数和构造函数

是否使用new

### new创建对象做的四件事情

* 创建一个新对象的内存空间
* 将this指向这个新对象
* 执行构造函数内部代码，为新对象添加属性和方法
* 返回当前的新对象

### 静态成员和实例成员

* 静态成员：从构造函数本身上的成员叫静态成员，只能通过构造函数调用
* 实例成员：从构造函数内部的成员叫实例成员，只能通过实例对象调用

### 原型对象

**属性放在构造函数，方法放在原型对象上，节省内存**

原型对象：prototype,构造函数的一个属性

语法：

```js
Star.prototype.sing=function(){
    
}

```



### 对象原型

作用：指向原型对象prototype

对象上都有这个属性

```js
console.log(obj.__proto__==Star.prototype);

```



当需要重新设置原型对象时候，需要设置一下构造器constructor重新指回构造函数

```js
Star.prototype={
    constructor:Star,
    sing:function(){
        
    },
    dance:function(){
        
    }
}

```



### 构造函数constructor

作用：指回构造函数本身

原型对象上的一个属性

### 三者关系

![1570797150687](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1570797150687.png)



### 原型链

提供成员查找机制，或者查找规则

![1570797720477](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1570797720477.png)



```js

```

元素标签的原型链：

HTMLinputElement--->HTMLElement---->Element---->Node----->EventTarget---->Object---null

作用域链（往上找）

0级作用域<-----1级作用域<-----2级作用域

### 扩展内置对象的原型对象方法

给数组添加获取最大值的方法：

```js
Array.prototype.max=function(){
    var max=0;
    for(var i=0;i<this.length;i++)
    {
        if(max<this[i]){
            max=this[i];
        }
    }
    return max;
}

```



### 继承

组合继承=构造函数+原型对象

语法：

属性继承：

```js
function Father(name,age){
    this.name=name;
    this.age=age;
}
Father.prototype.sing=function(){
    
}
//属性继承
function Son(name,age,scole){
    //父类对象
    Father.call(this,name,age);//改变this指向
    //this:表示当前改变的this指向
    //其他参数：Father其他参数
    this.scole=scole;
}

```



方法继承：

将父类的实例对象赋值给子类的原型对象，再把子类的原型对象指回构造函数constructor

```js
Son.prototype=new Father();
Son.prototype.constructor=Son;//需要重新指回构造函数
Son.prototype.sing=function(){
    
}//子类添加自己的方法，需要添加在继承方法的后面否则将会报错

```



## 类的本质



本质就是函数function,类中有原型对象，其实例对象中也有对象原型

语法糖：简单的语法



## 数组的方法

### forEach方法

遍历数组

```js
arr.forEach(function(item,index,arr){
//第一个参数：当前项
//第二个参数：当前索引值
//第三个参数：当前遍历数组本身
})

```



### filter方法

筛选数组

```js
arr.filter(function(item,index,arr){
    //参数设置与上面一样
    //返回值：返回一个新的数组
    return item
})

```



### some方法

查找数组:查找是否存在某一个值满足条件，当找到满足的值，立马结束程序（原理：存在一个返回值为true的语句 return true;）

```js
arr.some(function(item,index,arr){
    //参数设置与上面一样
    //返回值：true或者false
    return item==2;//return true
})

```



## 商品查询案例

思路：

* 打开页面，将数据遍历到表格上，考虑后面筛选和查找还会进行遍历到表格上，所以把遍历定义成一个方法
* 点击按钮，获取价格区间，进行筛选显示内容，所以注册一个点击事件，筛选价格区间的商品，filter返回一个新数组，想让此数组显示在页面上，需要再次调用之前定义好的方法，进行显示
* 通过改变下拉菜单的选项，进行查找商品
  * option有value属性时，此时select.value==option.value
  * option没有value属性时，此时select.value==选中的option文本内容
  * 通过选中的value和id进行比较，从而选出对应的商品，添加到新数组中，需要再次调用之前定义好的方法，进行显示

## 字符串方法

trim():清除字符串两侧的空白格

```js
var str='   app  '；
str=str.trim();

```



## 函数定义

* 命名函数

  ```js
  function fn(){}
  
  ```

* 匿名函数

  ```js
  //函数表达式
  var fn=function(){}
  //自调用函数
  (function(){})()
  
  ```

* 通过Function构造函数创建函数

  ```js
  var fun=new Function('a','b','console.log("哈哈")');//传递的参数均为字符串格式
  //函数也是对象
  
  ```

## 函数调用

```js
//普通函数
function fn(){}
fn();
//事件处理函数
btn.onclick=function(){}
//对象方法
obj.sing();
//定时器
window.setInterval(function(){},1000)
//构造函数
new Father();
//自调用函数
(function(){})()


```



## this指向改变

this指向：

普通函数：window

构造函数：实例对象

绑定事件处理函数：当前绑定的对象

对象方法：当前调用者

自调用函数：window

定时器：window

### call方法

语法：

```js
function fn(a){
  console.log(a);  
}
var obj={
    name:'张三',
}
fn.call(obj,1);
//改变fn的this的指向
//obj 当前改变的this指向
//1 fn函数的其他参数

```



### apply方法

语法：

```js
function fn(a,b){
    console.log(a,b);
}
var obj={
    name:'张三',
}
fn.apply(obj,[1,2]);
//改变fn的this指向
//obj 当前改变的this指向
//[1,2] fn函数其他参数，且注意参数必须是以数组形式传入
//该方法一般用于与数组相关的操作
Math.max.apply(null,[2,3,1,4,9]);


```



### bind方法

语法：

```js
btn.onclick=function(){
    this.disabled=true;
    window.setInterval(function(){
        this.disabled=false;
    }.bind(this),1000)
}

```



* 相同点：三者都改变了this的指向,**注意是函数调用三者**
* 不同点：
  * apply第二个参数必须传入数组
  * call,apply方法返回值为调用的函数的返回结果（两者调用会使函数也调用），bind会产生一个新的函数，但是不会调用该函数
* 应用场景：
  * call:继承
  * apply:数组操作
  * bind:不需要立即执行的函数，如定时器

## 严格模式

js模式分为严格模式和正常模式

严格模式分为：

​	脚本严格模式：脚本第一句写‘use strict’;

​	函数严格模式：函数第一句写‘use strict’;

开启严格模式变化：

变量变化：必须通过var声明，且变量不可以删除（delete ）

this指向改变：

​		普通函数this变为undefined

​		构造函数不使用new,this也为undefined

函数变化：

​		函数不能在非函数区域内定义(产生块级链作用域)

​		函数参数不能重名 eg:function(a,a){}



## 高阶函数

**函数返回值：把这个值返回到调用的位置**

return如果有值，把这个值返回到调用的位置，return后面不写值，默认返回undefined，不写return,返回undefined

把函数作为参数传递或者把函数当做返回值返回的函数，叫做高阶函数

```js
function fn(n)
{
    n();
}
var m=function(){
};
fn(m);

function fn(){
    return function(){
        
    }
}
var f1=fn();
f1();

//判断传入的参数为函数
function fn(callback){
    callback&&callback();
}

```



## 闭包

在一个作用域可以访问另一个函数作用域内的变量，通常是内部函数访问外部函数的变量

作用：延伸变量的使用范围

```js
function fn(){
    var n=1;
    function f1(){
        console.log(n);
    }
}

```



## 递归

在函数内部自己调用自己，类似死循环，需要利用return进行结束

### 浅拷贝

```js
var obj={
    name:'张三',
    sing：{
    sex:'男'
};
var newObj={};
}
for(var key in obj){
    newObj[key]=obj[key];
}
//浅拷贝就是当遇到对象等复杂类型时，拷贝地址
Object.assign(target,source);
Object.assign(newObj,obj);

```



### 深拷贝

当遇到拷贝对象时候，直接复制对象

```js
function kaoBei(target,current){
    for(var key in current){
        if(current[key] instanceof Array){
            target[key]=[];
            kaoBei(target[key],current[key]);
        }else if(current[key] instanceof Object){
            target[key]={};
            kaoBei(taget[key],current[key]);
        }else{
            target[key]=current[key];
        }
    }
}

```



## 正则表达式

简单字符+特殊字符（元字符）

### 正则表达式的创建

* 方式一：字面量

  ```js
  var reg=/abc/;//包括abc整体
  
  ```

  

* 方式二：构造函数

  ```js
  var reg=new RegExp(/abc/);
  
  ```

### 正则测试

```js
reg.test('字符串');
//返回值：布尔值

```



### 边界符

* ^ 以什么文本位于首部

* $ 以什么文本位于尾部

* 如果^和$一起使用，精确匹配

  ```js
  var reg=/^abc$/;//只能是abc
  
  ```

### 中括号

```js
var reg=/[abc]/;//多选一 a|b|c
var reg=/^[abc]$/;//只能是a|b|c
var reg=/^[^a-zA-Z0-9]$/;//中括号里面的^是取反的意思，除了a-zA-Z0-9，只能选一个


```



### 量词符

* \* 表示0-多次重复
* \+ 表示1-多次重复
* ? 表示0或者1次
* {n} 表示重复n次
* {n,}表示重复n到多次
* {n,m} 表示重复n到m次

### 预定义类

* \d  [0-9]
* \D [\^0-9]
* \w [0-9a-zA-Z]
* \W[\^0-9a-zA-Z]
* \s空格符
* \S 非空格符

### 注册页面

location.href='网址';//跳转页面

navigator.userAgent;//浏览器相关信息

history.back()//返回上一个页面

history.forward()//返回下一个页面

### replace替换

```js
var str='abdkashdsd';
str=str.replace('b','*')；
//可以传正则表达式
str=str.replace(/b/g,'*');
//其中g表示全局替换
//i表示忽略大小写

```







