---
title: jQuery
date: 2019-12-04 09:59:26
top:
categories:
   - 学习
   - jQuery
tags: jQuery
---

# jQuery

## 体验jQuery

* 引入jQuery文件

* 入口函数

  ```js
  $(function(){
      
  })
  
  $(document).ready(function(){
      //js版本
      var div=document.querySelector('div');
      div.style.display='none';
      
      //jQuery版本
      //先获取div
      //隐藏div
      var myDiv=$('div');
      myDiv.hide();
  })
  ```

## $符号

```js
$(function(){
    alert('你好');
})
jQuery(function(){
    alert('你好');
})
```



## jQuery对象

```js
//通过原生js获取div
var myDiv=document.querySelector('div');
console.dir(myDiv);//以对象形式将元素展示在控制台

//使用jQuery的方式
$(function(){
    //获取div
    var myDiv=$('div');
    console.dir(myDiv);
})
```



## DOM对象与jQuery对象的转换

* jQuery对象转化为DOM对象

  ```js
  var div=$('div');
  div[0];
  div.get(0);
  ```

  

* DOM对象转化为jQuery对象

  ```js
  var div=document.querySelector('div');
  $(div);
  ```

## jQuery对象

### 通过选择器获取jQ对象



```js
        $('选择器');//获取jQuery对象
        $('.first');
        $('#two');
        $('li:nth-child(3)');

        //jQ中的方法获取页面中的元素
        $('li:first');
        $('li:last');
        $('li:eq(2)');//索引从0开始
        $('li:odd');//索引值为奇数
        $('li:even');//索引值为偶数
        //作为比较，写在css内部
        li:nth-child(odd){}
        li:nth-child(even){}


```

### jQ获取元素的其他方式

* 获取当前元素的父元素

  ```js
  $('span').parent();//上下级父亲
  $('span').parents(['选择器']);//获取元素的所有父元素（可以获取指定父元素）
  
  ```

* 获取子元素

  ```js
  $('li:nth-child(3)').children(['选择器'])；//获取当前元素的所有直接的（子代）子元素，可以获取指定的子元素
  $('li:nth-child(3)').find(['选择器']);//获取当前元素的所有的（后代）子元素，可以获取指定的子元素，但是，一般基本上加参数
  ```

* 获取兄弟元素

  ```js
  $('p').siblings(['选择器']);//获取当前元素的所有的兄弟元素，可以获取指定的兄弟元素
  $('p').nextAll();//获取当前元素的后面的所有的兄弟元素
  $('p').prevAll();//获取当前元素的前面的所有的兄弟元素
  
  
  ```

* 判断当前元素是否有某个类名

  ```js
  $('li').hasClass('one');
  
  ```

* 获取索引值为n的元素

  ```js
  $('span').eq(n);
  
  ```

### 给jQ对象设置样式

```js
$('li').css('backgroundCOlor','red');//注意此处的属性名需要使用引号引起来
$('li').css({
    backgroundColor:'red',
    color:'green'
});//存在隐式迭代

```



## jQ对象绑定事件

* 鼠标移入事件mouseenter

  ```js
  $('div').mouseenter(function(){
      
  });
  //js基础学过的mouseover事件，也是鼠标移入事件，但是两者是有细微的差别，mouseenter没有冒泡
  
  ```

  

* 鼠标移出事件mouseleave

  ```js
  $('div').mouseleave(function(){
      
  })//mouseout
  
  ```

  

## 新浪导航

* 获取当前元素的索引值

  ```js
  $(this).index();
  
  ```

* 滑入滑出（后面会介绍）

  ```js
  $(this).slideUp();
  $(this).slideDown();
  
  ```

## 排他思想

* 语法：

  ```js
  $(this).css({color:'red'}).siblings().css({color:''
  })//链式变成
  
  ```

## 操作类的方式操作标签的样式

* 添加类名

  ```js
  $('div').addClass('box test');
  //注意：此处添加多个类名和js中的clasList的add()方法有区别，此处用空格，而add()方法是通过逗号进行添加多个类名
  
  ```

* 删除类名

  ```js
  $('div').removeClass();//不写参数表示移除全部类名
  $('div').removeClass('test');
  
  
  
  ```

* 切换类名

  ```js
  $('div').toggleClass('test')
  
  ```

## jQ操作元素的动画效果

### 显示与隐藏

* hide([speed,easing,fn])
  * 隐藏
  * 参数1：slow fast normal 毫秒值
  * 参数2：linear swing
  * 参数3：function(){}
* show([speed,easing,fn])
  * 显示
  * 参数与hide()的参数一样
* toggle([speed,easing,fn])
  * 切换
  * 参数与hide()的参数一样

### 滑动动画

* slideDown([speed],[easing],[fn])
  * 改变高度进行显示
  * 参数与hide()方法一样
* slideUp([speed,easing,fn])
  * 改变高度进行隐藏
  * 参数与hide()方法一样
* slideToggle([speed,easing,fn])
  * 改变高度进行切换显示和隐藏
  * 参数与hide()方法一样

### 淡入淡出

* fadeIn([speed,easing,fn])
  * 改变透明度进行显示
  * 参数和hide()一样
* fadeOut([speed,easing,fn])
  * 改变透明度进行隐藏
  * 参数和hide()一样
* fadeTo(speed,opacity,[easing],[fn])
  * 显示的透明度的程度
  * 其中opacity为必写属性，但是speed也是需要设置的
* fadeToggle([speed,easing,fn])
  * 改变透明度进行切换
  * 参数和hide()一样

### 自定义动画

* 语法：

* 参数1：param

* 参数2：speed

* 参数3:easing

* 参数4：fn

  ```js
  $(this).animate({
      width:300,
      //其中不能设置有关颜色的信息，需要后期引入插件才能进行实现
  })
  
  ```

## 动画排队

* stop()

  ```js
  $(this).stop().animate({
      width:400,
  });
  //一般加在动画的前面，更好的优化，停止当前正在执行的动画，以当前状态动画进行执行动画
  
  ```

## 操作标签的属性

* 操作固有属性

  ```js
  console.log($('div').prop('class'));//获取  	
  $('div').prop('class','one');//设置
  //其中设置开关属性的页通过prop设置和获取
  console.log($('div').prop('checked'));
  $('div').prop('checked',true);
  
  
  ```

* 获取自定义属性

  ```js
  console.log($('div').attr('myname'));//获取不是以data-开头的自定义属性
  console.log($('div').attr('data-age'));//获取以data-开头的自定义属性
  console.log($('div').attr('id'));//也可以获取固有属性
  $('div').attr('name','lxh')
  
  
  ```

* 操作缓存数据

  ```js
  //程序中，将数据保存下来的方式
  //变量，数组，对象，本地存储，自定义属性
  $('div').data('myage',180);//随着刷新将会消失
  //也可以获取data-开头的自定义属性
  
  ```

  

## 实现全选效果

* 小知识：

  ```js
  $('.ck input:checked');//获取所有选中的元素
  //通过程序的方式实现数据博村两位小数
  var total_money=total_money.toFixed(2);
  //实现用户手动输入修改对应的总价
  $('.i_number input').change(function(){})
  
  ```

* 设置和获取表单控件的值

  ```js
  $('input').val();
  $('input').val('值')
  
  ```

* 设置和获取普通标签中的值

  ```js
  $('div').html()//获取div内部的html结构文本内容 类似于innerHTML
  $('div').text()//获取div内部的文本内容 类似于innerText
  $('div').html('<span>我是一个span标签</span>');//设置div内部的html结构
  $('div').text('我是文本');//设置div内部的文本内容
  
  ```

* 遍历jQ对象

  * 第一种

    ```js
    $('li').each(function(index,domElement){
        console(index,domElement);//index为索引 domElement为dom对象
    })
    
    
    ```

  * 第二种

    ```js
    $.each($('li'),function(index,domElement){
        console.log(index,domElement);//index为索引 domElement为dom对象
        //此种遍历方式一般用于遍历数据，一般遍历页面中的元素使用第一种
    })
    
    ```

* 通过jQ对象创建元素

  ```js
  var span=$('<span>我是新创建的span</span>');//创建span标签
  $('div').html('html标签');
  //添加子元素
  $('div').append(span);//添加到div内部的最后面
  $('div').prepend(span);//添加到div内部的最前面
  
  //添加兄弟元素
  $('div').after(span);//添加到div的后面
  $('div').before(span);//添加到div的前面
  
  ```

* 删除元素

  ```js
  $(this).remove();//删除当前的元素
  $(this).empty();//删除当前元素的所有内部子元素
  $(this).html('');//删除当前元素的内部的html结构文本内容
  
  ```


## jQ方式获取元素大小和位置

* 获取元素大小
  * jQ对象.width()	获取宽度
  * jQ对象.height()       获取高度
  * jQ对象.innerWidth()    获取width+padding
  * jQ对象.innerHeight()    获取height+padding
  * jQ对象.outerWidth()      获取width+padding+border
  * jQ对象.outerHeight()         获取height+padding+border
  * jQ对象.outerWidth(true)     获取width+padding+border+margin
  * jQ对象.outerHeight(true)          获取height+padding+border+margin
* 设置元素大小
  * jQ对象.width(值)//不带单位
  * jQ对象.height(值)

## 获取元素元素位置

* offset	与父元素无关，获取当前元素相对于整个文档的位置

  ```js
  $('.one').offset()//返回一个对象
  $('.one').offset().left;
  $('.one').offset().top;
  
  ```

* position        如果当前父元素没有定位，那么参照整个页面，如果当前父元素有定位，直接参照父元素

  ```js
  $('.one').position();//返回一个对象
  $('.one').position().left;
  $('.one').position().top;
  
  ```

## 获取元素滚动出去的距离

* 给浏览器注册滚动事件

  ```js
  $(window).scroll(function(){
      $('html').scrollTop();
  })
  
  ```

* 文档没有animate方法，只有页面中的元素才有animate，其中animate中有一个属性scrollTop属性

## 通过on的方式给元素注册事件

* 一个对象可以同时注册多个事件

  ```js
  $('div').on('事件类型',function(){
      $(this).css('backgroundColor','red');
  })
  $('div').on({
      '事件类型':function(){
          
      },
      '事件类型':function(){
          
      }
  })
  
  ```

## 通过on注册委托事件

* 语法：

  ```js
  $('.box').on('click','.one',function(){
    //使.box内部的子元素.one有点击事件  
  })
  
  ```

## 解绑事件

* jQ对象.off()//解绑所有注册的事件
* jQ对象.off('mouseenter') 解绑鼠标进入事件
* jQ对象.off('事件类型','选择器') 解绑委托事件

## one事件

* 语法

  ```js
  $('.one').one(function(){
      //只执行一次
  })
  
  ```

## 自动触发事件

* 方式1：

  ```js
  $('div').click();
  
  
  ```

* 方式2：

  ```js
  $('div').trigger('click');
  
  ```

* 方式3：

  ```js
  $('div').triggerHandler()//默认行为不执行
  
  ```

  

* 小知识：

  ```js
  //自调用函数：让函数自己调用自己
  (function f2(){})()
  
  
  ```

## jQ中的事件对象

* 事件对象参数：与js基础中学习的基本一样
* 只不过可以不用设置参数直接使用event可以

## 拷贝对象

* 语法：

  ```js
  $.extend(obj1,obj2);
  //第一个参数，是布尔类型，默认为false,表示浅拷贝
  //第二个参数：目标拷贝对象
  //第三个参数：被拷贝的对象
  
  
  $.extend(true,obj1,obj2);
  //第一个参数，是布尔类型，表示深拷贝
  //第二个参数：目标拷贝对象
  //第三个参数：被拷贝的对象
  
  ```

* 总结：

  * 不管是深拷贝还是浅拷贝，如果原来对象中有一个和被拷贝对象相同的属性，会被覆盖掉
  * 不管是深拷贝还是浅拷贝，如果原来对象中不存在与被拷贝对象相同的属性，不会被覆盖掉
  * 如果是浅拷贝，那么拷贝过程中，遇到的是对象，是将对象的地址赋值给目标对象
  * 如果是深拷贝，那么在拷贝过程中，是直接将对象赋值一份拷贝给当前对象

## 多库共存

```js
var getelement=jQuery.noConflict();
getelement('div');//获取jQ对象

```



## 插件

* 先引入jquery文件，再引入插件

### 全屏滚动插件

```html
<div id='fullPage'>
    
    <div class='section'>
        第一
    </div>
    <div class='section'>
        第二
    </div>
    <div class='section'>
        第三
    </div>
</div>
<script src='jquery.js'></script>
<script src='jquery.fullPage.js'></script>


```



```js
$(function(){
    $('#fullPage').fullpage({
        sectionsColor:['red','green','pink']
    })
})

```

### 懒加载

```html
<img class='lazy' data-original='01.jpg'>
<script src='jquery.js'>
</script>
<script src='jquery.lazyload.js'></script>

```



```js
$(function(){
    $('img.lazy').lazyload();
})

```



## todoList案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <header>
        <section>
            <label for="title">todoList</label>
            <input type="text" value="" id="title">
        </section>
    </header>
    <section>
        <h2>正在进行</h2>
        <ol></ol>
    </section>

    <section>
        <h2>已经完成</h2>
        <ul></ul>
    </section>


    <script src="./js/jQuery.min.js"></script>
    <script>
        $(function () {

            // 调用加载数据的方法
            loadDate();
            // 1.先创建一条数据：如果原来就有数据，在原来数据基础上在追加一条新的数据，否则直接创建一条数据

            // 1.1先给输入框注册一个键盘事件
            $('#title').keydown(function (e) {
                // 先要明确用户按下的是回车键
                // console.log(e.keyCode);
                if (e.keyCode == 13) {
                    // 获取当前输入框中的值
                    var input_v = $(this).val();

                    // 获取本地存储中的数据

                    var list = getDate();
                    //    将输入框中的值直接添加到list中
                    // list.push(input_v);
                    list.push({
                        listname: input_v,
                        ischeck: false,
                    })
                    // 将新的数据再次存入到本地存储中
                    var str = JSON.stringify(list);
                    localStorage.setItem('todoList', str);

                    // 动态渲染标签：有几条数据就创建几个标签
                    loadDate();
                }

            })

            // 获取本地存储中国的数据
            function getDate() {
                var list = localStorage.getItem('todoList');
                if (list != null) {
                    //    如果有数据 那么就将原来数据转化为数组

                    return JSON.parse(list);
                } else {
                    //    localStorage.setItem('todoList','[]');
                    return [];
                }
            }
            //动态渲染标签 （动态创建标签）
            function loadDate() {
                // 获取本地存储的数据
                var list = getDate();
                // 为了避免重复加载，先将ol中的内容清空
                $('ol,ul').empty();
                
                // 动态遍历list 然后创建标签
                $.each(list, function (i, item) {
                    if (item.ischeck) {
                        // console.log(i,item);
                        // 创建li
                        var li = $('<li><input type="checkbox" checked><p>' + item.listname + '</p><a href="javascript:;" aindex="' + i + '">删除</a></li>');
                        $('ul').prepend(li);
                    } else {
                        // console.log(i,item);
                        // 创建li
                        var li = $('<li><input type="checkbox"><p>' + item.listname + '</p><a href="javascript:;" aindex="' + i + '">删除</a></li>');
                        // 将该标签添加到ol中
                        $('ol').prepend(li);
                    }


                })
            }

            // 实现删除效果
            $('ol,ul').on('click', 'a', function () {
                // 实现将本地存储的数据删除
                // console.log($(this
                // ).index());

                var list = getDate();


                // 获取自定义属性值
                // console.log($(this).attr('aindex'));
                var index = $(this).attr('aindex');

                // 从数组中删除一条数据
                list.splice(index, 1);

                // 重新将数据更新到本地存储中
                localStorage.setItem('todoList', JSON.stringify(list));

                // 重新加载数据
                loadDate();

            })

            // 实现状态修改
            $('ol,ul').on('click', 'input', function () {
                // 获取对应索引值
                var index = $(this).siblings('a').attr('aindex');
                console.log(index);

                // 获取本地存储的数据
                var list = getDate();

                // 修改
                list[index].ischeck = $(this).prop('checked');

                // 将数据更新到本地存储中
                localStorage.setItem('todoList', JSON.stringify(list));

                // 重新加载数据
                loadDate();


            })
        })
    </script>
</body>

</html>

```







