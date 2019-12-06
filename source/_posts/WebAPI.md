---
title: WebAPI
date: 2019-2-04 13:34:50
top:
categories:
   - 学习
   - WebAPI
tags: WebAPI
---

## WebAPI

* 节点：标签、文本、属性

### 获取节点DOM

* ById

  * 参数：id的字符串

  * 返回值：DOM节点 也是对象

    ```js
    document.getElementById('id字符串');
    //获取body
    document.body
    
    ```

* ByTagName 

  * 参数：标签名的1字符串

  * 返回值：伪数组 没有forEach方法 可以遍历 可以使用for循环

    ```js
    document.getElementsByTagName('li');
    ```

    

* ByClassName 

  * 参数：类名的字符串

  * 返回值 伪数组 没有forEach方法 可以遍历 可以使用for循环

    ```js
    document.getElementsByClassName('.box');
    ```

* querySelector

  * 参数：css选择器

  * 返回值：返回节点对象 （第一个被选中）

    ```js
    var box=document.querySelector('.box');
    ```

* querySelectorAll

  * 参数：css选择器

  * 返回值 伪数组 可以使用forEach循环 遍历 for循环

    ```js
    var lis=document.querySelectorAll('li');
    ```

    

### 注册事件on+事件类型

* 注册点击click事件

  * 事件源
  * 点击行为
  * 响应

  ```js
          btn.onclick=function(){
              alert('1');
          }
  ```

* 注册focus和blur事件

  - focus 获取焦点

  - blur 失去焦点

    ```js
    txt.onfocus=function(){
        
    }
    txt.onblur=function(){
        
    }
    ```

* 鼠标按下mousedown

  ```js
  box.onmousedown=function(){
      
  }
  ```

  

* 鼠标移动mousemove

  ```js
  box.onmousemove=function(){
      
  }
  
  ```

* 鼠标弹起mouseup

  ```js
  box.onmouseup=function(){
      
  }
  
  ```

* 键盘按下keydown

  ```js
  document.onkeydown=function(e){
      console.log(e.keyCode);//返回不同的键的码数
      console.log(e.ctrlKey);//判断按下的键是否为ctrl键
  }
  
  ```

* 键盘弹起keyup

  ```js
  document.onkeyup=function(){
      
  }
  
  ```

* 鼠标进入

  ```js
  box.onmouseover=function(){
      
  }
  
  ```

* 鼠标移出

  ```js
  box.onmouseout=function(){
      
  }
  
  ```

* 滚动事件

  ```js
  p.onscroll=function(){
      //卷入的高度
      console.log(p.scrollTop);
  }
  
  ```

  



### 对象的属性

* 属性：

  * 标准属性：
    * style

  ```js
              console.log(btn.style);//返回是style对象
  
              //获取
              console.log(btn.style.width);
  
              //设置
              btn.style.backgroundColor='red';
  
  ```

  * 开关属性
    * 值的状态只有两个 true false
    * disabled 设置是否禁用
    * checked 设置是否选择
    * selected 设置下拉框是否选择

* btn.value 是专门针对表单元素的标签 textarea 也尽量用value值进行获取

* innerHTML

  * 返回值为string类型

  * 可以识别html结构

    ```js
    btn.innerHTML='<li>新的元素</li>';
    
    ```

    

* 操作属性的方法：

  * 对属性进行增删改查

    * 获取属性getAttribute('属性名')

      * 参数：属性名
      * 返回值：属性值

      ```js
      box.getAttribute('abc');//可以获取标准属性和自定义属性，还可以获取自己定义的属性名
      
      
      ```

    * 设置属性setAttribute('属性名','属性值')

      * 参数：属性名和属性值

        ```js
        box.setAttribute('abc','234');
        
        ```

    * 删除属性removeAttribute('属性名')

      * 参数：删除的属性名

        ```js
        box.removeAttribute('属性名');
        
        ```

        

### 设置和获取类名

* 语法：

  ```js
  //获取
  console.log(box.className);
  //设置   原来的类名完全被覆盖
  box.className='e'；
  box.className+='bg_red';
  
  
  ```

###	classList

* 对类名进行增删改

  * 返回值：返回一个对象

* 添加类名：

  ```js
  btn.onclick=function(){
      div.classList.add('bg_red');
  }
  
  ```

* 删除类名

  ```js
  btn.onclick=function(){
      div.classList.remove('bg_red');
  }
  
  ```

* 切换类名

  ```js
  btn.onclick=function(){
      div.classList.toggle('bg_red');
  }
  
  ```



### 自定义属性

* 自定义属性命名：

  ```js
  //以data-开头进行命名
  <input type="button" data-src='./images/01.jpg'>
      
  
  ```

* 自定义属性获取

  ```js
  console.log(input.dataset);
  //返回一个对象
  console.log(input.dataset['src']);//input.dataset.src
  
  ```

* 函数内部有一个关键字 **this** 获取当前对象

  ```js
  var div=document.getElementById('box');
  div.onclick=function(){
      console.log(this);//div
  }
  
  ```

### 全选与反选案例

```js
        var allCk=document.getElementById(‘all)；
        var cks=document.getElementsByClassName('ck');
        allCk.onclick=function(){
            for(var i=0;i<cks.length;i++){
                cks[i].checked=allCk.checked;
            }
        }
        var is_checked;
        for(var j=0;j<cks.length;j++){
            cks[i].onclick=function(){
                is_checked=true;
                for(var i=0;i<cks.length;i++){
                    if(cks[i].checked==false){
                        is_checked=false;
                        break;
                       }
                }
                if(is_checked){
                    allCk.checked=true;
                }else{
                    allCk.checked=false;
                }
            }
        }

```



### 注册事件addEventListener

* 多次注册事件 不被覆盖

* 语法

  ```js
  btn.addEventListener('click',function(){
      
  })
  btn.addEventListener('click mouseenter',function(){
      
  })
  
  ```

* 小知识：

  ```js
  btn.click();
  //调用点击事件 不论按钮是以on+事件类型方式还是addEventListener注册的点击事件均可以使用此方式进行调用注册的点击事件
  
  ```

  

### 事件三个阶段

* 捕获：从外向里

* 到达目标

* 冒泡：从内向外 默认事件是在冒泡阶段执行的

  ```js
  box.addEventListener('click',function(){
      
  },false);//默认是false 表示冒泡阶段执行事件
  
  box.addEventListener('click',function(){
      
  },true);//true 表示捕获阶段执行事件
  
  ```

* 阻止冒泡

  ```js
  box.addEventListener('click',function(e){
      e.stopPropagation();
  },false)
  
  ```

### 事件对象

* 描述一次点击行为，看成是一个对象

* 属性和方法

  * 获取位置
    * 可视区域
      * e.clientX()；
      * e.clientY();
    * 页面左上角
      * e.pageX()
      * e.pageY()

  

  ![1568878061632](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1568878061632.png)

  * 获取目标对象

    * e.target

  * 获取绑定事件对象

    * e.currentTarget==this

  * 阻止浏览器默认行为

    * e.preventDefault()

    * return false;

      ```js
      document.oncontextmenu=function(){
          return false;
      }
      
      ```

      

### 获取元素位置

* 当子元素没有设置定位时

  ```js
  box.offsetLeft=父元素的边框+父元素的marginLeft+父元素的paddingLeft+子元素的marginLeft
  box.offsetTop=父元素的边框+父元素的marginTop+父元素的paddingTop+子元素的marginTop
  
  ```

  

* 当子元素设置定位

  ```js
  box.offsetLeft=left+marginLeft//无论是以谁定位
  box.offsetTop=top+marginTop//无论是以谁定位
  
  ```

* 获取元素位置的相对于哪个父亲

  box.offsetParent

  

  

### 跟着鼠标飞

* 想要东西飞起来就要设置脱标
  * position:absolute 绝对定位 相对于浏览器 也就是页面左上角 会随着滚动条的滚动而滚动
  * position:fixed  固定定位 相对于可视窗口区域 不会随着滚动条滚动而滚动
  * 所以：
    * 绝对定位和pageX、pageY搭配
    * 固定定位和clientX和clientY搭配，当然也可以和pageX和pageY搭配

### 事件解绑

* 当用on+事件类型进行解绑方式

  ```js
  btn.onclick=function(){
      btn.onclick=null;
  }
  
  ```

* 当用addEventListener事件进行解绑方式

  btn.addEventListener('click',function fn(){

  ​	btn.removeEventListener('click',fn);

  })

### 事件委托

* 当一些本身存在的子元素设置某些事件，但一旦父元素想办法进行添加一些新的子元素的时候，之前设置的子元素的某些事件就会失效，所以引入事件委托

* 为了让新增的子元素也有此事件的行为

* 给子元素的父元素注册事件 利用冒泡原理 实现父元素所有子元素注册事件

  ```js
  //e.target.nodeType:
  //节点标签：1
  //属性：2
  //文本：3
  
  //e.target.nodeValue
  //节点标签：null
  //属性:属性值
  //文本：文本内容
  
  //e.target.nodeName
  //节点标签：eg:LI
  //属性：小写属性名
  //文本：#text
  
  ul.addEventListener('click',function(e){
      if(e.target.nodeName=='LI'){
          alert('1');
      }
  })
  
  
  ```

### 修改、创建、添加节点

* 修改

  * 设置DOM节点内部html结构 识别HTML结构

  ```js
  		box.innerHTML='<a href="#">百度</a>';
  
  ```

  * 设置DOM节点内部的文本内容

  ```js
  		box.innerText='我是你爸爸';
  
  ```

* 创建节点

  * 只是在js中创建，在页面中不显示

    ```js
    var li=document.createElement('li');
    document.write();//识别html结构
    
    ```

* 添加节点

  * 在父元素的最后一个子元素后面添加

    ```js
    ul.appendChild(li);
    
    ```

  * 在指定位置添加子元素

    ```js
    ul.insertBefore(li,first);
    
    ```

### 发布微博

* 增删改 本地存储

### 通过节点获取节点

* 以下均为属性

  * 获取所有的子元素

  ```js
  		ul.children;//返回所有亲生子元素 伪数组
  
  ```

  * 获取亲生父元素

  ```js
  		li3.parentNode;
  
  ```

  * 获取兄弟元素

  ```js
  		li3.nextElementSibling;
  		li3.previousElementSibling;
  
  ```

  

  

### 删除节点

* 方法

  ```js
  ul.removeChild(first);
  
  ```

## BOM

### window及onload

* window是顶级对象

* window上大部分的属性和方法都是window调用的

  * 所有全局变量和函数都是window顶级对象上的属性和方法

    ```js
    window.a;
    var a;
    function fn(){}
    window.fn();
    
    ```

  * 隐式全局变量，不推荐使用

  * onload 等静态文件全部加在完成，其内部代码才进行执行

    ```js
    window.onload=function(){
        
    }
    
    ```

### 定时器

* 一次性定时器

  * 第一个参数：**等待**一定时间后执行的函数
  * 第二个参数：设置等待多久 毫秒
  * 返回值：清除定时器

  ```js
  var timer=setTimeout(function(){
      
  },1000)
  
  //清除定时器
  clearTimeout(timer);
  
  
  ```

* 永久定时器

  * 第一个参数：**等待**一定时间后执行的函数

  * 第二个参数：设置等待多久 毫秒

    ```js
    var timer=setInterval(function(){
        
    },1000)
    //清除定时器
    clearInterval(timer);
    
    ```

### BOM的location

* BOM上的一个属性 重新指定浏览器的地址栏上的地址 页面就会进行跳转

  ```js
  location.href='http://www.baidu.com';
  //必须加协议http://
  
  
  ```

### BOM的localStorage

* 用于将一些数据进行本地存储

* 返回对象

  * setItem设置本地数据

    ```js
    locaStorage.setItem('a',a);
    
    ```

  * getItem获取本地数据

    ```js
    localStorage.getItem('a');
    //获取不存在的数据 返回null
    
    ```

  * removeItem删除本地数据

    ```js
    localStorage.removeItem('a');
    
    ```

  * 全部清空

    ```js
    localStorage.clear();
    
    ```

### JSON

* 因为本地数据存储为字符串格式，当遇到一些对象时，需要转换为字符串，因此BOM提供其JSON格式的字符串的转换

* 一般格式(字符串 数字)

* 所有的键和使用双引号包起来

* 字符串也用双引号包起来

  ```js
  var arr=[
      {
          info:"",
          
      }
  ]
  
  ```

* 把对象转换为JSON格式的字符串

  * 参数：对象

  * 返回值：JSON格式的字符串

    ```js
    var str=JSON.stringify(arr);
    //存入本地时候，对于复杂类型的数据进行转换字符串
    
    ```

* 把JSON格式的字符串转换为对象

  * 参数：JSON格式的字符串

  * 返回值：对象

    ```js
    var arr=JSON.parse(str);
    
    
    ```

### 获取DOM节点的样式

* 只能获取行内样式

  ```js
  div.style.left;
  
  ```

* BOM中的getComputedStyle

  * 参数是DOM节点

  * 返回值：返回DOM节点的样式对象

    ```js
    window.getComputedStyle(box).width;
    
    ```

* 返回盒子的实际宽度和高度

  * width=content+padding+border

  * height=content+padding+border

  * 返回值：数字类型

    ```js
    box.offsetWidth;
    box.offsetHeight;
    console.log(box.style.width);//返回字符串 eg:120px; 只能获取行内元素 可以进行获取和设置
    console.log(box.offsetWidth);//返回数字 eg:120;只能进行获取不能设置 获取行内和css内部的样式 获取盒子真实宽度
    console.log(window.getComputedStyle(box).width);//返回字符串 eg:120px 返回的就是盒子的内容区域 只能进行获取 可以获取行内和css样式里的样式
    console.log(box.clientWidth);//返回数字，eg:100 返回的是盒子的可视区域的宽度，即width+padding 可以获取行内和css内部的样式
    
    ```

    

## tab栏

* 排他功能
* 自定义属性的使用

## 手风琴

* 排他功能

## 旋转木马

* 利用数组存储类名，在每次点击按钮时候，进行转换数组的顺序，使图片的类名重新进行赋值
* 点击右键 数组的操作是，删除第一个，进行添加数组的后面
* 点击左键 数组的操作时 删除最后一个 进行添加数组的前面

## 360开机动画

* 只能使用addEventListener注册事件

* 动画设置无限播放，下面的事件不会生效

* animationend

  ```js
  ul.addEventListener('animationend',function(){
      console.log('动画已经执行完');
  })
  
  ```

  

* transitionend

```js
ul.addEventListener('transition',function(){
    console.log('过渡已经执行完');
})

```



## 放大镜

* 比例计算

![1569330592598](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1569330592598.png)



## 事件对象-触摸事件

* 移动端

* 推荐使用addEventListener注册事件

* 

  * 触摸开始

    ```js
    box.addEventListener('touchstart',function(e){
        console.log(e.touches);//获取屏幕上所有的触摸点
        console.log(e.targetTouches);//获取元素上的触摸点
        console.log(e.changedTouches);//变化后的触摸点，获取离开屏幕上时的最后的点
    })
    
    ```

  * 触摸移动

    ```js
    box.addEVentlistener('touchmove',function(e){
         console.log(e.touches);//获取屏幕上所有的触摸点
        console.log(e.targetTouches);//获取元素上的触摸点
        console.log(e.changedTouches);//变化后的触摸点，获取离开屏幕上时的最后的点
    })
    
    ```

  * 触摸结束

    ```js
    box.addEventListener('touchend',function(e){
         console.log(e.touches);//获取屏幕上所有的触摸点
        console.log(e.targetTouches);//获取元素上的触摸点
        console.log(e.changedTouches);//变化后的触摸点，获取离开屏幕上时的最后的点
    })
    
    ```

## 封装tap手势

* 思路：
  * 获取开始触摸时的位置及时间，判断屏幕上所有的触摸点为1
  * 获取离开屏幕时的位置及时间，判断离开时候变化的触摸点数为1
  * 进行计算时间差和位置差，然后设置的标准进行比较，如果符合进行执行回调函数

## zepto类库引入

* 语法类似于jQuery

  * 获取节点对象

    ```js
    var div=$('div');
    
    ```

  * 设置样式

    ```js
    box.css({
        width:'500px'
    })
    
    ```

  * 绑定事件

    ```js
    box.on('click',function(){
        
    })
    box.click(function(){
        
    })
    
    ```

  * 添加子元素

    ```js
    box.append('<a href="#">百度</a>');
    
    ```

  * 显示或者隐藏

    ```js
    box.show();//显示
    box.hide();//隐藏
    //对于设置毫秒值的参数的时候，对于jQuery比较适用
    
    ```

* 手势一些模块分开进行引入

### touch.js的引入

* 点击事件

  ```js
  box.on('tap',function(){
      
  })
  
  ```

* 左滑

  ```js
  box.on('swipeLeft',function(){
      
  })
  
  ```

* 右滑

  ```js
  box.on('swipeRight',function(){
      
  })
  
  ```

## 轮播图

## 轮播图-无缝滚动

* 利用过渡执行结束事件以及定时器的控制是否有过渡，实现无缝滚动的效果

## swiper插件

* 语法：

  ```html
  <!--引入css和js文件-->
  <div class='swiper-container'>
      <div class='swiper-wrapper'>
          <div class='swiper-slide'>
              <a href='#'>
              	<img src=''>
              </a>
          </div>
      </div>
      <!--如果需要分页器-->
      <div class='swiper-pagination'>
          
      </div>
      <!--需要导航按钮-->
      <div class='swiper-button-prev'>
          
      </div>
      <div class='swiper-button-next'>
          
      </div>
      <!--需要进度条-->
      <div class='swiper-scrollbar'>
          
      </div>
  </div>
  
  ```

  

  ```js
  var mySwiper=new Swiper('.swiper-container'{
             //过渡执行时间
               speed:200,
             //形成闭环
                loop:true,
             //自动播放
                 autoplay:true,
                 navigation:{
                      nextEl:'.swiper-button-next',
                      prevEl:'.swiper-button-prev'
  
                },
                  pagination:{
                      el:'.swiper-pagination'
                  },
                  scrollbar:{
                         el:'.swiper-scrollbar',
                   }
  
  })
  
  ```

  



```js

```

