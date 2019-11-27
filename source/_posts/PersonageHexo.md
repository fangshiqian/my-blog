---
title: 搭建使用 Hexo 结合 GitHub Pages 搭建静态网 站
date: 2019-11-27 20:42:57
top:
categories: 工具
tags: 工具
---
> ​	Hexo官网: https://hexo.io/zh-cn/docs/index.html 
>
> ​	安装依赖:node.js	git
> ​	新建一个文件

## 1. 安装 Hexo

```javascript
1. npm install -g hexo-cli
2. hexo --version    (确认是否安装成功)
```

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E7%A1%AE%E8%AE%A4%E6%98%AF%E5%90%A6%E5%AE%89%E8%A3%85%E6%88%90%E5%8A%9F)

​			成功样式

## 2. 生成自己的网站

> ```javascript
> hexo init 网站项目目录名称
> ```
>
> 
>
> ```javascript
> hexo init my-blog			(举例)
> ```
>
> 

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E7%9B%AE%E5%BD%95)

## 3. 本地预览

> 在你的网站目录下执行该命令，它会启动一个本地 http 服务，用于预览 
>
> ```javascript
> npm run build
> ```
>
> ​	 部署
>
> ```javascript
> hexo server
> ```
>
> ​	 本地预览

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E6%9C%AC%E5%9C%B0%E9%A2%84%E8%A7%88)

注意: 查看完本地的这个之后直接关闭就可以了

## 4. 目录结构

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E7%9B%AE%E5%BD%95)

* node_modules 第三方包
* scaﬀolds 文章模板
* source 源代码，markdown
* themes 主题目录

## 5. 写文章

在项目的`source/_posts`中创建 Markdown 文件并写入：

```javascript
--title: 文章标题
--
Markdown内容...
```

只需要创建文件写就可以了，不需要做任何操作。

更多内容请参考： https://hexo.io/zh-cn/docs/writing 。

## 6. 如何部署(一步都不能错)

步骤3执行完 =>  执行命令:hexo generate

 生成静态文件。

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E6%96%87%E4%BB%B6)

这个就是要部署的一个文件

然后GIT推送到GitHub仓库

启动GitHub page 方式

这种方式麻烦(不适用)!!!!!!!!!!!!!!!!!!

以上方法适合本地测试使用!!!!!!!!!!!!!

## 7. 自动发布(远程仓库-正式安装)

### 7.1 准备

> ```javascript
> 1. hexo init my-blogs	创建文件夹
> ```

> ​	2. 在GitHub上创建远程仓库,下图所示:

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E4%BB%93%E8%BF%9C%E7%A8%8B%E5%BA%93)

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E6%9C%AC%E5%9C%B0%E4%BF%AE%E6%94%B9)

​	提交到远程仓库

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E6%8F%90%E4%BA%A4%E5%88%B0%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93)

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E4%BB%93%E5%BA%93)

### 7.2 在远程仓库部署

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E9%83%A8%E7%BD%B2)





![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/2)





![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E9%98%BF%E8%90%A8%E5%BE%B7)

​																						滑到最下边

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E5%AE%89%E6%85%B0)





![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E9%98%BF%E6%96%AF%E9%A1%BF)



![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/123)

```javascript
ACCESS_TOKEN

// Name 为该字段 复制即可
```





![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/123%E7%88%B1%E6%88%91%E7%9A%84)



![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/2374)

```js
name: GitHub Actions Build and Deploy Demo 
on:
  push:
    branches:
      - master 
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@master
        
      - name: Build and Deploy
        uses: JamesIves/github-pages-deploy-action@master
        env:
          ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
          BRANCH: gh-pages
          FOLDER: public
          BUILD_SCRIPT: npm install && npm run build
          
          // 复制该字段到Edit 里面
```





![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E5%87%A0%E5%8D%81%E5%9D%97)



![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E4%BD%BF%E7%94%A8)



![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/1231%E4%BD%8D)

​																					打开上面网址,查看是否能打开



## 8. [更换主题(点击此处获取连接)]( https://hexo.io/themes/ )

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/12312)



![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/12334%E6%89%8B%E6%89%93)

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/23454352)

​																						文件名改成git clone 后缀的名字

​																			解压成这样到这个文件放到my-blogs/themes 文件夹下

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/123%E8%AF%B7%E9%97%AE)

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E9%A9%B1%E8%9A%8A%E5%99%A8)

## 9. 直接推送到远程仓库,具体怎么修改内容参考主题文档(这个时候可以直接打开你的页面了)

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/1231242)



![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/12312434121)

## 10. 以后每次修改直好接提交到远程仓库,GitHub会自动发布