---
title: Webpack
date: 2018-12-03 09:33:09
top:
categories:
   - 学习
   - Webpack
tags: Webpack
---

# Webpack

* webpack是一个模块打包器，它本身主要打包js模块，结合生态中的一些loader可以实现对很多其他资源的打包，例如less,sass，图片，es6转es5,vue等等文件资源都可以
* 使用webpack,我们最终就能使用类似于vueCLI这个根据提供给我们的功能
  * 打包js
  * 打包css
  * 打包图片
  * 打包less
  * 打包less
  * 打包vue资源
  * 开发阶段的web服务
  * 代码热更新
  * 打包部署命令
  * ……
* webpack之前，还有一些别的构建工具
  * grunt
  * gulp
  * 百度的FIS
  * parcel:`https://parceljs.org/`
  * rollup
* 现在webpack已经被各大前端框架作为自己的脚手架工具的基层，例如：
  * Vue:VueCLI
  * React:crate-react-app
  * Angular:angular-cli
* 本身webpack只能打包javascript
* 参考文档：`官方文档：https://webpack.docschina.org/`







## webpack打包过程

### 准备

* 创建demo练习项目
* 在内部创建src文件夹
* 在src中创建叫`index.js`的文件，现在必须叫index.js，后面在进行配置修改
* 在src文件夹中创建foo.js
* 在src文件夹中创建index.html的文件



### 准备webpack

* 创建一个叫package.json文件（用于保存安装包的依赖信息），此文件无需手动创建，只需要在demo目录下，输入命令`npm init -y|npm init`,就会自动产生该文件

* 安装webpack到项目的开发依赖中，在demo目录下，输入命令`yarn add --dev webpack webpack-cli|yarn add -D webpack webpack-cli|npm install -D webpack webpack-cli|npm install --save-dev webpack webpack-cli`当安装完webpack和webpack-cli之后，demo文件夹会出现`nodee_modules和package-lock.json`两个文件

  * 其中所有的开发工具相关的包的依赖信息保存到devDependencies中，其实就是一个归类，都是安装包到项目

* 将`package.json`文件中的scripts中新增代码

  ![1575034547401](E:\black\就业班\webpack\assets\1575034547401.png)

* 在命令行中执行`npm run build`，npm就会找到package.json中的build配置项，运行webpack构建打包，此时执行完该命令就会发现demo文件夹下，多出来`dist`文件夹

  * webpack默认会找到src的`index.js`作为`打包的入口`，然后从入口分析所有的依赖:
    * a依赖了b
    * b依赖了c
    * a依赖了b
    * ……
    * 所有依赖的文件
  * 将他们编译构建处理，最终生成一个默认名字叫`main.js`文件写入dist目录
  * 在你的html文件中加载打包的结果dist/main.js进行访问测试，此时便看到相应的结果

  

  

## 配置文件

### 配置出口和入口文件



* webpack打包的入口和出口具有默认规则，如果想要自定义，或者其他一些更高级的功能配置，那么我们需要使用配置文件

  > rm -rf .git删除一切，不要乱来

* 在项目的根目录中创建`webpack.config.js`并写入

  > ```javascript
  > var path = require('path');
  > 
  > module.exports = {
  > mode: 'development',
  > entry: './src/main.js',
  > output: {
  >  path: path.resolve(__dirname, 'dist'),
  >  filename: 'bundle.js'
  > }
  > };
  > ```

* 在package.json中修改build配置项（非必须）

  > "scripts": {
  >
  > ​    "build":"webpack --config webpack.config.json"
  >
  > },

* 修改完成之后，进行重新打包构建`npm run build|yarn run build|yarn build`

* 关于npm中的scripts小知识：当在命令行中输入`npm run b`，也会同时出发preb,postb命令执行----`钩子`

  >"scripts": {
  >
  >​    "build": "webpack --config webpack.config.js",
  >
  >​    "preb": "node a.js",
  >
  >​    "b": "node b.js",
  >
  >​    "postb": "node c.js"
  >
  >},

  

### 打包模式mode

* development：开发模式，更快的打包速度（无优化，没有压缩）
* production：生产模式，更优的打包结果（优化，例如代码压缩）`默认`
* 在webpack.config.js中写入：

>   mode: 'development',





## 打包css

* 已知webpack只对js进行打包，如果想要对其他资源进行打包，需要利用loader插件，进行相关的配置

* 具体配置步骤

  * 安装：`npm install --save-dev style-loader css-loader`

  * 在main.js入口文件中引入css文件`import './style/index.css'`

  * 在webpack.config.js中添加：

    > ```js
    > module.exports = {
    > module: {
    >  rules: [
    >    {
    >      test: /\.css$/i,
    >      use: ['style-loader', 'css-loader'],
    >    },
    >  ],
    > },
    > };
    > ```



## 打包图片

* 安装`npm install --save-dev file-loader`

* 在webpack.config.js中写入：

  > ```diff
  > module.exports = {
  >  entry: './src/index.js',
  >  output: {
  >    filename: 'bundle.js',
  >    path: path.resolve(__dirname, 'dist'),
  >  },
  >  module: {
  >    rules: [
  >      {
  >        test: /\.css$/,
  >        use: [
  >          'style-loader',
  >          'css-loader'
  >        ],
  >      },
  > +       {
  > +         test: /\.(png|svg|jpg|gif)$/,
  > +         use: [
  > +           'file-loader',
  > +         ],
  > +       },
  >       ],
  >     },
  >   };
  > ```



## 打包html文件

* 为了解决打包之后的路径问题，我们必须把html文件也打包到dist目录中，然后运行dist中的html文件

* 安装`npm install --save-dev html-webpack-plugin`

* 在webpack.config.js中添加：

* 参考文档：`https://github.com/jantimon/html-webpack-plugin`

  > ```diff
  > const path = require('path');
  > + const HtmlWebpackPlugin = require('html-webpack-plugin');
  > 
  >   module.exports = {
  >     entry: {
  >       app: './src/index.js',
  >       print: './src/print.js',
  >     },
  > +   plugins: [
  > +     new HtmlWebpackPlugin({
  > +       title: 'Output Management',
  > +     }),
  > +   ],
  >     output: {
  >       filename: '[name].bundle.js',
  >       path: path.resolve(__dirname, 'dist'),
  >     },
  >   };
  > ```





## 自动清除dist目录

* 安装：`npm install --save-dev clean-webpack-plugin`

* 在webpack.config.js中写入：

  > ```diff
  > const path = require('path');
  > const HtmlWebpackPlugin = require('html-webpack-plugin');
  > + const { CleanWebpackPlugin } = require('clean-webpack-plugin');
  > 
  >   module.exports = {
  >     entry: {
  >       app: './src/index.js',
  >       print: './src/print.js',
  >     },
  >     plugins: [
  > +     new CleanWebpackPlugin(),
  >       new HtmlWebpackPlugin({
  >         title: 'Output Management',
  >       }),
  >     ],
  >     output: {
  >       filename: '[name].bundle.js',
  >       path: path.resolve(__dirname, 'dist'),
  >     },
  >   };
  > ```



## 打包字体文件

* 安装：`npm install --save-dev file-loader`

* 在webpack.config.js中添加：

  > ```diff
  > const path = require('path');
  > 
  > module.exports = {
  >  entry: './src/index.js',
  >  output: {
  >    filename: 'bundle.js',
  >    path: path.resolve(__dirname, 'dist'),
  >  },
  >  module: {
  >    rules: [
  >      {
  >        test: /\.css$/,
  >        use: [
  >          'style-loader',
  >          'css-loader'
  >        ],
  >      },
  >      {
  >        test: /\.(png|svg|jpg|gif)$/,
  >        use: [
  >          'file-loader',
  >        ],
  >      },
  > +       {
  > +         test: /\.(woff|woff2|eot|ttf|otf)$/,
  > +         use: [
  > +           'file-loader',
  > +         ],
  > +       },
  >       ],
  >     },
  >   };
  > ```

## 打包less

* 安装：`npm install less-loader style-loader css-loader --save-dev`

* 在webpack.config.js中添加：

  > ```js
  > module.exports = {
  > module: {
  >  rules: [
  >    {
  >      test: /\.less$/,
  >      use: [
  >        {
  >          loader: 'style-loader', // creates style nodes from JS strings
  >        },
  >        {
  >          loader: 'css-loader', // translates CSS into CommonJS
  >        },
  >        {
  >          loader: 'less-loader', // compiles Less to CSS
  >        },
  >      ],
  >    },
  >  ],
  > },
  > };
  > ```

## 打包ES转ES5

* w为了能让代码中的ES6能运行在低版本的浏览器，我们需要把ES6转为ES5向下兼容

* babel是一个专门将ES6转ES5的编译工具

* 安装：`npm install -D babel-loader @babel/core @babel/preset-env webpack`

* 在webpack.config.js中配置

  > ```javascript
  > module: {
  > rules: [
  >  {
  >    test: /\.m?js$/,
  >    exclude: /(node_modules|bower_components)/,
  >    use: {
  >      loader: 'babel-loader',
  >      options: {
  >        presets: ['@babel/preset-env']
  >      }
  >    }
  >  }
  > ]
  > }
  > ```

## API兼容处理

* 通过以上配置，只能把基本的语法转换兼容处理，例如：const,let,箭头函数，解构赋值……，但是不会处理一些API方法，例如：字符串的includes方法，数组的includes方法，find,findIndex,includes……

* 参考文档:https://www.babeljs.cn/docs/babel-polyfill

* 安装：`npm install --save @babel/polyfill`

* webpack.config.js中设置：

  > module.exports = {
  > entry: ["@babel/polyfill", "./app/js"],
  > };



## 开启缓存

* babel打包比较耗时，当代码文件比较多的时候，开启缓存，提高打包的效率

* 在webpack.config.js中设置：

  > ```js
  > module: {
  > rules: [
  >  {
  >    test: /\.m?js$/,
  >    exclude: /(node_modules|bower_components)/,
  >    use: {
  >      loader: 'babel-loader',
  >      options: {
  >        presets: ['@babel/preset-env'],
  >        cacheDirectory: true
  >      }
  >    }
  >  }
  > ]
  > }
  > 
  > ```

## source maps

* 源码导航，让代码行数和实际文件一一对应

* 在webpack.config.js中设置

  > devtool: 'source-map',

## 使用watch监视模式

* 自动执行npm run build

* 在package.json中添加：

  > "scripts": {
  >
  > ​    "build": "webpack",
  >
  > ​    "watch": "webpack --config webpack.config.js --watch"
  >
  > },

## 使用webpack-dev-server

* 开启Web服务器

* 监视打包

* `自动刷新浏览器`

* 安装：`npm install --save-dev webpack-dev-server`

* 在webpack.config.js中设置：

  >  devServer: {
  >
  >  ​        contentBase: './dist',
  >
  >  ​        open: false
  >
  >  ​    },

* 在package.json中添加

>  "scripts": {
>
>  ​    "build": "webpack",
>
>  ​    "watch": "webpack --config webpack.config.js --watch",
>
>  ​    "serve": "webpack-dev-server --open"
>
>  },



## 热更新

* webpack-dev-serve默认是刷新整个页面实现更新，，有一种更好的方式叫热更新，可以实现不刷新页面的情况下更新内容变化
* 注意：对js不支持热更新

> devServer: {
>
> ​        contentBase: './dist',
>
> ​        hot:true,
>
> ​        open: false
>
> ​    },



## 打包vue

* 安装：`npm install -D vue-loader vue-template-compiler`

* 配置webpack.config.js

* 参考文档：`<https://vue-loader.vuejs.org/guide/#manual-setup>`

  > ```js
  > // webpack.config.js
  > const VueLoaderPlugin = require('vue-loader/lib/plugin')
  > 
  > module.exports = {
  > module: {
  >  rules: [
  >    // ... other rules
  >    {
  >      test: /\.vue$/,
  >      loader: 'vue-loader'
  >    }
  >  ]
  > },
  > plugins: [
  >  // make sure to include the plugin!
  >  new VueLoaderPlugin()
  > ]
  > }
  > 
  > ```

## 配置解析的后缀名

* webpack默认只支持

  * .wasm
  * mjs
  * js
  * json等后缀名可以省略

* 如果想要设置其他后缀名，需要配置

  >  resolve: {
  >       // 可以省略的文件扩展名
  >       // 默认 resolve: {extensions: ['.wasm', '.mjs', '.js', '.json'] }
  >       extensions: ['.js', '.vue', '.json']
  >  },

## 配置路径别名

* 类似在VueCLI使用@表示src路径

* 在webpack.config.js中额resolve中添加

  > resolve: {
  >
  > ​        // 可以省略的文件扩展名
  >
  > ​        // 默认 resolve: {extensions: ['.wasm', '.mjs', '.js', '.json'] }
  >
  > ​        extensions: ['.js', '.vue', '.json'],
  >
  > ​        alias: {
  >
  > ​            // 名字：值
  >
  > ​            // 注意对象的键名如果是特殊符号，必须加引号
  >
  > ​            "@": path.join(__dirname, './src')
  >
  > ​        }
  >
  > ​    },

## 使用ESLint

* ESlint是专门用于JavaScript代码格式校验的工具

* 安装:`npm install eslint eslint-loader --save-dev`

* 配置webpack.config.js

  >  // 配置ESlint
  >
  >  ​            {
  >
  >  ​                // 注意必须有强制提前
  >
  >  ​                enforce: 'pre',
  >
  >  ​                test: /\.js$/,
  >
  >  ​                // 排除 exclude 
  >
  >  ​                // 排除第三方包 格式校验只需要校验我们自己的代码就可以了，不需要校验第三方包
  >
  >  ​                exclude: /node_modules/,
  >
  >  ​                loader: 'eslint-loader',
  >
  >  ​            },

* 在命令行中输入：`.\node_modules\.bin\eslint.cmd --init`

  ![1575048618713](E:\black\就业班\webpack\assets\1575048618713.png)

  ![1575048686616](E:\black\就业班\webpack\assets\1575048686616.png)

  ![1575048707731](E:\black\就业班\webpack\assets\1575048707731.png)

  ![1575048729422](E:\black\就业班\webpack\assets\1575048729422.png)

  ![1575048750739](E:\black\就业班\webpack\assets\1575048750739.png)

  ![1575048777730](E:\black\就业班\webpack\assets\1575048777730.png)

  ![1575048803533](E:\black\就业班\webpack\assets\1575048803533.png)

  ![1575048821668](E:\black\就业班\webpack\assets\1575048821668.png)

  ![1575048848841](E:\black\就业班\webpack\assets\1575048848841.png)

  

  ## 配置校验规则

  * ESLint附带大量的规则，你可以使用注释或者配置文件修改你的项目中要使用的规则，要改变的一个规则设置，你必须将规则ID设置为下列之一：

    > "off" 或 0 - 关闭规则
    > "warn" 或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
    > "error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)

  * 在.elintrc.js中进行设置

    > // 配置代码校验规则
    >
    > rules: {
    >
    > ​    // off 就是关闭
    >
    > ​    // 规则id(代号):控制选项
    >
    > ​    'no-new': 'off',
    >
    > ​    semi:['error','always']
    >
    > }

  * 也可以在代码中使用注释临时控制代码格式校验

  * 为了在文件注释里配置规则，使用以下格式的注释：

    > /* eslint eqeqeq: "off", curly: "error" */

  * 更多配置建议参考 https://eslint.bootcss.com/docs/user-guide/configuring/

  ​                                                

## 在Vue-CLI创建项目中配置webpack

* 优化
  * 打包的速度
  * 打包的结果