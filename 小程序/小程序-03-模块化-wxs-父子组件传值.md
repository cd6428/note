#### 1.小程序的模块化

> * **使用module.exports或者exports对外暴露接口.通过require来进行导入,类似于node中的导入导出语法**
> * **通用的方法可以写在一个js文件中,供所有需要的页面来进行使用**

```js
function fn (x) {
  return 'nihao' + x
}


function fn1 (x) {
  return 'hello' + x
}


module.exports = {
  fn,
  fn1
}
//模块化的导入导出操作
```

单独定义了一个module.js文件,并导出两个方法

```js
const obj = require('../../utils/module')

Page({

  /**
   * 页面的初始数据
   */
  data: {
    info: 'chendong',
    msg: 'BeiJin'
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    console.log(obj.fn(this.data.info));
    // 小程序中如何在js文件中取到初始化data中的值
    this.setData({msg: app.change(this.data.msg)})
  }
})
```

在需要使用的页面的js文件中进行导入,然后使用即可





#### 2.npm模块

* **小程序目前不支持直接引入 node_modules** 
* **首先下载包之后需要构建npm,其次需要使用npm模块**



#### 3.getApp()

> 我们可以在app.js这个文件中去定义全局的变量还有方法,在任何页面中都是可以使用的,也就是说所有的页面都是可以共享定义在app.js文件中的数据和方法,但是我们需要在页面的js文件中通过`getApp()`这个方法来进行取值,之后才能进行使用

```js
App({
  change (info) {
    return `****${info}****`
  }
})


const app = getApp()

Page({

  /**
   * 页面的初始数据
   */
  data: {
    info: 'chendong',
    msg: 'BeiJin'
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    console.log(obj.fn(this.data.info));
    // 小程序中如何在js文件中取到初始化data中的值
    this.setData({msg: app.change(this.data.msg)})
  }
})
```







#### 4.wxs的使用

`类似于vue中过滤器的用法`

**页面中的数据是原始数据经过处理后的,而且在这个处理的过程中不能更改原始数据的值,我们可以使用`wxs`来实现**

wxs支持模块化,其实很简单.我们就是在wxs中定义一些函数的处理逻辑,首先定义一个形参,这个形参未来会接收js中所定义的数据,我们通过处理逻辑对数据进行处理,处理成为我们想要的数据类型,然后放入到页面中去进行使用,其实wxs就是一个数据处理的过程,我们可以单独定义一个页面的wxs,也可以定义全局的wxs





#### 5.小程序中的父子组件及其传值操作

* 父传子

  ```js
  <comSon sonAcceptData='{{info}}' bind:send='acceptData'></comSon>
  
  properties: {
      sonAcceptData: {
        type: String
      }
    },
  ```

  和vue中的父传子对比,自定义属性前面不需要加上`:`了

* 子传父

  ```js
  <button type="primary" bind:tap="clickMe">clickMe</button>
  
  methods: {
      clickMe () {
        this.triggerEvent('send', this.data.message)
      }
    }
    
  <comSon sonAcceptData='{{info}}' bind:send='acceptData'></comSon>
  
  methods: {
      acceptData (res) {
        this.setData({someInfo: res.detail})
      }
    }
  ```

  

和vue中的父传子对比,`$emit`更改为了`triggerEvent`,不需要使用@来进行监听事件了,用bind就可以了,父组件方法中接收数据的方式也发生了改变,通过res.detail来接收传递过来的数据,和vue中相比,总体差不多,细节方面还是有一些区别的







#### 6.vant组件库小程序





#### 7.F2





#### 8.日历





