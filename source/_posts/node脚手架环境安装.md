---
title: Vue环境安装
date: 2022-05-20 21:58:10
tags:
    node,Vue
categories:
    VueCli
---

## 环境安装

### 一、node

#### 1.**为什么需要node环境**

Vue.js本质上就是一个Js库，可以直接在页面通过script标签引用。这种使用方式只使用了VueJs的”**构建用户界面**“，使用不了他的**模块化**

Vue.js可以在html里直接引用后使用，等到与Vue一起配合使用的第三方应用的库或框架多起来后，一个个从html里引入就不方便了，所有要借用node.js中的npm管理包的引入，是方便包管理.

当我们使用了npm包管理以后，需要编译打包成为浏览器可识别的文件就需要用到node.js中的程序打包工具比如webpack，这些辅助工具让我们在开发的时候可以只关注业务开发，其他的工作交由这些工具提供各种自动化处理，让前端开发更快更简洁

#### 2.下载安装

- nodeJS下载地址：https://nodejs.org/en/download/

- 查看node版本： **node –v**   （安装8以上版本）
- 内置NPM包管理器 查看npm:  **npm -v**

#### 3.NPM镜像

- npm 镜像：

  **淘宝npm镜像**

   registry地址：http://registry.npm.taobao.org/

  **cnpm镜像**

​        registry地址：http://registry.cnpmjs.org/

• **设置镜像源：npm config set registry http://registry.npm.taobao.org/ **

• **查看镜像源：** **npm** **config** **get registry** 



### 二、VueCli脚手架

#### 1.安装

```
npm install -g @vue/cli
```

#### 2.查看版本

```
vue --version

vue -V
```

#### 3.升级

```
npm update -g @vue/cli
```

