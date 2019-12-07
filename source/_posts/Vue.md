---
title: Vue
date: 2019-12-04 13:47:57
top:
categories:
   - 学习
   - Vue
tags: Vue
---

# Vue

## Vue介绍

* 构建用户界面（UI网页）的框架，关注视图层
* 框架：综合功能的封装
* MVVM（数据驱动视图）model view modelview
* 可以轻松构建单页面应用程序(spa) single page application
* 核心特点：
  * 数据操作视图更新，解放DOM操作
  * 组件化开发，提高开发效率和维护
* 官方教程：`http://cn.vuejs/org/guide/`
* 不支持IE8及以下

## Vue下载

* 网址：`：https://cdn.vuejs.org/index.html`
* CDN缓存技术`https://cdn.jsdelivr.net/npm/vue/dist/vue.js`
* npm下载 `npm i vue`

## Vue基本使用

* 引入vue.js文件，通过script标签

* 会有一个构造函数Vue

* 实例化构造函数，参数传入一个对象

  ```js
  new Vue({
      el:'p'，
      data:{
      num:0,//数字初始化
      str:'',//字符串初始化
      isSeen:false,//布尔类型初始化
      arr:[],//数组初始化
      obj:{},//对象初始化或者开始为null
  }
  })
  ```

* 通过vue的`自定义属性`，操作页面中的元素，其属性值，相当于放在js中解析，支持javascript的表达式

  ```html
  <p v-show='false'>对p标签进行隐藏</p>
  <p v-if='false'>
      对p标签进行隐藏
  </p>
  <!--v-if属性值为布尔类型时，一般如果不写值，默认为true
  v-show如果不添加任何值，默认值为false-->
  <p v-text="msg">相当于innerText</p>
  <p v-html> 相当于innerHTML</p>
  <p>{{msg}}</p><!--将数据展示到标签内部{{}}和v-text均可-->
  
  ```

* vue可以结合其他类库一起使用，互不影响

## Vue实例对象的属性（实例选项）

###	el

* 视图，模板

* 是划分范围，选中页面中的元素

* 值可以是选择器，DOM对象，jQ对象，建议使用id

* 如果选择器选中的是多个，只会对一个生效

* 不可以操作body和html

  ```js
  new Vue({
      el:document.querySelectorAll('div');//如果选中所有不会生效，还会报错
  })
  ```

### data

* 数据

* 其值是一个对象

  ```js
  new Vue({
      el:'p',
      data:{
          seen:false,
          msg:'我是一段文本',
          list:[1,2,3,4],
          user:{
              name:'张三',
              age:18,
              gender:'男'
          }
      }
  })
  ```

* 概念：

  > data---数据 
  >
  > 对数据进行管理-->模型model
  >
  > el-->视图 模板

* 注意：

  * 对于对象的修改
    * 对象没有初始化的对象成员如果修改不会更新到视图中
    * 也有方式可以动态添加未初始化的数据成员并且更新到视图中`解决方法：Vue.set(app.user,'gender','男')`
    * 可以直接对对象进行重新赋值实现视图更新
  * 对于数组的修改
    * 通过数组的一些操作方法可以正常进行视图的更新
    * 对数组进行重新赋值可以更新视图
    * 通过索引设置数组不会更新 vm.list[0]=newValue`解决方法：Vue.set(vm.list,0,{newValue})`
    * 通过设置数组长度不可以更新视图vm.list.length=newLength

### methods

* 其值是一个对象

* 专门定义方法的属性，也可以定义事件的回调函数

* **注意：当在data中定义了和methods中相同的属性名，以data中的为准，methods中不允许重复**

* **methods属性不允许使用箭头函数进行定义，会改变this指向(window)，但是可以使用ES6方式去定义**

  ```js
  new Vue({
      el:'#app',
      methods:{
          clicked:function(){
              
          },
          //与上面定义的方法相同：clicked(){
              
         // }
      }
  })
  ```

### mounted

* 类似window.onload

* 页面加载就执行

  ```js
  new Vue({
      el:'p',
      data:{},
      mounted:function(){
          document.querySelector('li:nth-child(2)').style.color='red';
      }
  })
  
  ```

### watch

* 侦听器

* 监听数据变化的机制

  ```js
  new Vue({
      el:'p',
      watch:{
          msg:function(newValue,oldValue){
              //newValue 新变化的数据
              //oldValue 旧变化的数据
              console.log(newValue,oldValue)
          }
      }
  })
  ```

  

### computed

* 计算属性通道

* 当视图中的数据处于不确定状态时，采用计算属性

* 其中属性值为这个属性对应的`函数的返回值`

* 在data中定义过的属性，不准在computed中重复定义，所以想要计算某个属性，直接无需在data中定义，在computed直接使用即可，就相当于定义过了

  ```js
  new Vue({
      el:'p',
      data:{
         student:null, 
      },
      computed:{
          student:function(){
              return this.students.filter(item=>{
                  return this.name=item.name
              })
          }
      }
  })
  ```

  

### created  

* vue实例对象实例化完成之后出发

  ```js
  new Vue({
      el:'p',
      created(){
         
      }
  })
  
  ```

  

## 数据绑定

* 模型中的数据与视图的对应关系
* 节点=属性+标签+内容
* 数据绑定=属性绑定+文本绑定+事件绑定

### 属性绑定

* 在Vue中对属性进行数据绑定，使用`v-bind:属性名="值"`

* 可以简写`<p :class="[cls1]"></p>`

* 语法：

  ```html
  <p v-bind:title='title'>一段内容</p>
  <script>
      new Vue({
          el:'p',
          data:{
              title:'我是title'
          }
      })
  </script>
  
  ```

* 属性绑定特殊

  * 对`style`属性(相对特殊，绑定时，其值为对象)

    ```html
    <p v-bind:style="{color:'red',backgroundColor:'#ffff'}">
       注意：red加上引号，否则按照变量进行解析会报错
    </p>
    
    ```

    

  * 对`class`属性(相对特殊，绑定时，其值为对象，其中属性名为存在的类名，属性值为布尔类型，是否使用该属性名作为类名)

    ```html
    <p v-bind:class="{test:true,demo:false}">
        
    </p>
    <p v-bind:class="[cls1,cls2]">
        
    </p>
    <script>
        new Vue({
            el:'p',
            data:{
                cls1:'test',
                cls2:'demo'
            }
        })
    </script>
    
    
    
    ```

### 文本绑定

* 双大括号不能写在属性中

* 语法：

  ```html
  <div id='app'>
      <p v-text='txt'>
  		相当于innerText    
  	</p>
      <p v-text='"我是文本“'>
          此处方式主要，因为Vue的自定义属性内部的属性值，相当于放到js中解析，所以要注意书写格式
      </p>
  	<p v-html='txt1'>
      	相当于innerHTML
  	</p>
  	<p>
      	{{msg}}常用
  	</p>
      <p>
          {{list[0]}}支持访问数组单元
      </p>
      <p>
          {{user.name}}支持访问对象，访问方式还是对象.的方式
      </p>
  </div>
  <script>
  
      new Vue({
          el:'p',
          data:{
              txt:'我是文本',
              txt1:'<h1>我是html结构的文本</h1>',
              msg:'我也是文本',
              list:['a','b','c'],
              user:{
                  name:'张三',
                  age:18
              }
          }
          
      })
  </script>
  
  
  ```

### 事件绑定

* 语法：`v-on:事件名称=“回调函数”`

* 可以简写`@事件名称=”回调函数“`

* 当没有事件的回调函数没有传递参数的时候，实际上是有一个默认参数的，叫`事件对象`，实质和js中学的一样，传入书写固定格式为`$event`

  ```html
  <div id="app">
      <a href="javascript:;" v-on:click='clicked'点击</a>//相当于方法的调用，传递的参数相当于实参
      <input type="button" @click="clicked1($event,a)" value='点击我获取事件对象'>
  </div>
  <script>
      new Vue({
          el:'#app',
          data:{},
         //提供专门定义方法的属性methods,也可以定义事件的回调函数
          methods:{
              clicked:function(){
                  console.log('点了');
              },
              clicked1:function(ev,n){//事件的声明，参数相当于形参
                  console.log(ev,a);
                  console.log(ev.target);//表示当前点击的DOM对象
              }
          }
      })
  </script>
  
  
  ```

### 事件绑定-修饰符

* 在vue中通过，`.修饰符`进行解决一些特殊的逻辑问题，如：冒泡，获取按键信息等
* 事件修饰符：
  * .stop 阻止冒泡
  * .prevent 阻止表单提交默认行为
    * 以下几点会触发表单的提交行为
      * 点击type为submit的input
      * 在文本框中回车
      * 点击普通按钮`<button></button>`
      * 建议在form的submit事件中阻止表单自动提交行为
  * .capture 
  * .self
  * .once
  * .passive
* 按键修饰符
  * .13
  * .enter
  * .tab
  * .delete
  * .esc
  * .space
  * .down
  * .left
  * .right
  * .up
* 系统修饰符
  * .ctrl
  * .alt
  * .shift
  * .meta
* vue中也存在冒泡
  * 在原生js中阻止冒泡行为通过`事件对象.stopPropagation()`阻止
* 这里使用原生js方式也是可以的，但是vue提供自己特有的方式

```html
<div id='app'>
   <div id='parent' @click="clickParent">
       <div id="child" @click.stop="clickChild"><!--阻止冒泡事件-->
           
       </div>
    </div>
    <form @submit.prevent='send'>//阻止表单提交默认行为
        
    </form>
    <input type="text" @keyup="send">
    <input type='text' @keyup.13="send"><!--点击回车按键触发send事件-->
    <input type="text" @keyup.enter="send"><!--点击回车键触发send事件-->
    <input type="text" @keyup.shift.enter="send"><!--点击shift+enter触发send事件-->
    <input type="text" @keyup.ctrl.shift.enter="end"><!--点击ctrl+shift+enter按键触发send事件-->
</div>
<script>
    new Vue({
        el:'#app',
        methods:{
            clickParent(){
                console.log('父亲');
            },
            clickChild(){
                console.log('儿子');//当点击子元素，父元素的点击事件也会触发，默认产生冒泡
            },
            send(){
                console.log('你按下了这些按键……');
            }
        }
    })
	
</script>

```



### 事件绑定-this指向

* 事件绑定中的this指向是vue的实例对象，且不可采用箭头函数的书写方式，因为会改变this的指向(window)

  



### 事件绑定-参数

* 默认参数是事件对象`$event`

  ```html
  <p @click='clicked'>
      
  </p>
  <!--等价于-->
  <p @click='clicked($event)'>
      
  </p>
  
  ```

  

* 传递参数直接`<p @click='clicked(a,$event)'></p>`

  ```js
  new Vue({
      el:'p',
      methods:{
          clicked(a,ev){
                console.log(ev.target);//表示当前点击的DOM对象
  
          }
      }
  })
  
  ```

  

## 响应式数据绑定

* 模型中的数据和视图的响应式绑定（自动机制）

* 自己理解为就是，通过改变模型中的数据data来控制视图的显示

* vue的实例对象可以直接访问data中的属性，也可以访问methods中的方法,或者`vue.$data.属性名`

* 实例：

  ```html
  <div id="app">
      <h1>
          {{msg}}
      </h1>
      <button @click='changeData'>
          更改一个数据，视图自动变化
      </button>
  </div>
  <script>
      var app=new Vue({
          el:'#app',
          data:{
              msg:'我是文本',
          },
          methods:{
              changeData:function(){//此处不建议采用箭头函数的书写，因为会改变this指向(window)
                  this.msg='我是更改的文本';//这里的this指的是app，vue的实例对象
                  this.demo();
              }，
              demo:function(){
          		console.log('我就是一个普通方法');
      		}
          }
      })
  
  </script>
  
  ```

## 双向绑定数据

* 前提：有自动机制（响应式数据绑定） 模型中的数据与视图相互响应

* 前面的响应式的数据绑定是：从vue的data中获取数据到视图中

* 视图上改变vue中的数据data

  ```html
  <div id="app">
      <input type="text" v-model="txt">//内部相当于为input注册input事件，并且记录input输入的值给txt,通过表单的v-model进行改变模型的data数据
      <button @click='clicked'>
          查看改变的数据
      </button>
  </div>
  <script>
      new Vue({
          el:'#app',
          data:{
              txt:'',
          },
          methods:{
              clicked:function(){
                  console.log(this.txt);
              }
          }
      })
  </script>
  
  ```

* 从视图上更新data数据，并在视图上进行响应（双向绑定）

  ```html
  <div id="app">
      <h1>
          {{msg}}
      </h1>
      <input type="text" v-model='msg'>
  </div>
  <script>
      new Vue({
          el:'#app',
          data:{
              msg:''
          }
      })
  </script>
  
  ```





## 结构

### v-show和v-if区别

* v-if和v-show都是控制视图的显示或隐藏
* 两者区别：
  * v-if:直接移除页面中的元素
  * v-show:通过`display:none`进行控制视图的显示或隐藏元素
  * v-show无论真假始终渲染元素，v-if只有为true才会渲染
  * 所以页面中对元素操作频繁时，用v-show,反之用v-if,另外v-if是惰性的，一旦为false,内部的所有元素都不会渲染

### v-if v-else-if v-else的使用

* 相当于js中的if - else if - else）

* 注意：

  * v-if与v-else之间不准存在普通标签否则会报错

  * v-if和v-else必须在同一级

    ```html
    	<!-- 它是一个整体 -->
    	<p v-if='seen'>hello</p> 
    	<!-- 他俩组成一个整体 -->
    	 <p v-if='1==1'>哈哈</p> 
    	 <p v-else>world</p> 
    
    
    ```

    

* 语法：

  ```html
  <div id="app">
      <p v-if="age>=17">
          成年
      </p>
      <p v-else>
          未成年
      </p>
      <span v-if="score>=80">
     		优秀 
      </span>
      <span v-else-if='age>=70'>
     		良好 
      </span>
      <span v-else>
     		及格 
      </span>
  </div>
  <script>
      new Vue({
          el:'#app',
          data:{
              age:19,
              score:88,
          }
      })
  </script>
  
  ```

### v-for使用

* 相当于js的forin

* 语法：

  ```html
  <div id="app">
      
      <ul>
          <li v-for='(item,index) in list'>{{index}}--{{item}}</li>
      </ul>
      <p>
          <span v-for="(item,key,index) in user">{{key}}:{{item}}</span>
      </p>
      <p v-for='n in 10'>
          {{n}}
      </p>
  </div>
  <script>
      new Vue({
          el:'#app',
          data:{
              list:[1,2,3,4],
              user:{
                  name:'张三',
                  age:18
              }
          }
      })
  
  </script>
  
  ```

* 数组更新

  * 常见的数组方法可以让其正常的进行视图更新
  * 或者直接对数组重新赋值
  * 注意以下两种不会更新视图
    * 通过索引直接设置数组不可以更新 vm.list[0]=newValue
    * 通过改变数组长度不可以更新 vm.list.length=newLength

* 对象更新

  * 对没有初始化的对象成员设置不能更新到视图上
  * 直接重新赋值该对象可以更新到视图上
  * 修改对象的某一个初始化的成员可以更新到视图上

### 在template标签中使用v-for

* 当需要遍历多个元素又不想增加额外标签节点时候，使用template标签是vue提供的一个特殊的标签，不会生成渲染结果

* **注意**

  * template上不能使用key,要把key加到真实的节点上

  * 不能使用v-show

    ```html
    <div id='app'>
        <template v-for='item in todos'>
       		<p>
                {{item.id}}
            </p> 
            <p>
                {{item.title}}
            </p>
        </template>
    </div>
    
    ```

    

## 补充

> input事件：表单`正在`输入触发此事件



## 微博案例

```js
<div class="weibo" id="app">
    <textarea class="weibo-text"  v-model='msg' @keyup.shift.enter='send'></textarea>
    <input class="weibo-btn" value="发布" type="button" @click='send'>
    <ul class="weibo-list">
        <li v-for='(item,index) in wblist'>{{item}}<span @click='deletewb(index)' :index='index'>删除</span>
        </li>
    </ul>
  </div>
</body>
<script src="./libs/vue.js"></script>
<script>
    new Vue({
        el:'#app',
        data:{
            msg:'',
            wblist:[],
        },
        methods:{
            send(){
                // console.log('发送');
                this.wblist.unshift(this.msg);
                this.msg=""
            },
        
           
            deletewb(i){
                this.wblist.splice(i,1);

            }
        }
    })
</script>

```





## key的使用

* vue在进行模板渲染的时候，为了提升性能，并不是每次都创建新的节点，而是当页面有重复的节点，会选择直接复用（此复用是指原位置变化）

* key的值一般不会使用索引值

* 只能是`简单类型`的字符串和数字类型，不能是数组和对象

* 为了解决它的弊端，存在一个叫`key`的属性

  ```html
  <div id="app">
      <div v-if="seen">
              <label for="">用户名：</label>
              <input type="text" key='1' placeholder="username">
          </div>
          <div v-else>
              <label for="">密码：</label>
              <input type="text" key='2' placeholder="password">
          </div>
          <div>
              <button @click='clicked'>切换</button>
        </div>
  </div>
  <script>
          new Vue({
              el:'#app',
              data:{
                  seen:true,
              },
              methods:{
                  clicked:function(){
                      this.seen=false;
                  }
              }
          })
      </script>
  
  ```

* 应用场景：与v-for结合

  ```html
  <div id="app">
        <ul>
            <li :key='item.id' v-for='item in list'>{{item.name}}
                <input type="text">
            </li>
        </ul>
      </div>
      <script src="./libs/vue.js"></script>
      <script>
          var app=new Vue({
              el:'#app',
              data:{
                  list:[{
                      id:Math.random(),
                      name:'张三',
                      age:18,
                      gender:'男'
                  },
                  {
                      id:Math.random(),
                      name:'张三1',
                      age:18,
                      gender:'男'
                  },{
                      id:Math.random(),
                      name:'张三2',
                      age:18,
                      gender:'男'
                  }],
                
              },
              methods:{
                  random(){
                      return 
                  }
              }
            
          })
      </script>
  
  ```

  

## 指令使用

* 就是带v-前缀的特殊属性

* v-once:数据引用一次

  ```html
  <div id="app">
      <p v-once>
          {{text}}
      </p>
      <p>
        {{text}}  
      </p>
  </div>
  
  ```

* v-cloak解决模板渲染时的页面闪烁，结合css使用

* 语法：

  ```html
  <style>
      [v-cloak]{
          display:none;
      }
  </style>
  <div id='app'>
      <p v-cloak>
          {{text}}
      </p>
  </div>
  <script src='./libs/vue.js'></script>
  <script>
      var wm=new Vue({
          el:'#app',
          data:{
              text:'我是',
          },
          
      })
  </script>
  
  ```

* v-pre：表示对应的标签不会再被vue处理

* 语法：

  ```html
  <p v-pre>
      {{msg}}
  </p>
  
  ```

  

### v-model

* 跟踪视图改变模型数据

* 使用

  * 对于type为text和textarea,使用v-model相当于对其进行绑定input事件来进行追踪当前元素内部的value值的变化

    * 其中v-model的修饰符

      > v-model.lazy:使其绑定的事件转换为change事件
      >
      > v-model.number：使其输入的内容进行数字类型转换
      >
      > v-model.trim:使其清除左右两边的空格

      ```html
      <div id='app'>
          <h1>
              {{username}}
          </h1>
          <input type='text' v-model='username'>
          <textarea v-model='msg'></textarea>
      </div>
      
      ```

  * 对于checkbox和radio类型的表单控件，使用v-model相当于对其进行绑定change事件，`需要配合value属性`,当不设置value时`还是控制选中状态`

    * 其中多选框需要设置数据为数组类型,为了收集选中的内容

    * 无需通过checked指定默认的选中项

      ```html
      <div id="app">
           <input type="checkbox" :value='"足球"' v-model='hobby'>足球
           <input type="checkbox" :value='"篮球"' v-model='hobby'>篮球
           <input type="radio"  :value='"男"' v-model='gender'>男
           <input type="radio"  :value='"女"' v-model='gender'>女
          </div>
          <script src="./libs/vue.js"></script>
          <script>
              var app=new Vue({
                  el:'#app',
                  data:{
                     gender:'男',
                     hobby:['足球','篮球']
                    
                  },
                  methods:{
                     
                  }
                
              })
          </script>
      
      ```

  * 对于select类型的表单控件，使用v-model相当于对其进行绑定change事件，可以配合value属性（建议配合）

    * 配合value时，参考的标准为value

    * 不配合value时，参考的标准为当前选中的option的文本内容

      ```html
      <div id="app">
           <select name="" id="" v-model='number'>
               <option value="0">--请选择--</option>
               <option value="1">北京</option>
               <option value="2">上海</option>
           </select>
          </div>
          <script src="./libs/vue.js"></script>
          <script>
              var app=new Vue({
                  el:'#app',
                  data:{
                     number:1
                    
                  },
                  methods:{
                     
                  }
                
              })
          </script>
      
      
      ```

## 全选和反选案例

* 实例：

  ```html
   <table id="app">
      <tr>
        <th>
          <input type="checkbox" name=""   id="checkAll" :checked='list.length==checkedItem.length' @click='ckClick' 
         />全选/全不选
        </th>
        <th>菜名</th>
        <th>商家</th>
        <th>价格</th>
      </tr>
      <tr :key='item.id' v-for='item in list'>
        <td>
          <input type="checkbox"    class="ck" :value='item.food' v-model='checkedItem'  />
        </td>
        <td>{{item.food}}</td>
        <td>{{item.brand}}</td>
        <td>{{item.price}}</td>
      </tr>
  
    </table>
  </body>
  <script src="./libs/vue.js"></script>
  <script>
          new Vue({
              el:'#app',
              data:{
                  isCk:false,
                  list:[
                      {id:1,food:'红烧肉',brand:'李家',price:'￥200'},
                      {id:2,food:'烧肉',brand:'赵家',price:'￥203'},
                      {id:3,food:'红肉',brand:'孙家',price:'￥205'},
                  ],
                  checkedItem:[],
              },
              methods:{
                  ckClick:function(e){
                      if(e.target.checked)
                      {
                         this.list.forEach(item=>{
                          //    this.checkedItem.push(item.food);
                          console.log(item.food);
                          this.checkedItem.push(item.food)
                          
                          
                         }) 
                      }
  
                  }
              }
          })
  </script>
  
  
  ```

##  动态属性

* 对于属性绑定和事件绑定中的属性和事件名，变为动态的变量

* 语法：

  ```html
  <div id="app">
          <p  @[eve]='clicked' :[prop]='"我是"'><!--注意此处属性值的写法，进入vue管理，属性值当js中解析，所以需要两次引号-->
      </div>
      <script src="./libs/vue.js"></script>
      <script>
          var app=new Vue({
              el:'#app',
              data:{
                  eve:'click',
                  prop:'title',
              },
              methods:{
              clicked(){
                  console.log('我被点了……');
                  
              }
              }
            
          })
      </script>
  
  ```

## 计算属性

* 当视图中的数据展示处于不确定状态时。当你需要提供一些代码逻辑改变数据，从而进行渲染数据，可以采用计算属性

* 自己理解：也是`双向绑定`的一种体现，就是在computed内部计算属性，随着数据的不断改变，从而实现不断重新计算属性，对于事件绑定的事件处理函数均定义在methods中，其余如果涉及到页面渲染的(el,data,computed等)，计算属性的方法定义在computed中

* 触发时机，是页面加载时触发+视图改变促使数据改变

* 一定要有返回值，返回之后就是属性值

* 自带缓存技术

  ```html
    <div id="app">
          <input type="text" v-model='name'>
          <ul>
              <li v-if='student.length'>
                  <span>{{student[0].name}}</span>
                  <span>{{student[0].age}}</span>
                  <span>{{student[0].gender}}</span>
  
              </li>
              <div v-else>
                  什么都没有
              </div>
          </ul>
      </div>
      <script src="./libs/vue.js"></script>
      <script>
          var app = new Vue({
              el: '#app',
              data: {
                  name: '',
                  students: [
                      { name: '小明', age: 20, gender: '男' },
                      { name: '小画', age: 10, gender: '男' },
                      { name: '小李', age: 22, gender: '男' },
                  ],
              },
              computed: {
                  student: function () {
                      return this.students.filter(item => {
                          return this.name == item.name
                      })
                  }
              },
           
  
          })
      </script>
  
  ```

## 侦听器

* 监听数据变化的机制

* 监听数据变化，获取新的数据和旧的数据，没有直接涉及渲染页面，当你想通过数据的变化实现一些特定逻辑，使用watch监视

* 不需要返回值，不需要绑定模式功能特点

* 触发机制=数据一改变就触发

  ```html
    <div id="app">
          <h1>{{name1}}</h1>
          <input type="text" v-model='name'>
          
      </div>
      <script src="./libs/vue.js"></script>
      <script>
          var app = new Vue({
              el: '#app',
              data: {
                  name: 1,
                  name1:'',
                  seen: false,
                  students: [
                      { name: '小明', age: 20, gender: '男' },
                      { name: '小画', age: 10, gender: '男' },
                      { name: '小李', age: 22, gender: '男' },
                  ],
              },
            watch:{
                  name:function(newV,oldV)
                  {
                      // this.name1=newV.split('').reverse().join('');
                      console.log(1);
                      console.log(Boolean(Number(newV)));
                                    
                      if(!Number(newV)&&newV!='')
                      {
                          this.name=oldV;
                      }
                  }
            }
  
          })
      </script>
  
  
  ```

## Vue DevTools调试工具

* vue devtools插件默认只能工作在http协议下
* 如果想要它在file://本地文件地址协议下工作，必须手动设置启动`允许访问文件网址`



## 基础案例

* todoMVC.com

* 初始化：

  * 下载模板
  * 使用github把模板下载到本地
  * 切换到下载的目录
  * 模板项目把样式等文件放到第三方包里面，所以我们需要执行npm i安装它的那些依赖项才能正常预览这个项目

* 需求说明：

* [ ] 任务列表

  * [ ] 有数据的时候
  * [ ] 没有数据的时候

* [ ] 添加任务

  * [ ] 添加任务到列表中
  * [ ] 文本框清空

* [ ] 删除单个任务项

* [ ] 单个任务状态切换

* [ ] 删除所有已完成任务

* [ ] 切换所有任务的完成状态（全选功能）

* [ ] 显示所有未完成的数量

* [ ] 数据筛选

  * [ ] 展示所有任务
  * [ ] 展示已完成任务
  * [ ] 展示未完成任务
  * [ ] 刷新页面保持筛选状态

* [ ] 数据持久化

  * [ ] 这里没有后端接口，我们可以使用本地存储简单处理一下

* [ ] 编辑任务

  * [ ] 双击获取编辑状态
  * [ ] 回车保存
  * [ ] esc取消

* 代码(index.html)

  ```html
  <!doctype html>
  <html lang="en">
  
  <head>
  	<meta charset="utf-8">
  	<meta name="viewport" content="width=device-width, initial-scale=1">
  	<title>Template • TodoMVC</title>
  	<link rel="stylesheet" href="node_modules/todomvc-common/base.css">
  	<link rel="stylesheet" href="node_modules/todomvc-app-css/index.css">
  	<!-- CSS overrides - remove if you don't need it -->
  	<link rel="stylesheet" href="css/app.css">
  </head>
  
  <body>
  	<section class="todoapp" id="app">
  		<header class="header">
  			<h1>todo</h1>
  			<input class="new-todo" placeholder="What needs to be done?" autofocus v-model='message'
  				@keyup.enter='addItem'>
  		</header>
  		<!-- This section should be hidden by default and shown when there are todos -->
  		<section class="main">
  			<input id="toggle-all" class="toggle-all" type="checkbox" @change='toggleChecked' :checked='isAll'>
  			<label for="toggle-all">Mark all as complete</label>
  			<ul class="todo-list">
  				<li :key='item.id' v-for="item in list" :class=" {completed:item.done,editing:item==isEdit}">
  					<div class="view">
  						<input class="toggle" type="checkbox" v-model='item.done' >
  						<label @dblclick="isEdit=item">{{item.title}}</label>
  						<button class="destroy" @click='delItem(item.id)'></button>
  					</div>
  					<!-- {{isEdit}} -->
  					<input class="edit" :value="isEdit.title" @keyup.enter='editItem' @keyup.esc='isEdit={}'>
  				</li>
  			</ul>
  		</section>
  		<!-- This footer should hidden by default and shown when there are todos -->
  		<footer class="footer">
  			<!-- This should be `0 items left` by default -->
  			<span class="todo-count"><strong>{{count}}</strong> item left</span>
  			<!-- Remove this if you don't implement routing -->
  			<ul class="filters">
  				<li>
  					<a class="selected" href="#/">All</a>
  				</li>
  				<li>
  					<a href="#/active">Active</a>
  				</li>
  				<li>
  					<a href="#/completed">Completed</a>
  				</li>
  			</ul>
  			<!-- Hidden if no completed items are left ↓ -->
  			<button class="clear-completed" v-show='isShow' @click='delCompleted'>Clear completed</button>
  		</footer>
  	</section>
  	<footer class="info">
  		<p>Double-click to edit a todo</p>
  		<!-- Remove the below line ↓ -->
  		<p>Template by <a href="http://sindresorhus.com">Sindre Sorhus</a></p>
  		<!-- Change this out with your name and url ↓ -->
  		<p>Created by <a href="http://todomvc.com">you</a></p>
  		<p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
  	</footer>
  	<!-- Scripts here. Don't remove ↓ -->
  	<script src="./node_modules/vue/dist/vue.js"></script>
  	<script src="node_modules/todomvc-common/base.js"></script>
  	<script src="js/app.js"></script>
  </body>
  
  </html>
  
  ```

* 代码(app.js)

  ```js
  const app = new Vue({
  	el: '#app',
  	data: {
  		message: '',
  		list:JSON.parse(window.localStorage.getItem('todolist'))||[],
  		isEdit: []
  	},
  	watch: {
          //每当list发生变化（添加删除修改）
          //默认只会监视数组成员的添加，删除，无法监视修改到成员中的对象数据修改
          //之前写的形式都是简写
          /*
          list(newValue,oldValue){
          	
          } 
          */
          //深度监视一般针对复杂数据类型：数组，对象之类的
  		list:{
              //handler就是数据改变之后执行的处理函数
  			handler(){
  				window.localStorage.setItem('todolist',JSON.stringify(this.list));
  			},
  			deep:true//深度监视默认为false
  		}
  	},
  	
  	computed: {
  		isAll() {
  			return this.list.every(item => {
  				return item.done
  			})
  		},
  		count() {
  			var count = 0;
  			this.list.forEach(item => {
  				if (!item.done) {
  					count++;
  				}
  			})
  			return count;
  		},
  		isShow() {
  			return this.list.some(item => {
  				return item.done
  			})
  		}
  
  	},
  	methods: {
  		addItem() {
  			this.list.push({
  				id: this.list[this.list.length - 1].id + 1,
  				title: this.message,
  				done: false,
  			});
  			this.message = '';
  		},
  		delItem(id) {
  			this.list.forEach((item, index) => {
  				if (item.id == id) {
  					this.list.splice(index, 1);
  				}
  			})
  
  		},
  		toggleChecked(e) {
  			this.list.forEach(item => {
  				item.done = e.target.checked;
  			})
  		},
  		delCompleted() {
  			for (var i = 0; i < this.list.length; i++) {
  				if (this.list[i].done) {
  					this.list.splice(i, 1);
  					i--;
  				}
  			}
  		},
  		editItem(e) {
  			// console.log(e.target.value);
  			this.isEdit.title = e.target.value;
  			// this.isEdit=null;
  			this.isEdit = {};
  
  		}
  
  	}
  })
  
  
  ```

* 自己写的(index.html)

  ```html
  <!doctype html>
  <html lang="en">
  
  <head>
  	<meta charset="utf-8">
  	<meta name="viewport" content="width=device-width, initial-scale=1">
  	<title>Template • TodoMVC</title>
  	<link rel="stylesheet" href="node_modules/todomvc-common/base.css">
  	<link rel="stylesheet" href="node_modules/todomvc-app-css/index.css">
  	<!-- CSS overrides - remove if you don't need it -->
  	<link rel="stylesheet" href="css/app.css">
  </head>
  
  <body>
  	<section class="todoapp" id="app">
  		<header class="header">
  			<h1>todomvc</h1>
  			<!-- 
  				实践建议：所有事件处理函数都起名为onXx,有利于阅读
  			 -->
  			<input class="new-todo" placeholder="What needs to be done?" autofocus v-model='inputTitle'
  				@keyup.13='onAdd'>
  		</header>
  		<!-- This section should be hidden by default and shown when there are todos -->
  		<template v-if='todos.length'>
  			<section class="main">
  				<input id="toggle-all" class="toggle-all" type="checkbox" @change='checkToggle'
  					:checked='todos.length==checkedArr.length'>
  				<label for="toggle-all">Mark all as complete</label>
  				<ul class="todo-list">
  
  					<!-- 
  			
  									任务项：li有三种内置样式
  									completed 已完成状态
  									没有class 未完成状态
  									editing 编辑状态
  								 -->
  					<li :key='todo.id' v-for='(todo,index) in toggleArr'
  						:class='{completed:todo.done,editing:todo==isEdit}'>
  
  						<div class="view">
  							<!-- 
  								表单元素 checkbox
  								双向绑定
  									数据影响视图
  										true:选中
  										false:不选
  									视图影响数据
  										选中 把数据修改为true
  										取消选中 把数据修改为false
  
  									数据改变，就会影响视图更新
  									为啥checkobox 切换把样式也给影响了，因为class也绑定了todo.done这个数据
  									
  										 -->
  							<input class="toggle" type="checkbox" v-model='todo.done' @change='changed(index)' >
  							<label @dblclick="isEdit=todo">{{todo.title}}</label>
  							<button class="destroy" @click='onDelete(index)'></button>
  						</div>
  						<!-- 编辑文本框默认隐藏，当任务项；li拥有editing为编辑模式 -->
  						<input class="edit" :value="todo.title" @keyup.13='onSave' @keyup.esc='isEdit=null'>
  					</li>
  				</ul>
  			</section>
  			<!-- This footer should hidden by default and shown when there are todos -->
  			<footer class="footer">
  				<!-- This should be `0 items left` by default -->
  				<span class="todo-count"><strong>{{count}}</strong> item left</span>
  				<!-- Remove this if you don't implement routing -->
  				<ul class="filters">
  					<li>
  						<a :class="{selected:isShowAll}" href="#/" @click='showAll'>All</a>
  					</li>
  					<li>
  						<a href="#/active" :class="{selected:isShowActive}" @click='showActive'>Active</a>
  					</li>
  					<li>
  						<a href="#/completed" :class="{selected:isShowCompleted}" @click='showCompleted'>Completed</a>
  					</li>
  				</ul>
  				<!-- Hidden if no completed items are left ↓ -->
  				<button class="clear-completed" v-show='isShow' @click='onDeleteCompleted'>Clear completed</button>
  			</footer>
  		</template>
  	</section>
  	<footer class="info">
  		<p>Double-click to edit a todo</p>
  		<!-- Remove the below line ↓ -->
  		<p>Template by <a href="http://sindresorhus.com">Sindre Sorhus</a></p>
  		<!-- Change this out with your name and url ↓ -->
  		<p>Created by <a href="http://todomvc.com">you</a></p>
  		<p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
  	</footer>
  	<!-- Scripts here. Don't remove ↓ -->
  	<script src="node_modules/todomvc-common/base.js"></script>
  	<script src="./node_modules/vue/dist/vue.js"></script>
  	<script src="js/app.js"></script>
  </body>
  
  </html>
  
  ```

  

* 自己写的(app.js)

  ```js
  var app = new Vue({
  	el: '#app',
  	data: {
  		inputTitle: '',//用户输入的任务名称
  		todos: [
  			{ id: 1, title: '吃饭', done: false },
  			{ id: 2, title: '睡觉', done: true },
  			{ id: 3, title: '打豆豆', done: false },
  			{ id: 4, title: '跑步', done: true },
  
  		],
  		isEdit: {},
  		isSeen: true,
  		toggleArr: [],
  		isShowActive:false,
  		isShowCompleted:false,
  		isShowAll:true,
  		isDelete:{},
  		// todosNew: []
  	},
  	computed: {
  		isShow() {
  			return this.todos.some(item => {
  				return item.done;
  			})
  		},
  		count() {
  			var count = 0;
  			this.toggleArr.forEach(item => {
  				if (!item.done) {
  					count++;
  				}
  			})
  			return count;
  		},
  		checkedArr() {
  			var ckArr = [];
  			this.todos.forEach((item, index) => {
  				if (item.done) {
  					ckArr.push(item);
  				}
  			})
  			return ckArr;
  		},
  		activeArr() {
  
  		},
  		
  
  	},
  	watch: {
  		
  		
  	},
  	methods: {
  		onAdd() {
  			// 1.得到文本框的数据
  			// 2.非空校验
  			if (!this.inputTitle.trim()) {
  				alert('请输入内容');
  				return;
  			}
  			console.log(this.todos);
  			
  			// 3.如果没有问题，把数据添加到任务列表中
  			this.toggleArr.push({
  				id: this.todos[this.todos.length-1].id+1,
  				title: this.inputTitle,
  				done: false
  			});
  			this.todos=this.toggleArr;
  			localStorage.setItem('todos',JSON.stringify(this.todos));
  
  			// 4.清空数据
  			this.inputTitle = '';
  		},
  		onDelete(index) {
  			this.toggleArr.splice(index, 1);
  			this.todos.splice(index,1);
  			localStorage.setItem('todos',JSON.stringify(this.todos));
  
  		},
  		onDeleteCompleted() {
  			var todosNew = [];
  			this.todos.forEach((item, index) => {
  				console.log(1);
  
  				if (!item.done) {
  
  					todosNew.push(item);
  
  				}
  			})
  			this.todos = todosNew;
  		},
  		showActive(e) {
  			this.toggleArr=[];
  			this.todos.forEach(item => {
  				if (!item.done) {
  					this.toggleArr.push(item);
  				}
  			})
  			this.isShowActive=true;
  			this.isShowAll=false;
  			this.isShowCompleted=false;
  			localStorage.setItem('isShowPage',JSON.stringify({
  				isShowAll:this.isShowAll,
  				isShowActive:this.isShowActive,
  				isShowCompleted:this.isShowCompleted
  			}));
  		},
  		showCompleted() {
  			this.toggleArr=[];
  			this.todos.forEach(item => {
  				if (item.done) {
  					this.toggleArr.push(item);
  				}
  			})
  			this.isShowCompleted=true;
  			this.isShowAll=false;
  			this.isShowActive=false;
  			localStorage.setItem('isShowPage',JSON.stringify({
  				isShowAll:this.isShowAll,
  				isShowActive:this.isShowActive,
  				isShowCompleted:this.isShowCompleted
  			}));
  
  		},
  		checkToggle(e) {
  			this.todos.forEach(item => {
  				item.done = e.target.checked;
  			})
  
  		},
  		onSave(e) {
  			this.isEdit.title = e.target.value
  			this.isEdit = null;
  		},
  		showAll(){
  			this.toggleArr=[];
  			this.todos.forEach(item => {
  				this.toggleArr.push(item);
  	
  			})
  			this.isShowAll=true;
  			this.isShowActive=false;
  			this.isShowCompleted=false;
  			localStorage.setItem('isShowPage',JSON.stringify({
  				isShowAll:this.isShowAll,
  				isShowActive:this.isShowActive,
  				isShowCompleted:this.isShowCompleted
  			}));
  
  		},
  		changed(index){
  			// console.log('被点了');
  			localStorage.setItem('todos',JSON.stringify(this.todos));
  			if(!this.isShowAll)
  			{
  				
  				this.toggleArr.splice(index,1);
  			}else{
  				console.log(index);
  				// localStorage.setItem('todos',JSON.stringify(this.todos));
  
  				
  			}
  			
  		}
  
  
  	},
  	mounted: function () {
  		
  		var str=localStorage.getItem('todos');
  		var page=localStorage.getItem('isShowPage');
  		if(!str||!page)
  		{
  			
  			localStorage.setItem('isShowPage',JSON.stringify({
  				isShowAll:this.isShowAll,
  				isShowActive:this.isShowActive,
  				isShowCompleted:this.isShowCompleted
  			}));
  			localStorage.setItem('todos',JSON.stringify(this.todos));
  			str=localStorage.getItem('todos');
  			page=localStorage.getItem('isShowPage')
  		}
  		this.todos=JSON.parse(str);
  		page=JSON.parse(page);
  		this.isShowAll=page.isShowAll;
  		this.isShowActive=page.isShowActive;
  		this.isShowCompleted=page.isShowCompleted;
  		
  		this.todos.forEach(item => {
  			// this.toggleArr.push(item);
  			if(this.isShowAll)
  			{
  				this.showAll();
  			}
  			else if(this.isShowActive)
  			{
  				this.showActive();
  			}
  			else if(this.isShowCompleted)
  			{
  				this.showCompleted();
  			}
  
  		});
  		
  	}
  })
  
  
  ```

  





> 小知识：
>
> 对于表单元素改变的时候
>
> 1.对于checkbox来讲，当选中状态改变的时候，无论通过什么方式（DOM，vue）获取checkbox改变之后的状态都建议使用change事件
>
> 2.不要使用click点击事件，因为点击事件触发的时候，checkbox的切换状态可能还没有改变，所以通过click事件获取checkbox的checked状态可能存在误差

> 数组中常用的方法：
>
> ​	1.forEach方法（大多数情况下可以代替for循环）
>
> ​		eg:
>
> ​			arr.forEach((item,index)=>{
>
> ​			})
>
> ​	2.some方法（判断数组中是否包含指定条件的元素）它会遍历数组，然后对每一项执行条件判断，只要有一个满足条件，停止遍历，返回true,如果到循环结束都没有满足条件的元素，返回false
>
> ​		eg:
>
> ​			arr.some((item,index)=>{
>
> ​				return item.title='睡觉'
>
> ​			})
>
> ​	3.every判断数组是元素是否全部满足某个条件
>
> ​		eg:
>
> ​			arr.every((item,index)=>{
>
> ​				return item.done
>
> ​			})
>
> ​	4.filter从数组中根据某个条件过滤数据得到一个新的数组，注意：过滤结果还是一个数组
>
> ​		eg:
>
> ​			arr.filter((item,index)=>{
>
> ​				return item.done
>
> ​			})
>
> ​	5.find根据条件查找某个元素，它会遍历找到第一个满足条件的元素，停止遍历，并立即返回
>
> ​		eg:
>
> ​			arr.find((item,index)=>{
>
> ​					return item.id=3
>
> ​			})
>
> ​	6.findIndex根据条件查找元素的索引
>
> ​		eg:
>
> ​			arr.findIndex((item,index)=>{
>
> ​				return item.id=3
>
> ​			})		
>
> ​	7.includes判断数组是否包含指定元素，类似indexof，返回布尔值，一般用于数组中都是普通类型：字符串，数字
>
> ​	eg:
>
> ​			arr.includes(1);

## 编辑插件

* ​	vscode:live-server
* sublime:sublime server

## 与服务器通信

* 类似于jQuery中的ajax库（axios）

### 学习准备

#### 	JSON-server

* 是一个提供测试环境接口的工具，可以帮我们快速生成一套接口服务，专门用于学习测试

* 使用步骤

  > 1.安装：`https://github.com/typicode/json-server`
  >
  > 2.在cmd中输入`npm install -g json-server`
  >
  > 3.测试是否安装成功：`son-server --version `
  >
  > 4.创建一个目录json-server-demo,然后在该目录中创建一个文件叫db.json并写入以下内容：
  >
  > ```json
  > {
  > "posts": [
  >  { "id": 1, "title": "json-server", "author": "typicode" }
  > ],
  > "comments": [
  >  { "id": 1, "body": "some comment", "postId": 1 }
  > ],
  > "profile": { "name": "typicode" }
  > }
  > 
  > ```
  >
  > 5.最后，进入db.json文件所属的目录，执行`json-server --watch db.json`
  >
  > ![snipaste_20191107_173920](E:\black\就业班\vue\assets\snipaste_20191107_173920.png)
  >
  > 

  

### 接口说明

* jsonServer会根据db.json文件中的内容生成一些接口

  * 获取用户列表

    > 请求方法：get
    >
    > 请求路径:/users
    >
    > 请求参数：
    >
    > 响应数据：用户列表

  * 查询指定用户列表

    > 请求方法：get
    >
    > 请求路径:/users?name=姓名&gender=性别&age=年龄
    >
    > 请求参数：
    >
    > Query(查询字符串)参数：
    >
    > ​	name:姓名
    >
    > ​	age:年龄
    >
    > ​	gender:性别
    >
    > 响应数据：指定用户列表

  * 添加用户

    > 请求方法：post
    >
    > 请求路径:/users
    >
    > 请求参数：
    >
    > ​	{	
    >
    > ​		"name":用户名称,
    >
    > ​		"age":年龄,
    >
    > ​		"gender":性别
    >
    > ​	}
    >
    > 响应数据：新增用户信息
    >
    > 注意：请求体数据必须是json格式字符串

  * 删除用户

    > 请求方法：DELETE
    >
    > 请求路径:/users/id
    >
    > eg:`例如删除id为3的用户:http://localhost:3000/users/3`
    >
    > 请求参数：
    >
    > 响应数据：{}

  * 修改用户：

    > 请求方法：PATCH
    >
    > 请求路径:/users/id
    >
    > eg:`例如修改id为3的用户:http://localhost:3000/users/3`
    >
    > 请求参数：
    >
    > body请求体数据：
    >
    > {
    >
    > ​	"name":名称,
    >
    > ​	"age":年龄,
    >
    > ​	"gender":性别
    >
    > }
    >
    > 注意：name,age,gender都是可选的，修改谁就传谁
    >
    > 响应数据：修改之后的用户的完整信息

### axios介绍

* 网址：`http://github.com/axios/axios`

* 安装:`npm install axios`

* 获取用户列表

  > axios({
  >
  > ​	method:'GET',
  >
  > ​	url:'http://localhost:3000/users',
  >
  > ​	
  >
  > }).then(res=>{
  >
  > ​	res是响应对象
  >
  > ​	接口返回的数据在res.data中
  >
  > ​	config:本次请求配置信息对象，很少使用
  >
  > ​	data:真正响应结果数据
  >
  > ​	headers：响应头数据，很少使用
  >
  > ​	request:请求对象，几乎不使用
  >
  > ​	status:响应状态码
  >
  > ​	statusText:响应状态短语	
  >
  > ​	console.log(res.data);
  >
  > })

* 查询指定用户列表

  > axios({
  >
  > ​	method:'GET',
  >
  > ​	url:'http://localhost:3000/users?id=2',//查询id为2的用户,或者写在params
  >
  > ​	params:{	
  >
  > ​		id:2,
  >
  > ​		name:'张三'
  >
  > ​	},
  >
  > ​	
  >
  > 
  >
  > }).then(res=>{
  >
  > ​	console.log(res);
  >
  > })

* 添加用户

  > axios({
  >
  > ​	method:'post',
  >
  > ​	url:'http://localhost:3000/users',
  >
  > ​	data:{
  >
  > ​		name:'',
  >
  > ​		age:'',
  >
  > ​		gender:''
  >
  > ​	}
  >
  > }).then(res=>{
  >
  > ​	if(res.status==201){
  >
  > ​		console.log(res.data);
  >
  > ​	}
  >
  > })

* 删除用户：

  > axios({
  >
  > ​	method:'DELETE',
  >
  > ​	url:'http://localhost:3000/users/1',//删除id为1的用户
  >
  > ​	
  >
  > }).then(res=>{
  >
  > ​	console.log(res);
  >
  > })

* 修改用户：

  > axios({
  >
  > ​	method:'PATCH',
  >
  > ​	url:'http://localhost:3000/users/2',//修改id为2的用户
  >
  > ​	data:{
  >
  > ​		name:'',
  >
  > ​		age:'',
  >
  > ​		gender:''
  >
  > ​	}
  >
  > }).then(res=>{
  >
  > ​	console.log(res,data);
  >
  > })

### 配置

* 配置基础路径

> axios.defaults.baseURL='http://localhost:3000'

### axios快捷写法

> ​	 axios.get(url[, config])
>
> ​        axios.get('http://localhost:3000/users'
>
> ​            //可选的配置对象
>
> ​        ).then(res => {
>
> ​            console.log(res);
>
> ​        })
>
> ​        // axios.delete(url[, config])
>
> ​        // axios.head(url[, config])
>
> ​        // axios.options(url[, config])
>
> ​        // axios.post(url[, data[, config]])
>
> ​        // axios.put(url[, data[, config]])
>
> ​        // axios.patch(url[, data[, config]])

### axios错误处理

> ```js
> axios({
>  method:'GET',
>  url:'http://localhost:3000/users',
>  
> }).then(res=>{
> //成功执行then
>  //在axios中，默认只有>=200和<400的状态码都认为成功
>  //axios在这个请求失败之后不执行then里面的代码
> }).catch(err=>{
>  //失败执行catch
> })
> 
> ```

### vue和axios结合

```html
 <div id="app">
        <!-- <h1>{{message}}</h1> -->
        <!-- 
            表单的submit事件：当表单中的submit或者button点击的时候，或者表单文本框中敲回车的时候都会触发submit事件
         -->
        <form @submit.prevent="onAdd">
            <div>
                <label for="">姓名</label>
                <input type="text" v-model='user.name'>
            </div>
            <div>
                <label for="">年龄</label>
                <!-- 
                        v-model支持一个修饰符：.number可以把绑定的数据自动转为数字类型
                     -->
                <input type="text" v-model.number='user.age'>
            </div>
            <div>
                <label for="">性别</label>
                <input type="radio" value='男' v-model='user.gender' name="gender">男
                <input type="radio" value='女' v-model='user.gender' name="gender">女
            </div>
            <div>
                <input type="submit" value="添加">
            </div>
        </form>
        <table>

            <thead>
                <tr>
                    <th>id</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                    <th>操作</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td>{{user.id}}</td>
                    <td>{{user.name}}</td>
                    <td>{{user.age}}</td>
                    <td>{{user.gender}}</td>
                    <td>
                        <button @click='onClick(user.id)'>删除</button>
                    </td>
                </tr>

            </tbody>
        </table>
    </div>
    <script src="./libs/vue.js"></script>
    <script src="./node_modules/axios/dist/axios.js"></script>
    <script>
        axios.defaults.baseURL = 'http://127.0.0.1:3000';
        // // 1.发送请求获取数据
        // axios({
        //     method: 'GET',
        //     url: '/users',

        // }).then(res => {//then方法中的回调函数，只有当请求成功的时候才会执行
        //     // 2.将请求的数据赋值给vue来使用 （vue中的数据一定要提前初始化）
        //     //  把vue实例中的users=res.data

        //     app.users = res.data;
        //     // 3.将数据绑定到模板中
        // })
        const app = new Vue({
            el: '#app',
            data: {
                message: 'hello vue.js',
                // 根据接口要求包括视图，抽象出需要绑定的数据字段
                // 这里的名字也不要瞎起，因为这个数据要提交给后端接口
                user: {
                    name: '',
                    age: '',
                    gender: ''
                },
                users: []//存储用户数据列表
            },
            methods: {
                onAdd() {
                    console.log(23);

                    // 1.获取表单数据
                    // 1.1根据接口和视图抽象出数据放到初始化到data中
                    // 建议表单相关的数据放到单独的数据对象中
                    // 1.2然后使用v-model把数据分别绑定到对应的表单元素上
                    // 1.3完了利用VueDevTools调试工具测试数据是否绑定OK
                    // 

                    // 2.请求提交
                    // json-server 默认提供了CORS跨域 后端跨域 前端不需要做任何处理
                    // 在后端的CORS请求中，浏览器会先发出一个方法请求方法OPTIONS的预检请求
                    // 整个过程都是自动的，不需要代码参与，浏览器默认行为

                    axios({
                        method: 'POST',
                        url: '/users',
                        data: this.user,


                    }).then(res => {
                        console.log(res);
                        // 添加成功 重新获取最新的用户数据列表
                        this.loadUsers();
                    }).catch(err => {
                        window.alert('添加失败' + err);
                    })

                    // 3.根据响应结果进行后续处理
                },
                loadUsers() {
                    axios({
                        method: 'GET',
                        url: '/users',

                    }).then(res => {
                        // 注意：then方法中的函数务必使用箭头函数，否则里面的this指向有问题
                        //tnen方法中的回调函数，只有当请求成功的时候才会执行
                        // 2.将请求的数据赋值给vue来使用 （vue中的数据一定要提前初始化）
                        //  把vue实例中的users=res.data

                        this.users = res.data;
                        // 3.将数据绑定到模板中

                        // 不太建议在created中写大量的业务逻辑代码
                        // 我们更推荐把这些功能封装成一个一个的函数放到methods中
                    })
                },
                onClick(id){
                    if(!window.confirm('Are you sure?'))
                    {
                        return
                    }
                        axios({
                            method:'DELETE',
                            url:'/users/'+id,//建议所有字符串都使用es6模板字符串方式
                            
                        }).then(res=>{
                            this.loadUsers();
                        }).catch(err=>{
                            window.alert('删除失败！');
                        })
                }
            },
            // 实例选项：created
            // 他是一个函数，他会在vue初始化完成以后自动调用
            // 我们可以在它里面访问this,获取vue实例
            // 常见的场景就是：在页面加载好以后请求获取数据列表
            created() {
                // // 1.发送请求获取数据
                // axios({
                //     method: 'GET',
                //     url: '/users',

                // }).then(res => {
                //     // 注意：then方法中的函数务必使用箭头函数，否则里面的this指向有问题
                //     //tnen方法中的回调函数，只有当请求成功的时候才会执行
                //     // 2.将请求的数据赋值给vue来使用 （vue中的数据一定要提前初始化）
                //     //  把vue实例中的users=res.data

                //     this.users = res.data;
                //     // 3.将数据绑定到模板中

                //     // 不太建议在created中写大量的业务逻辑代码
                //     // 我们更推荐把这些功能封装成一个一个的函数放到methods中
                // })

                // 方法也可以直接通过vue实例进行调用
                this.loadUsers();
            }
        })
    </script>

```

##　组件基础

* 引入组件的原因：为了避免更多的冗余标签及逻辑等

* 一个标签`<span-btn>`代表一个组件，写一个标签相当于一个组件的实例
* 注册一个全局组件（要写在vue实例对象之前）`Vue.component(组件名称，组件对象)`
  * 组件名称一般采用abc 单词或abc-d双词（全小写）进行定义
* 页面结构template`有且只有一个根节点`
* data是一个带返回值的函数（因为组件和组件之间要保存独立的数据）

```html
 <div id="app">
        <span-btn></span-btn>
        <span-btn></span-btn>

    </div>
    <script src="./libs/vue.js"></script>
   
    <script>
        Vue.component('span-btn',{
            template:`<div>
            
                <span>{{count}}</span>
                <button @click='changeCount'>按钮</button>
            </div>`,
            data(){
                return {
                    count:0,
                }
            },
            methods:{
                changeCount(){
                    this.count++;
                }
            }
        })
        new Vue({
            el:'#app',
        })
    </script>

```



## 全局组件

* 只要你实例化一个vue对象，就自动注册了这个全局组件（拥有）
* 注意：**全局组件要写在所有vue实例对象的最前面**
* `Vue.component(组件名称,组件对象)`

## 局部组件

* 在哪个实例对象上注册组件，就对哪个实例对象起作用

* `components:{组件名称：组件对象}`

  ```html
    <div id="app">
          <span-btn></span-btn>
          <span-btn></span-btn>
  
      </div>
      <div id="app1">
          <h1>我是vue实例2</h1>
          <span-btn></span-btn>
          <span-btn></span-btn>
  
      </div>
      <script src="./libs/vue.js"></script>
      <script>
          new Vue({
              el: '#app1',
              components:{
                  "span-btn":{
                      template:`<div>我试一下</div>`
                  }
              }
          })
         
          new Vue({
              el: '#app',
          });
  
      </script>
  
  ```

## 组件总结

* 特点：
  * 组件是一个特殊的Vue实例
  * 没有el实例选项，有template属性
  * 组件和vue实例对象的区别是组件中的data是带有返回值的函数
  * template代表页面的结构（有且只有一个根节点）
  * 组件之间是独立的
* 局部组件和全局组件之间区别：注册位置不同，应用范围不同

## 组件嵌套

* 一旦形成组件嵌套，就有了父子关系
* 在组件中使用了其他组件的标签，就会产生组件嵌套
* 组件嵌套形式
  * 下面展示的是组件和组件之间的纯嵌套
  * Vue实例对象与组件之间的嵌套（就是在视图中直接写组件标签）

```html
 
    <div id="app1">
        <h1>我是vue实例2</h1>
        <span-btn></span-btn>
        <span-btn></span-btn>

    </div>
    <script src="./libs/vue.js"></script>
    <script>
        Vue.component("span-btn",{
            template:`<p>
            我是你爸爸
            <span-child></span-child>
            <child></child>
            </p>`,
            components:{
                "child":{
                    template:`<p style="color:red">我是直系亲属</p>`
                }
            }
        });
        Vue.component('span-child',{
            template:`<p>我是你儿子</p>`
        })
        new Vue({
            el: '#app1',
            
        })
       
      
    </script>

```



## 组件通信的几种情况

* 父组件=>子组件`通过props`
* 子组件=>父组件
* 兄弟组件=>兄弟组件

## 父组件给子组件传值Props

* 给谁传值就在谁身上定义属性（Vue自定义属性），属性值为要`传递`的数据的名字
* 在子组件内部`接收`属性，通过props，其值为数组（字符串数组）
* 子组件中使用该数据，名字也为props中的写字符串数组的名字

```html
<!--Vue实例对象与子组件进行嵌套1-->  
<div id="app1">
        <foods :foodlist='list'></foods>  
    </div>
    <script src="./libs/vue.js"></script>
    <script>
      
        new Vue({
            el: '#app1',
            data:{
                list:['红烧肉','糖醋里脊','四喜丸子'],
            },
            components:{
                'foods':{
                    template:`<div>我是饭{{foodlist}}</div>`,
                    props:['foodlist'],
                    methods:{
                        fnc(){
                            console.log(this.foodlist);//this指向是当前的组件对象，可以直接访问内部的data数据，或者props传过来的值，与Vue实例对象内部的this一样
                        }
                    }
                }
            }
        })


    </script>
<!--Vue实例对象与子组件之间进行传递值2-->
    <div id="app1">
        <child :cities="citylist"></child>
    </div>
    <script src="./libs/vue.js"></script>
    <script>
      
        new Vue({
            el: '#app1',
            data:{
                citylist:['上海','北京','天津','重庆'],
            },
            components:{
                "child":{
                    template:`<div>
                        我去过的城市有：
                        <ul>
                            <li v-for="city in cities">{{city}}</li>
                        </ul>
                    </div>`,
                    props:['cities'],
                }
            }
            
        })


    </script>

<!--组件与组件之间嵌套时，进行父传子-->
    <div id="app1">
        <!-- <foods :foodlist='list'></foods>   -->
        <father></father>
    </div>
    <script src="./libs/vue.js"></script>
    <script>
        Vue.component('father',{
            template:`<div>
                我是父亲
                <child :num="count"></child>
            </div>`,
            data(){
                return {
                    count:0,
                }
            },
            components:{
                "child":{
                    template:`<div>
                        我是儿子
                        {{num}}
                    </div>`,
                    props:['num']
                }
            }
        })
        new Vue({
            el: '#app1',
           
           
        })


    </script>





```

## SPA

* 单页面应用程序：
  * 多个模块访问一个一个网页
  * 一次向服务器获取资源
* 优点：
  * 减缓网络延迟
  * 完全组件化开发
* 缺点：
  * 首屏加载慢-->`按需加载`不刷新页面，只请求js模块
  * 不利于SEO-服务端渲染
  * 开发难度略高

### SPA原理

* 实现在前端自由切换的模块--事件监听onhashchange进行实现自由切换
* 对当前的模块由记忆功能--页面刷新锚点之前点击的锚点还存在，只需要通过锚点获取响应的内容
* 不引起页面刷新---锚点不会引起页面刷新
* 解决：
  * 解决页面不刷新以及模块之间进行切换
    * 前端路由--通过hash值获取当前锚点（模块）
    * 通过事件监听hash改变`onhashchange`

```html
<!--js实现路由的实现过程-->
 	<a href="#bj">北京</a>
    <a href="#sh">上海</a>
    <a href="#sz">深圳</a>
    <a href="#gz">广州</a>
    <div class="container"></div>
    <script>
        var fnc= function () {
            var dom = document.querySelector('.container');
            var path = window.location.hash.substr(1);
            switch (path) {
                case 'bj':
                    dom.innerHTML = '北京';
                    break;
                case 'sh':
                    dom.innerHTML = '上海';
                    break;
                case 'sz':
                    dom.innerHTML = '深圳';
                    break;
                case 'gz':
                    dom.innerHTML = '广州';
                    break;
                default:
                    break;
            }
        };
        fnc();
        window.onhashchange =fnc;
    </script>

```



## VueRouter路由

* 需要下载vue-router插件

* 通过to属性实现不同模块之间的跳转

* 步骤

  * 引入vue-router.js文件
  * 定义导航`<router-link>`可以不设置
  * 第一容器`<router-view>`必须有
  * 实例化VueRouter
  * 配置路由表，一个地址对应一个组件（模块）
  * 挂载路由

  ```html
    <div id="app">
        <router-link to='/main'>主食</router-link>
        <router-link to='/meat'>肉食</router-link>
        <router-link to='/soup'>汤</router-link>
        <router-view></router-view>
  
    </div>
    <script src="./libs/vue.js"></script>
    <script src="./vue-router.js"></script>
    <script>
        var router=new VueRouter({
            routes:[
                {
                    path:'/main',
                    component:{
                        template:`<div>吃什么吃，啥也没有</div>`
                    }
                },
                {
                    path:'/meat',
                    component:{
                        template:`<div>塞牙缝</div>`
                    }
                },
                {
                    path:'/soup',
                    component:{
                        template:`<div>喝西北风</div>`
                    }
                }
            ]
        })
        new Vue({
            el:'#app',
            router
        })
    </script>
  
  ```

## 动态路由

* 动态路由传参
* 获取参数`$route.params`=>获取所有动态路由参数的集合

```html
 <div id="app">
      <router-link to='/foods/主食'>主食</router-link>
      <router-link to='/foods/肉食'>肉食</router-link>
      <router-link to='/foods/汤'>汤</router-link>
      <router-view></router-view>

  </div>
  <script src="./libs/vue.js"></script>
  <script src="./vue-router.js"></script>
  <script>
      var router=new VueRouter({
          routes:[
              {
                  path:'/foods/:foodname',
                  component:{
                      template:`<div>吃什么吃，啥也没有{{$route.params.foodname}}</div>`
                  }
              }
          ]
      })
      new Vue({
          el:'#app',
          router
      })
  </script>

```





## VueRouter中to的其他赋值方式

* 字符串

* 变量

* 对象

* 对象name形式

  ```html
   <div id="app">
          <router-link to='/bj'>北京</router-link>
          <router-link to='/sh'>上海</router-link>
          <!-- 变量 -->
          <router-link :to='shStr'>上海(变量)</router-link>
          <!-- 对象 -->
          <router-link :to='{path:"/sh"}'>上海（对象）</router-link>
          <!-- 对象name形式 -->
          <router-link :to='{name:"sd"}'>上海（对象name形式）</router-link>
  
          <router-link to='/sz'>深圳</router-link>
          <router-link to='/gz'>广州</router-link>
          <router-view></router-view>
  
      </div>
      <script src="./libs/vue.js"></script>
      <script src="./vue-router.js"></script>
      <script>
          var router = new VueRouter({
              routes: [
                  {
                      path: '/bj',
                      component: {
                          template: `<div>北京</div>`
                      }
                  },
                  {
                      name:'sd',
                      path: '/sh',
                      component: {
                          template: `<div>上海</div>`
                      }
                  },
                  {
                      path: '/sz',
                      component: {
                          template: `<div>深圳</div>`
                      }
                  }, {
                      path: '/gz',
                      component: {
                          template: `<div>广州</div>`
                      }
                  }
              ]
          })
          new Vue({
              el: '#app',
              data:{
                  shStr:'/sh'
              },
              router
          })
      </script>
  
  <!--传递参数的to的不同赋值形式-->
  <div id="app">
          <router-link to='/bj/首都'>北京</router-link>
          <router-link to='/sh/是吗'>上海</router-link>
          <!-- 变量 -->
          <router-link :to='shStr'>上海(变量)</router-link>
          <!-- 对象 -->
          <router-link :to='{path:"/sh/是吗3"}'>上海（对象）</router-link>
          <!-- 对象name形式 -->
          <router-link :to='{name:"sd",params:{ab:"我是"}}'>上海（对象name形式）</router-link>
  
          <router-link to='/sz'>深圳</router-link>
          <router-link to='/gz'>广州</router-link>
          <router-view></router-view>
  
      </div>
      <script src="./libs/vue.js"></script>
      <script src="./vue-router.js"></script>
      <script>
          var router = new VueRouter({
              routes: [
                  {
                      path: '/bj/:abc',
                      component: {
                          template: `<div>北京{{$route.params.abc}}</div>`
                      }
                  },
                  {
                      name:'sd',
                      path: '/sh/:ab',
                      component: {
                          template: `<div>上海{{$route.params.ab}}</div>`
                      }
                  },
                  {
                      path: '/sz',
                      component: {
                          template: `<div>深圳</div>`
                      }
                  }, {
                      path: '/gz',
                      component: {
                          template: `<div>广州</div>`
                      }
                  }
              ]
          })
          new Vue({
              el: '#app',
              data:{
                  shStr:'/sh/是吗1'
              },
              router
          })
      </script>
  
  ```

## 重定向

* 拦截谁就在谁的路由上写`redirect`

  ```html
    <div id="app">
          <router-link to='/bj/首都'>北京</router-link>
          <router-link to='/sh/是吗'>上海</router-link>
          <router-link to='/sz'>深圳</router-link>
          <router-link to='/gz'>广州</router-link>
          <router-view></router-view>
  
      </div>
      <script src="./libs/vue.js"></script>
      <script src="./vue-router.js"></script>
      <script>
          var router = new VueRouter({
              routes: [
                  {
                      path: '/bj/:abc',
                      component: {
                          template: `<div>北京{{$route.params.abc}}</div>`
                      }
                  },
                  {
                      name: 'sd',
                      path: '/sh/:ab',
                      component: {
                          template: `<div>上海{{$route.params.ab}}</div>`,
                         
                      },
                      redirect:'/bj/abc'
                  },
                  {
                      path: '/sz',
                      component: {
                          template: `<div>深圳</div>`
                      }
                  }, {
                      path: '/gz',
                      component: {
                          template: `<div>广州</div>`
                      }
                  }
              ]
          })
          new Vue({
              el: '#app',
            
              router
          })
      </script>
  
  ```

## 编程式导航

* 实现跳转

  * a标签
  * window.location.href
  * 采用代码行为进行跳转
    * $.router.push() 推进一条记录，点击返回回到上次的地址
    * $.router.replace()替换当前记录，不能返回，替换记录
    * $.router.go()为正值前进，为负值后退

  ```html
   <div id="app">
  
          <router-view></router-view>
  
      </div>
      <script src="./libs/vue.js"></script>
      <script src="./vue-router.js"></script>
      <script>
          // 1. 实例化一个导航路由
          // 2. 导航为 A, B, C, D
          // 3. 实现A => B, B => C, 然后从C返回时, 直接回到A
          // 4. 实现A => B, B => C, C => D 从D返回时 不能返回
          // 5. 实现A => B, B => C, C => D 从D返回直接返回到A 在A中直接前进到D
          var router = new VueRouter({
              routes: [
                  {
                      path: '/',
                      redirect: '/A'
                  },
                  {
                      path: '/A',
                      component: {
                          template: `<div>我是A，我要去B<button @click='goB'>去B</button></div>`,
                          methods: {
                              goB() {
                                  this.$router.push('/B');
                              }
                          }
                      },
                  },
                  {
                      path: '/B',
                      component: {
                          template: `<div>我是B，我要去C<button @click='goC'>去C</button></div>`,
                          methods: {
                              goC() {
                                  this.$router.replace('/C');
                              }
                          }
                      },
                  },
                  {
                      path: '/C',
                      component: {
                          template: `<div>我是C，我要去D<button @click='goD'>去D</button></div>`,
                          methods: {
                              goD() {
                                  this.$router.replace('/D');
                              }
                          }
                      },
                  },
                  {
                      path: '/D',
                      component: {
                          template: `<div>我是D，我要去A<button @click='goA'>去A</button></div>`,
                          methods: {
                              goA() {
                                  // this.$router.push('/cy');
                              }
                          }
                      },
                  },
                 
              ]
          })
          new Vue({
              el: '#app',
              router
          })
      </script>
  
  ```

## 激活路由样式

* 当前选中的模块会有一个class类名`class="router-link-exact-active router-link-active"`

* 所以可以通过设置当前拥有类名的标签，产生一定的样式

  ```html
   <style>
          .router-link-active{
              color: red;
              font-size: 40px;
          }
   </style>
  
  ```

## 路由嵌套

* 二级路由设置通过children属性进行设置，属性值也是一个数组，和routes一样

```html
 <div id="app">
        <router-link to='/hot'>热点</router-link>
        <router-link to='/edu'>教育</router-link>
        <router-link to='/soc'>社会</router-link>
        <router-link to='/music'>音乐</router-link>
        <router-view></router-view>
    </div>
    <script src="./libs/vue.js"></script>
    <script src="./vue-router.js"></script>
    <script>
        var router=new VueRouter({
            routes:[
                {
                    path:'/',
                    redirect:'/hot'
                },
                {
                    path:'/hot',
                    component:{
                        template:`<div>热点</div>`
                    }
                },
                {
                    path:'/edu',
                    component:{
                        template:`<div>教育</div>`
                    }
                },
                {
                    path:'/soc',
                    component:{
                        template:`<div>社会</div>`
                    }
                },
                {
                    path:'/music',
                    children:[
                        {
                            path:'',
                            component:{
                                template:`<p>我是默认的二级路由内容</p>`
                            }
                        },
                        {
                            path:'/music/pop',
                            component:{
                                template:`<div>流行音乐</div>`
                            }
                        },
                        {
                            path:'/music/class',
                            component:{
                                template:`<div>古典音乐</div>`
                            }
                        },
                        {
                            path:'/music/jazz',
                            component:{
                                template:`<div>爵士音乐</div>`
                            }
                        }
                    ],
                    component:{
                        template:`<div>音乐
                            <router-link to="/music/pop">流行音乐</router-link>
                            <router-link to="/music/class">古典音乐</router-link>
                            <router-link to="/music/jazz">爵士音乐</router-link>
                            <router-view></router-view>
                        </div>`
                    }
                }
            ]
        })
        new Vue({
            el:'#app',
            router
        })
    </script>

```



## 生命周期--钩子函数

> 分为四个阶段：（8个钩子函数）
>
> ​	❀实例化Vue对象前后：实例化对象之前的beforeCreate也是摆设
>
> ​		beforeCreate:对象实例化之前，一般不做处理
>
> ​		created:对象实例化完成后：一般用于数据查询（接口调用，获取数据），但是此阶段斌没有完成页面渲染
>
> ​	❀页面渲染完成前后
>
> ​		beforeMount:页面渲染之前，加载数据，查询数据，但是这里依然没有完成页面渲染
>
> ​		mounted:页面渲染完成后，加载数据，页面渲染完成，可以$refs来获取dom对象，可以把查询到的数据更新到页面上
>
> ​	❀数据更新前后：摆设，因为有更好的watch侦听，这个在不同的数据之间没啥区别
>
> ​		beforeUpdate:数据更新前
>
> ​		updated:数据更新后
>
> ​	❀实例销毁前后：实例销毁后destroyed是摆设
>
> ​		beforeDestroy:实例销毁前（将之前定义定时器销毁，因为当某个组件退出江湖之后，操作他的定时器还存在的话，会报错）
>
> ​		destroyed：实例销毁后