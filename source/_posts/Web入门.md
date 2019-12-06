---
title: Web入门
date: 2018-12-03 09:33:09
top:
categories:
   - 学习
   - Web入门
tags: Web入门
---

# HTML

## 1. HTML骨架结构

```html
<!-- 声明文档类型,告诉浏览器按照哪个版本的html解析 -->
<!DOCTYPE html>
<html lang="en">
    <!-- lang=zh-CN 用于搜素引擎看的 -->
<head>
    <meta charset="UTF-8">
    <!-- 元信息 不是给用户看的 给搜索引擎和浏览器看的
        charset 字符集
		unicode 万国码
		gb2312 中文简体
		big5 中文繁体
		GBK 中间简体和中文繁体
    -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- <title>Document</title> 标签页会显示的信息 -->
</head>
<body>
    
</body>
</html>
```

## 2. 排版标签

* 标题标签h1~h6 字体加粗 上下生成空白行, h1在一个页面上只能使用一次,多次使用不符合w3c标准,不利于页面搜索引擎`seo`优化
* 段落标签` p` 上下生成空白行
* 水平线`hr`
* 换行`br`

## 3. 文本格式化标签

* 加粗`strong / b`
* 斜线`em / i`
* 下划线`ins / u`
* 删除线`del / s`
* 上标/下标`sup / sub`

## 4. 图片标签

* src  图片来源
* alt  图片不显示的时候显示的文字 替换文本
* title  提示文本 鼠标悬停到图片上显示的文字
* width 宽
* height 高
* border 边框

```html
<body>
    <img src="./Fshiqian.jpg"
    alt="图片"
    title="文本"
    width="300"
    height="500"
    border="5"/>
</body>
```

## 5. 超链接

* herf 跳转目标
* target 打开方式
  * _blank 在新窗口打开(原页面不关闭)
  * _self 在新的窗口打开(原页面关闭)

```html
	<a href="http://baidu.com" target="_blank">百度</a>
	<a href="http://baidu.com" target="_self">百度</a>
	<a href="#">什么鬼</a>
```

## 6. base

* 控制页面所有的超链接是以什么方式打开
* 放在head里面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
+   <base target="_blank" />
    <title>Document</title>
</head>
<body>
    <a href="http://baidu.com">百度</a>
    <a href="#">什么鬼</a>
</body>
</html>
```

## 7. 锚点

* 同页面

```html
<a herf="#test">测试</a>
....
<h3 id="test">测试接收</h3>
```

* 不同页面

```html
a href='test.html#test'>测试</a>

<!--另一个页面test.html-->
<h3 id='test'>
    测试接收
</h3>
```

## 8. 特殊字符

```html
<!--
&lt; <
&gt; >
&copy;©
&reg;®
&amp;&
&times;x
&divide;÷
&plusmn;±
&degree;°
&sup2;²
&sup3;³
&yen;￥
-->

```

## 9. 注释

* Ctrl + /

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
    <!-- <p>注释样式</p> -->
</body>
    <script>
        // script中注释样式
    </script>
</html>
```

## 10. 路径

* 相对路径

```html
<img src="./Fshiqian.jpg" alt="">
```

* 句对路径

  * 本地盘符

  ```html
  <img src="D:\QD\新建文件夹\代码\Fshiqian.jpg" alt="">
  ```

  * 网络盘符(互联网)

  ```html
  <img src="http://Fshiqian.jp.jpg" alt="">
  ```

## 11. 浏览器

* 见的五大浏览器：谷歌、火狐、ie、opera、safari
* 浏览器内核：渲染引擎和js引擎
* 常见浏览器内核：Trident(ie)、Webkit(safari)、Presto(opera)、chromium/Blink(chrome）、Gecko(firefox)
* 对于移动端：Android-webkit、IOS/wp7-safari或者ie的TrWeb标准：html(结构)+css(样式)+javascript(行为)ident
* Web标准：html(结构)+css(样式)+javascript(行为)

## 12. div和span区别

* div占一行	span在一行内显示

## 13. 列表

* 无序列表

```html
<!--
	ul连不能直接写文字和标签，ul只能嵌套li
	li外面必须有父元素ul或者ol li里面可以嵌套任意标签
-->
<ul>
    <li>元素</li>
    <li>
    	<p>嵌套</p>
    </li>
</ul>

```

* 有序列表

```html
<!--
	ol连不能直接写文字和标签，ol只能嵌套li
	li外面必须有父元素ul或者ol li里面可以嵌套任意标签
-->

<ol>
    <li>新闻</li>
</ol>
```

* 自定义列表

```html
<dl>
    <dt>自定义列表标题</dt>
    <dd>解释项1</dd>
    <dd>解释项2</dd>
</dl>

```

## 14.表格

* 语法

```html
<table>
    <!--tr外边必须有父元素table,tr里面只能嵌套td和th(表头)，td里面可以嵌套任意元素-->
    <tr>
    	<td>单元格</td>
        <td>单元格</td>
        <td>单元格</td>
    </tr>
    <tr>
    	<td>单元格</td>
        <td>单元格</td>
        <td>单元格</td>
    </tr>
</table>

```

* 表格属性
  * border 边框
  * 边框与内容之间距离 cellpadding，默认值1
  * 边框与边框之间距离 cellspacing，默认值2
  * 表格宽度 width
  * 表格高度 height
  * 水平对齐方式 align=center/left(默认)/right
  * 设置在表格上，整张+表格水平对齐方式
  * 设置在tr和td上，里面内容水平对齐方式
* 表格的标题和表头

```html
<table>
    <caption>我是标题</caption>
    <tr>
        <!--里面文字加粗居中-->
    	<th>表头</th>
    </tr>
    <tr>
    	<td>单元格</td>
    </tr>
</table>
```

* 结构

```html
<table>
    <!--
	thead tbody 不代表行或者列，是给表格分成2部分，使表格更有序，增强语义化，更好的seo
-->
    <thead>
    	<tr>
        	<th>表头1</th>
            <th>表头2</th>
            <th>表头3</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<td>单元格</td>
            <td>单元格</td>
            <td>单元格</td>
        </tr>
    </tbody>
</table>
```

* 合并单元格

  * colspan 合并列
  * rowspan 合并行

  ```html
  <table>
      
      <tr>
      	<td rowspan='2'>1</td>
          <td>2</td>
          <td>3</td>
      </tr>
      <tr>
          <td>2</td>
          <td>3</td>
      </tr>
  	<tr>
      	<td colspan='2'>1</td>
          <td>3</td>
      </tr>
  
  </table>
  
  
  ```

## 15. 表单

* form 表单域

* action 手机信息提交给哪个文件处理

* name 表单域的名称

* method 传递信息的方法

* method=‘get’ 默认值 通过浏览器的地址栏进行传递信息 post

* 表单控件

  * 单行文本输入框

  ```html
  <input type='text' value='孙子' name='username' maxlength='字符长度' size='宽'>
  
  ```

  * 密码框

  ```html
  <input type='passward'>
  
  ```

  * label使用（点击文字，input获取焦点）

  ```html
  <label for='user'>昵称：<input type='text' id='user'>
  
  ```

  * 单选框

  ```html
  <input type='radio' name='sex' id='female'>女
  <!--
  	checked默认选择状态
  -->
  <input type='radio' name='sex' id='male' checked='checked'>男
  
  ```

  * 多选框

  ```html
  <input type='checkbox' >爸爸
  <input type='checkbox'>密码
  ```

  * 下拉菜单

  ```html
  <select>
      <!--
  	selected 设置默认选择
  -->
      <option selected='selected'>1995</option>
      <option>1996</option>
      <option>1997</option>
  </select>
  ```

  * 文件域

  ```html
  <input type='file'>
  ```

  * 文本域

  ```html
  <textarea col='一行字符的个数' rows=''></textarea>
  ```

  * 按钮

  ```html
  <input type='submit' value='提交'>可以提交
  <input type='reset' value='重置'>
  <input type='button' value='按钮'>不可提交
  <button>按钮</button> 可以提交
  ```

  

