---
title: 动画、响应式、flex
date: 2019-12-04 09:46:34
top:
categories:
   - 学习
   - 动画、响应式、flex
tags: 动画、响应式、flex
---

## 2D转换

### 位移translate

* 与定位区别：

  * 定位会脱标，可能影响其他盒子的位置
  * 定位会使行内元素转换为行内块元素

* 使用：

  * transform:translateX(),translateY() translate()
  * transform:translate(50px,50px)
  * transform:translate(100%,50%);相对于盒子自身宽高
  * 正值相对于x,y轴正方向进行移动

* 重点：居中方案

  ``` css
          div{
              position:absolute;
              left:50%;
              top:50%;
              transform:translate(-50%,-50%);
          }
          基础班：
          div{
              position:absolute;
              left:50%;
              top:50%;
              margin-left:-盒子本身宽度的一半;
              margin-top:-盒子本身高度的一半;
          }
          div{
              //前提是盒子要设置宽度（手动），否则无效
              position:absolute;
              left:0;
              top:0;
              bottom:0;
              right:0;
              margin:auto;
          }
  ```

  

### 旋转rotate

* 使用：
  * transform:rotate(45deg);正值顺时针
* 小知识：
  * 伪元素：字体图标或者手动制作小图标使用 **行内元素**
    * 只能用在双标签上
    * 伪元素后面不能紧跟伪类 正确写法：div:hover::after
  * 百分比：
    * 定位：相对于父级元素
    * 背景大小：相对于当前元素
    * 位移：相对于自身宽高‘
    * 宽高：相对于父级元素

### 转换中心

* 使用：

  transform-origin:200px 200px;

  transform-origin:0 100%;

  transform-origin:left bottom;

  transform-origin:0; 第二格参数默认为50%



### 缩放scale

* 使用：

  transform:scale(2，0.5)；//长宽方向使用一个缩放比

* **注意：**

  * 后面所有属性都不会影响其他盒子的位置（tranform特点）
  * 缩放，使下面的文字，css属性，子元素都会跟着缩放

  

  

### tranform简写

* 使用：
  * transform:translate() rotate() scale() 一般情况下，移动写在旋转的前面，反之可能会改变初始轴的方向



## 动画

* 使用：

  * 定义动画：

  ``` css
          @keyframes dong_hua{
              from{
  
              }
              to{
  
              }
          }
  
  ```

  

  * 定义动画序列：

  ``` css
          @keyframes dong_hua{
              0%{
  
              }
              50%{
  
              }
              100%{
  
              }
          }
  ```

  * 调用动画

    ​	animation:animation-name animation-duration;

* 注意：变化一定是基于上一个状态的，注意层叠出现

* 属性：

  * animation-name:dong_hua 动画名称
  * animation-duration:1s; 执行时间
  * animation-timing-function:linear;速度变化,其中有个拆分步骤steps(n)
  * animation-delay:1s ; 动画延迟
  * animation-iteration-count:infinite; 循环次数
  * animation-diretion:alternate; 循环方向
  * animation-fill-mode:forwards/backwards/both;动画等待结束状态
  * animation-paly-state:paused/running;动画播放状态 

## 3D转换

### 景深

* perspective:500px;近大远小
* 一般加在body上
* 值越小，变化越剧烈

### 位移translate3d

* 使用：与2d基本相同
* 注意：z轴移动

### 旋转rotate3d

* 使用：与2d基本相同

* 左手定律

* 注意：z轴方向屏幕垂直向外

* 自定义轴向

  transform:rotate3d(1,1,0,45deg)

### 缩放scale3d

* 使用：基本与2d相同
* 注意：z轴无效果



### transform简写

* 与2d基本相同

### 开启3D转换

* 给做3d转换的元素的亲生父亲开启空间：tansform-style:preserve-3d





## 流式布局

* 百分比布局+二倍图

### viewport

* 设置

  <meta name='viewport' content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">

### background-size

* 使用：

  background-size:100%;当前盒子宽度

  background-size:contain/cover;

### 二倍图

### css3盒子

* box-sizing:border-box
* 应用场景：
  * 左固定，右侧拉伸
  * 左右固定，中间拉伸

### margin的使用

* 只要没有给盒子宽度，设置外边距不会撑宽盒子，只会往内挤

### 设置定位

* 设置定位的盒子，宽度百分比100%会失效（转换为行内块元素）
* 使用定位，不设置偏移量将会按照原来位置进行脱标

### 京东

```css
//必须是n+2,不能顺序颠倒，其中n从0开始
a:nth-child(n+2){
    
}
```

##  flex布局

* 伸缩布局，弹性布局，伸缩盒布局，弹性盒布局
* 等比
* display:flex;
* vertical-align,clear,float失效

### 容器属性

* flex-direction:row/column主轴方向设置
* justify-content:flex-start/flex-end/center/space-round/space-between控制子元素在主轴上排布方式
* flex-wrap:wrap/nowrap;是否换行；默认不换行，当子元素设置宽度，会进行合理压缩
* flex-flow:flex-direction/flex-wrap
* align-items:flex-start/flex-end/center/stretch;控制子元素侧轴对齐方式（其中子元素只有一行）
* align-content:flex-start/flex-end/center/space-round/space-between/stretch控制子元素侧轴对齐方式（其中子元素为多行）

### 项目属性

* flex:设置百分比或者份数
* align-self:控制单独子元素侧轴上对齐方式
  * 注意：
    * 默认值是auto,当父元素设置align-items或者align-content,会继承父元素值，当父元素没有设置，值为stretch
* order设置子元素的排列，值越小，越靠前

## rem布局

* 等比变化

* 1em=父亲字体大小

* 1rem=html字体大小

* 媒体查询

  ```css
  @media screen and|not|only (min-width:750px){
      //宽度在width>=750px;
      css-code
  }
  ```

* 档位划分

* rem+媒体查询

* rem布局+flex布局+媒体查询（flexible.js）其中css用less

* lesss相关语法：

  * 定义变量

    ```css
    @color:green;
    ```

    

  * 嵌套

    ```css
    .father{
    
        .son{
            
        }
        &:hover{
            
        }
    
    }
    ```

  * 运算

    * 单位：	
      * 两个不同单位，选择前面的单位
      * 使用同一个单位，单位就是这个单位

## 响应式布局

### 版心

* 0-768px xs
* 768-992px sm
* 992-1200px md
* 1200--无穷大 lg



### Bootstrap布局

```html
    <!DOCTYPE html>
    <html lang="zh-CN">
      <head>
        <meta charset="utf-8">
        <!-- 要求 当前网页 使用 IE浏览器 最高版本的内核 来渲染 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">

        <!-- 视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放 -->
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <title>Bootstrap Template</title>

        <!-- Bootstrap 的文件引入 已经有初始化文件 Normalize.css-->
        <link href="./bootstrap-3.3.2-dist/css/bootstrap.min.css" rel="stylesheet">

        <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
        <!--解决ie9以下浏览器对html5新增标签的不识别，并导致CSS不起作用的问题-->
        <!--解决ie9以下浏览器对 css3 Media Query  的不识别 -->
        <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->

        <!-- 条件注释:小于IE9的版本 -->
        <!--[if lt IE 9]>
          <script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
          <script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
        <![endif]-->
      </head>
      <body>
      </body>
    </html>
```



* 布局容器和预制类名

  ``` css
  <div class="container">//有15px内边距
  	<div class="btn btn-default"></div>
  <a class="text-muted"></a>
  <span class="glyphicon glyphicon-home"></span>
  </div>
  
  ```

### 栅格系统

* 总共12份

```css
	<div class="col-md-3"></div>//有内边距15px
	<div class="row"></div>//去掉父元素container的15px内边距
    <div class="col-md-pull-offset-2"></div>//偏移
	<div class="col-md-push-offset-2"></div>

```



* row没有设置宽度

  ``` css
  .row{
      margin-left:-15px;
      margin-right:-15px;
  }
  
  ```

  

### 响应式工具

* 只在某模式下进行显示

  ``` html
  <div class="visible-md">
      
  </div>
  
  ```

* 只在某个模式下进行隐藏

  ```html
  <div class="hidden-lg">
      
  </div>
  
  ```

* 设置图片大小，随着屏幕的变化而变化，当屏幕大于图片时，按照图片的大小进行显示；当屏幕小于图片时，按照屏幕大小进行显示 min-width:100%;

* 向上分配：选低档位

* 向下分配：媒体查询











