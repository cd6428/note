#### 1.小程序中如何阻止事件的冒泡

```js
<button type="primary" catch:tap="clickMe">clickMe</button>
```

将之间的bind:tap="clickMe"改写成为catch:tap="clickMe",这样当点击按钮时就不会触发冒泡行为

事件默认是在冒泡阶段执行



```js
<button type="primary" capture-bind:tap="clickYou">clickYou</button>
```

将事件的执行机制更改为在捕获阶段执行,了解即可,这样的用户体验很不好





```js
<button type="primary" mut-bind:tap="clickHei">clickHei</button>
```

设置互斥点击事件,也就是说设置了互斥的点击事件的按钮,只会触发被点击按钮的逻辑





#### 2.小程序中的生命周期

> 小程序中的生命周期分为两类,分别是应用级别App以及页面级别Page

(1)应用级别app

```js
App({
  // 当第一次启动时，只会执行一次；就是启动了就执行；
  onLaunch: function() {
    console.log(1);
    wx.reques();
  },

  // 页面展示时触发
  onShow: function() {
    console.log(2);
  },
  // 页面隐藏时触发
  onHide: function() {
    console.log(3);
  },

  // 小程序抛出错误，捕获错误时触发
  onError: function() {
    console.log("error");
  },

  // 小程序启动时且同时，设置的页面找不到时，
  // 启动后，再次找不到页面，这个函数不执行；
  onPageNotFound: function() {
    console.log("没有找到页面");
  }
})
```

(2)页面级别page

```js
Page({
  // 路径页面加载完时
  onLoad: function() {
    console.log("page-页面加载了");
  },

  // 页面显示时
  onShow: function() {
    console.log("page-页面显示");
  },

  // 页面渲染完成时
  onReady: function() {
    console.log("page-页面渲染完成时");
  },
    
  // 页面隐藏时
  onHide: function() {
    console.log("page-页面被隐藏的时候");
  },
})
```

加载onLoad/页面展示onShow/渲染onReady/页面隐藏onHide





```html
<text>AAAAAA</text>
<navigator url="../live/live">点击我跳转到B页面</navigator>
<!-- 第一次打开A页面时,页面触发加载显示渲染的生命周期函数,当跳转到B页面时,首先触发A页面隐藏的生命周期函数,其次触发B页面加载显示渲染的函数,当点击返回按钮时,B页面被销毁,触发A页面的显示函数,如果点击链接再次跳转到B页面,触发A页面隐藏函数,再触发B页面加载显示渲染的函数,重新生成B页面-->
```

```
<navigator url="../live/live">点击我跳转到B页面</navigator>
```

小程序中的navigator相当于a链接,url地址相当于href属性,可以通过点击链接实现页面跳转,同时可以通过?的方式来进行传参

```
<navigator url="../live/live?id=1&name='chen'">点击我跳转到B页面</navigator>
```

那么在跳转后我们如何取到参数值呢?

* **小程序页面跳转传参并取值**

在跳转后页面Page的onLoad生命周期函数中通过query参数来进行取值,query参数中包含有传进来参数的值



* **场景值**