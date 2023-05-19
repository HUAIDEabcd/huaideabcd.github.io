---
title: uni-app基础教程
date: 2022-05-20 21:58:10
tags:
    uniapp
categories:
    UniAPP
---

## uni-app基础教程

uni-app是一个使用Vue.js开发所有前端应用的框架，开发者编写一套代码，可发布到iOS，Android，H5，以及各种小程序（微信/支付宝/百度/头条/ QQ /钉钉）等多个平台

## 一、环境配置

### 1.下载HBuilderX

通过HBuilderX可视化界面，HBuilderX内置相关环境，开箱即用，无需配置nodejs

开始之前，开发者需先下载安装如下工具：

- HBuilderX：[官方IDE下载地址](http://www.dcloud.io/hbuilderx.html)

下载App开发版，可开箱即用；如下载标准版，在运行或发行uni-app时，会提示安装uni-app插件，插件下载完成后方可使用。

如使用cli方式创建项目，可直接下载标准版，因为uni-app编译插件被安装到项目下了



### 2.创建uni-app 

在点击工具栏里的文件->新建->项目：

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648524298.png)

选择uni-app类型，输入项目名，选择模板，点击创建，即可成功创建。

uni-app自带的模板有。Hello uni-app，是官方的组件和API示例。还有一个重要模板是uni ui项目模板，日常开发推荐使用该模板，已内置大量常用组件。

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648522188.png)

### 3.运行uni-app

1. 浏览器运行：进入hello-uniapp项目，点击工具栏的运行->运行到浏览器->选择浏览器，即可在浏览器里面体验uni-app的H5版。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648534799.png)
2. 真机运行：连接手机，开启USB调试，进入hello-uniapp项目，点击工具栏的运行->真机运行->选择运行的设备，即可在该设备里面体验uni-app。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648539232.png)如手机无法识别，请点击菜单运行-运行到手机或模拟器-真机运行常见故障排查指南。注意当前开发App也需要安装微信开发者工具。
3. 在微信开发者工具里运行：进入hello-uniapp项目，点击工具栏的运行->运行到小程序模拟器->微信开发者工具，即可在微信开发者工具里面体验uni-app。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648534190.png)注意：如果是第一次使用，需要先配置小程序ide的相关路径，才能运行成功。如下图，需在输入框输入微信开发者工具的安装路径。若HBuilderX不能正常启动微信开发者工具，需要开发者手动启动，然后将uni-app生成小程序工程的路径复制到微信开发者工具里面，在HBuilderX里面开发，在微信开发者工具里面就可以看到实时的效果。uni-app或将项目编译到根目录的unpackage目录。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648543404.png)
4. 在支付宝小程序开发者工具里运行：进入hello-uniapp项目，点击工具栏的运行->运行到小程序模拟器->支付宝小程序开发者工具，即可在支付宝小程序开发者工具里面体验uni -app。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648545095.png)
5. 在百度开发者工具里运行：进入hello-uniapp项目，点击工具栏的运行->运行到小程序模拟器->百度开发者工具，即可在百度开发者工具里面体验uni-app。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648544849.png)
6. 在字节跳动开发者工具里运行：进入hello-uniapp项目，点击工具栏的运行->运行到小程序模拟器->字节跳动开发者工具，即可在字节跳动开发者工具里面体验uni -app。![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648554563.png)

提示

- 如果是第一次使用，需要配置开发工具的相关路径。请点击工具栏的运行->运行到小程序模拟器->运行设置，配置相应的小程序开发者工具的路径。
- 支付宝/百度/字节跳动小程序工具，不支持直接指定项目启动并运行。因此开发工具启动后，替换HBuilderX控制台中提示的项目路径，在相应的小程序开发者工具中打开。
- 如果自动启动小程序22
- 】 发工具失败，请手动启动小程序开发工具放入HBuilderX控制台提示的项目路径，打开项目。

运行的快捷键是Ctrl+r。HBuilderX还提供了快捷运行菜单，可以按数字快速选择要运行的设备：

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011648558276.png)

### 4.目录结构

一个 uni-app 工程，默认包含如下目录及文件：

```
┌─components            uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─hybrid                存放本地网页的目录，详见
├─platforms             存放各平台专用页面的目录，详见
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─wxcomponents          存放小程序组件的目录，详见
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 应用生命周期
├─manifest.json         配置应用名称、appid、logo、版本等打包信息，详见
└─pages.json            配置页面路由、导航条、选项卡等页面类信息，详见
    
```

### 5.手机模拟器

**下载手机模拟器**

MUMU模拟器：https://mumu.163.com/

**模拟器端口：**

|                        |                |
| ---------------------- | -------------- |
| **手机模拟器的名称**   | **默认端口号** |
| Genymotion模拟器       | 5555           |
| 夜神模拟器             | 62001/52001    |
| 海马玩模拟器           | 26944          |
| mumu模拟器             | 7555           |
| 天天模拟器             | 6555           |
| 逍遥安卓模拟器         | 21503          |
| BlueStacks 蓝叠3模拟器 | 5555           |
| 雷神安卓模拟器         | 5555           |
| 腾讯手游助手           | 5555           |



### 应用生命周期

uni-app 支持如下应用生命周期函数：

| 函数名               | 说明                                                    |
| -------------------- | ------------------------------------------------------- |
| onLaunch             | 当`uni-app`初始化完成时触发（局部只触发一次）           |
| onShow               | 当`uni-app`启动，或从后台进入前台显示                   |
| onHide               | 当`uni-app`从前台进入后台                               |
| onError              | 当`uni-app`报错时触发                                   |
| onUniNViewMessage    | 对`nvue`页面发送的数据进行监听，可参考 nvue 向 vue 通讯 |
| onUnhandledRejection | 对未处理的 Promise 拒绝事件监听函数（2.8.1+）           |
| onPageNotFound       | 页面不存在监听函数                                      |
| onThemeChange        | 监听系统主题变化                                        |

注意：**应用生命周期仅可在 App.vue 中监听，在其他页面监听无效**

### 页面生命周期

uni-app 支持如下页面生命周期函数：

| 函数名                              | 说明                                                         | 平台差异说明                                         | 最低版本 |
| ----------------------------------- | ------------------------------------------------------------ | ---------------------------------------------------- | -------- |
| onInit                              | 监听页面初始化，其参数通onLoad参数，为上个页面传递的数据，参数类型为Object（用于页面传参），触发时机早于onLoad | 百度小程序                                           | 3.1.0+   |
| onLoad                              | 监听页面加载，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参） |                                                      |          |
| onShow                              | 监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回进入当前页面 |                                                      |          |
| onReady                             | 监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发 |                                                      |          |
| onHide                              | 监听页面隐藏                                                 |                                                      |          |
| onUnload                            | 监听页面卸载                                                 |                                                      |          |
| onResize                            | 监听窗口尺寸变化                                             | App，微信小程序                                      |          |
| onPullDownRefresh                   | 监听用户拖动动作，一般用于拖动刷新，参考示例                 |                                                      |          |
| onReachBottom                       | 页面上拉触底事件的处理函数                                   |                                                      |          |
| onTabItemTap                        | 单击选项卡时触发，参数为对象，具体见以下注意事项             | 微信小程序，百度小程序，H5，App（自定义组件模式）    |          |
| onShareAppMessage                   | 用户点击右上角分享                                           | 微信小程序，百度小程序，字节跳动小程序，支付宝小程序 |          |
| onPageScroll                        | 监听页面滚动，参数为对象                                     | nvue 暂不支持                                        |          |
| onNavigationBarButtonTap            | 监听原生标题栏按钮点击事件，参数为对象                       | 5+ App，H5                                           |          |
| onBackPress                         | 监听页面返回，返回事件= {from：backbutton，navigationBack}，backbutton 表示来源是左上角返回按钮或android 返回键； navigateBack 表示来源是 uni.navigateBack；详细说明及使用：onBackPress 详解。支付宝小程序只有真机能触发，只能监听非 navigateBack 引起的返回，不可阻止默认行为。 | App，H5、支付宝小程序                                |          |
| onNavigationBarSearchInputChanged   | 监听原生标题栏搜索输入框输入内容变化事件                     | App，H5                                              | 1.6.0    |
| onNavigationBarSearchInputConfirmed | 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。 | App，H5                                              | 1.6.0    |
| onNavigationBarSearchInputClicked   | 监听原生标题栏搜索输入框点击事件                             | App，H5                                              | 1.6.0    |
| onShareTimeline                     | 监听用户点击右上角转发到朋友去                               | 微信小程序                                           | 2.8.1+   |
| onAddToFavorites                    | 监听用户点击右上角收藏                                       | 微信小程序                                           | 2.8.1+   |

onInit使用注意

- 仅百度小程序基础库 3.260 以上支持 onInit 生命周期
- 其他版本或平台可以同时使用 onLoad 生命周期进行兼容，注意避免重复执行相同逻辑
- 不依赖页面传参的逻辑可以直接使用 created 生命周期替代

### 组件生命周期

`uni-app` 组件支持的生命周期，与 vue 标准组件的生命周期相同。这里没有页面级的 onLoad 等生命周期：

| 函数名        | 说明                                                         | 平台差异说明   | 最低版本 |
| ------------- | ------------------------------------------------------------ | -------------- | -------- |
| beforeCreate  | 在实例初始化之后被调用。[详见](https://cn.vuejs.org/v2/api/#beforeCreate) |                |          |
| created       | 在实例创建完成后被立即调用。[详见](https://cn.vuejs.org/v2/api/#created) |                |          |
| beforeMount   | 在挂载开始之前被调用。[详见](https://cn.vuejs.org/v2/api/#beforeMount) |                |          |
| mounted       | 挂载到实例上去之后调用。[详见](https://cn.vuejs.org/v2/api/#mounted) 注意：此处并不能确定子组件被全部挂载，如果需要子组件完全挂载之后在执行操作可以使用`$nextTick`[Vue官方文档](https://cn.vuejs.org/v2/api/#Vue-nextTick) |                |          |
| beforeUpdate  | 数据更新时调用，发生在虚拟 DOM 打补丁之前。[详见](https://cn.vuejs.org/v2/api/#beforeUpdate) | 仅 H5 平台支持 |          |
| updated       | 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。[详见](https://cn.vuejs.org/v2/api/#updated) | 仅 H5 平台支持 |          |
| beforeDestroy | 实例销毁之前调用。在这一步，实例仍然完全可用。[详见](https://cn.vuejs.org/v2/api/#beforeDestroy) |                |          |
| destroyed     | Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。[详见](https://cn.vuejs.org/v2/api/#destroyed) |                |          |



## 三、路由

uni-app页面路由为框架统一管理，需要在pages.json里配置每个路由页面的路径和页面样式。类似的小程序在app.json中配置页面路由相同

### 页面栈

框架以栈的形式管理当前所有页面，当发生路由切换的时候，页面栈的表现如下：

| 路由方式 | 页面栈表现                       | 触发时机                                                     |
| :------- | -------------------------------- | ------------------------------------------------------------ |
| 初始化   | 新页面入栈                       | uni-app：的第一个页面                                        |
| 新页面   | 新页面入栈                       | 调用API  uni.navigateTo ，使用组件  <navigator open-type =“ navigate” /> |
| 页面重启 | 当前页面出栈，新页面入栈         | 调用API  uni.redirectTo ，使用组件 <navigator open-type =“ redirectTo” /> |
| 页面返回 | 页面不断出栈，直到目标返回页     | 调用API  uni.navigateBack  ，使用组件 <navigator open-type =“ navigateBack” /> ，用户按左上角返回按钮，安卓用户点击物理后退键 |
| 标签切换 | 页面全部出栈，只留下新的标签页面 | 调用API  uni.switchTab  ，使用组件 <navigator open-type =“ switchTab” />  ，用户切换Tab |
| 重加载   | 页面全部出栈，只留下新的页面     | 调用API  uni.reLaunch  ，使用组件  <navigator open-type =“ reLaunch” /> |

### 判断平台

平台判断有2种场景，一种是在编译期判断，一种是在运行期判断。

- 编译期判断编译期判断，即条件编译，不同平台在编译出包后已经是不同的代码

```js
// #ifdef H5
    alert("只有h5平台才有alert方法")
// #endif
```

- 运行期诊断运行期判断是指代码已经打入包中，仍然需要在运行期判断平台，此时可使用uni.getSystemInfoSync().platform判断客户端环境是Android，iOS还是小程序开发工具（在百度小程序开发工具，微信小程序开发工具，支付宝小程序开发工具中使用uni.getSystemInfoSync().platform返回值重置devtools）。

```js
switch(uni.getSystemInfoSync().platform){
    case 'android':
       console.log('运行Android上')
       break;
    case 'ios':
       console.log('运行iOS上')
       break;
    default:
       console.log('运行在开发者工具上')
       break;
}
```

## 四、样式布局

uni-app 支持的通用 css 单位包括 px、rpx

- px 即屏幕像素
- rpx 即响应式px，一种根据屏幕宽度自适应的动态单位。以750宽的屏幕为基准，750rpx恰好为屏幕宽度。屏幕变宽，rpx 实际显示效果会等比放大。

vue页面支持普通H5单位，但在nvue里不支持：

- rem 默认根字体大小为 屏幕宽度/20（微信小程序、字节跳动小程序、App、H5）
- vh viewpoint height，视窗高度，1vh等于视窗高度的1%
- vw viewpoint width，视窗宽度，1vw等于视窗宽度的1%

nvue还不支持百分比单位。

App端，在 pages.json 里的 titleNView 或页面里写的 plus api 中涉及的单位，只支持 px。注意此时不支持 rpx

nvue中，uni-app 模式（nvue 不同编译模式介绍）可以使用 px 、rpx，表现与 vue 中一致。weex 模式目前遵循weex的单位，它的单位比较特殊：

- px:，以750宽的屏幕为基准动态计算的长度单位，与 vue 页面中的 rpx 理念相同。（一定要注意 weex 模式的 px，和 vue 里的 px 逻辑不一样。）
- wx：与设备屏幕宽度无关的长度单位，与 vue 页面中的 px 理念相同

### 样式导入

使用@import语句可以导入外联样式表，@import后跟需要导入的外联样式表的相对路径，用;表示语句结束。

```html
<style>
    @import "../../common/uni.css";

    .uni-card {
        box-shadow: none;
    }
</style>
```

### 内联样式

框架组件上支持使用 style、class 属性来控制组件的样式。

- style：<view :style="{color:color}" />
- class：<view class="normal_view" />

### 选择器

目前支持的选择器有：

| 选择器           | 样例           | 样例描述                                            |
| ---------------- | -------------- | --------------------------------------------------- |
| .class           | .intro         | 选择所有拥有 class="intro" 的组件                   |
| #id              | #firstname     | 选择拥有 id="firstname" 的组件                      |
| element          | view           | 选择所有 view 组件                                  |
| element, element | view, checkbox | 选择所有文档的 view 组件和所有的 checkbox 组件      |
| ::after          | view::after    | 在 view 组件后边插入内容，**仅微信小程序和App生效** |
| ::before         | view::before   | 在 view 组件前边插入内容，**仅微信小程序和App生效** |

注意：

- 在 uni-app 中不能使用 * 选择器。
- page 相当于 body 节点，例如：<!-- 设置页面背景颜色 --> page { background-color:#ccc; }

### 全局样式与局部样式

定义在 App.vue 中的样式为全局样式，作用于每一个页面。在 pages 目录下 的 vue 文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖 App.vue 中相同的选择器。

注意：

- App.vue 中通过 @import 语句可以导入外联样式，一样作用于每一个页面。
- nvue页面暂不支持全局样式

### 背景图片

uni-app 支持使用在 css 里设置背景图片，使用方式与普通 web 项目大体相同，但需要注意以下几点：

- 支持 base64 格式图片。
- 支持网络路径图片。
- 小程序不支持在css中使用本地文件，包括本地的背景图和字体文件。需以base64方式方可使用
- 使用本地路径背景图片需注意：在背景图片小于 40kb 时，uni-app 编译到不支持本地背景图的平台时，会自动将其转化为 base64 格式；图片大于等于 40kb，会有性能问题，不建议使用太大的背景图，如必须使用，则需自己将其转换为 base64 格式使用，或将其挪到服务器上，从网络地址引用。本地背景图片的引用路径推荐使用以 ~@ 开头的绝对路径。 .test2 { background-image: url('~@/static/logo.png'); }

**注意**

- 微信小程序不支持相对路径（真机不支持，开发工具支持）

### 字体图标

uni-app 支持使用字体图标，使用方式与普通 web 项目相同，需要注意以下几点：

- 支持 base64 格式字体图标。
- 支持网络路径字体图标。
- 小程序不支持在css中使用本地文件，包括本地的背景图和字体文件。需以base64方式方可使用。
- 网络路径必须加协议头 https。
- 从 [http://www.iconfont.cn](http://www.iconfont.cn/) 上拷贝的代码，默认是没加协议头的。
- 从 [http://www.iconfont.cn](http://www.iconfont.cn/) 上下载的字体文件，都是同名字体（字体名都叫iconfont，安装字体文件时可以看到），在nvue内使用时需要注意，此字体名重复可能会显示不正常。
- 使用本地路径图标字体需注意：在字体文件小于 40kb 时，uni-app 会自动将其转化为 base64 格式；字体文件大于等于 40kb，仍转换为 base64 方式使用的话可能有性能问题，如必须使用，则需自己将其转换为 base64 格式使用，或将其挪到服务器上，从网络地址引用；字体文件的引用路径推荐使用以 ~@ 开头的绝对路径。 @font-face { font-family: test1-icon; src: url('~@/static/iconfont.ttf'); }

nvue中不可直接使用css的方式引入字体文件，需要使用以下方式在js内引入。nvue内不支持本地路径引入字体，请使用网络链接或者base64形式。src字段的url的括号内一定要使用单引号。

```js
var domModule = weex.requireModule('dom');
domModule.addRule('fontFace', {
  'fontFamily': "fontFamilyName",
  'src': "url('https://...')"
})
```

示例：

```js
<template>
    <view>
        <view>
            <text class="test">&#xe600;</text>
            <text class="test">&#xe687;</text>
            <text class="test">&#xe60b;</text>
        </view>
    </view>
</template>
<style>
    @font-face {
        font-family: 'iconfont';
        src: url('https://at.alicdn.com/t/font_865816_17gjspmmrkti.ttf') format('truetype');
    }
    .test {
        font-family: iconfont;
        margin-left: 20rpx;
    }
</style>
```

### `<template/>`和`<block/>` 

uni-app 支持在 template 模板中嵌套 <template/> 和 <block/>，用来进行 列表渲染 和 条件渲染。

<template/> 和 <block/> 并不是一个组件，它们仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。

代码示例

```js
<template>
    <view>
        <template v-if="test">
            <view>test 为 true 时显示</view>
        </template>
        <template v-else>
            <view>test 为 false 时显示</view>
        </template>
    </view>
</template>
<template>
    <view>
        <block v-for="(item,index) in list" :key="index">
            <view>{{item}} - {{index}}</view>
        </block>
    </view>
</template>
```

## 五、条件编译

### 条件编译

条件编译是用特殊的**注释**作为标记，在编译时根据这些特殊的注释，将注释里面的代码编译到不同平台。

写法：以 **#ifdef** 或 **#ifndef** 加 **%PLATFORM%** 开头，以 **#endif** 结尾。

- \#ifdef：if defined 仅在某平台存在
- \#ifndef：if not defined 除了某平台均存在
- %PLATFORM%：平台名称

| 条件编译写法                                             | 说明                                                         |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| #ifdef **APP-PLUS** 需条件编译的代码 #endif              | 仅出现在 App 平台下的代码                                    |
| #ifndef **H5** 需条件编译的代码 #endif                   | 除了 H5 平台，其它平台均存在的代码                           |
| #ifdef **H5** \|\| **MP-WEIXIN** 需条件编译的代码 #endif | 在 H5 平台或微信小程序平台存在的代码（这里只有\|\|，不可能出现&&，因为没有交集） |

%PLATFORM% 可取值如下：

| 值            | 平台                                                       |
| ------------- | ---------------------------------------------------------- |
| APP-PLUS      | App                                                        |
| APP-PLUS-NVUE | App nvue                                                   |
| H5            | H5                                                         |
| MP-WEIXIN     | 微信小程序                                                 |
| MP-ALIPAY     | 支付宝小程序                                               |
| MP-BAIDU      | 百度小程序                                                 |
| MP-TOUTIAO    | 字节跳动小程序                                             |
| MP-QQ         | QQ小程序                                                   |
| MP            | 微信小程序/支付宝小程序/百度小程序/字节跳动小程序/QQ小程序 |

支持的文件

- .vue
- .js
- .css
- pages.json
- 各预编译语言文件，如：.scss、.less、.stylus、.ts、.pug

注意： 条件编译是利用注释实现的，在不同语法里注释写法不一样，js使用 // 注释、css 使用 /* 注释 */、vue/nvue 模板里使用 <!-- 注释 -->；

### API 的条件编译

```
// #ifdef  %PLATFORM%
平台特有的API实现
// #endif
```

示例，如下代码仅在 App 下出现:

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011802238739.png)

示例，如下代码不会在 H5 平台上出现：

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011802241844.png)

除了支持单个平台的条件编译外，还支持多平台同时编译，使用 || 来分隔平台名称。

示例，如下代码会在 App 和 H5 平台上出现：

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011802243759.png)

### 组件的条件编译

```
<!--  #ifdef  %PLATFORM% -->
平台特有的组件
<!--  #endif -->
```

示例，如下广告组件仅会在微信小程序中出现：

![uniapp](https://atts.w3cschool.cn/attachments/day_200401/202004011802252870.png)

### 样式的条件编译

```
/*  #ifdef  %PLATFORM%  */
平台特有样式
/*  #endif  */
```

注意： 样式的条件编译，无论是 css 还是 sass/scss/less/stylus 等预编译语言中，必须使用 /*注释*/ 的写法。

正确写法

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011802252730.png)

错误写法

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011802257137.png)

### pages.json 的条件编译

下面的页面，只有运行至 App 时才会编译进去。

![img](https://atts.w3cschool.cn/attachments/day_200401/202004011802265419.png)

不同平台下的特有功能，以及小程序平台的分包，都可以通过 pages.json 的条件编译来更好地实现。这样，就不会在其它平台产生多余的资源，进而减小包体积。

### 注意

- Android 和 iOS 平台不支持通过条件编译来区分，如果需要区分 Android、iOS 平台，请通过调用 uni.getSystemInfo 来获取平台信息。支持ifios、ifAndroid代码块，可方便编写判断。

