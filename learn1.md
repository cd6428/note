#### 1.git命令

> git commit --amend     修改提交的commit信息

修改完毕后,按shift+:      紧接着后面按wq     回车从而退出编辑状态 







#### 2.vue生命周期钩子destroyed中可以做的事情

> 销毁组件中所定义的定时器     +     关闭socket.io的连接







#### 3.总结一下vue异步更新dom的原理

> vue是根据数据来驱动视图更新,但是该过程是异步的







#### 4.Object.keys()和Object.values()

> Object.keys()接收一个对象参数,把对象中所有的key取出来组成一个数组进行返回

> Object.values()接收一个对象参数,把对象中所有的values取出来组成一个数组进行返回







#### 5.如何在父组件中去修改子组件中的数据呢?

> `this.$refs.refMoreAction.isReport = false`

通过ref获取到子组件这个dom元素,我们可以console.log这个dom元素,会发现上面有子组件中的数据,我们直接通过这个dom元素拿到子组件中的数据,然后进行更改





#### 6.两个数组之间的减法

```js
const arr = this.allChannels.filter(channel => {
        const idx = this.channels.findIndex(item => item.id === channel.id)
        if (idx === -1) {
          return true
        } else {
          return false
        }
 })
```

可选频道数组 = 全部频道数组 - 已有频道数组

仔细看一下两个数组之间的减法是如何实现的







#### 7.class类的几种绑定方式

> `:class="{cur:idx===curIndex}"`
>
> ``:class="布尔值 ？ 类名1 ：类名2"`
>
> `:class="{类名1：布尔值1， 类名2：布尔值2 .......}`

绑定一个class类,类名为cur,但是只有在后面的判定条件为true的时候,这个class类才会被添加上去





#### 8.数组操作: 类似于[id: xxx],通过数组方式改变为[id: xxx, seq: 1]形式

```js
const channels = [...this.channels, curChannel].map((item, idx) => {
          return {
            id: item.id,
            seq: idx
          }
 }).filter(item => item.id !== 0)
```

通过展开运算符生成一个新数组,同时利用数组的map方法生成新的数组形式,并过滤去除数组的第一项







#### 9.在子组件中修改父组件传递的prop

>如果从父组件中传入的props是引用数据类型(数组，对象),则在子组件中可以通过数组提供的方法(如果是数组)如push或者对象的方法(如果是对象)来间接修改props的数据,但是注意不能直接修改值,改动之后在父组件中所传递给props的值也会相应的发生改变





#### 10.如果高亮搜索关键字?

```js
computed: {
    // 根据keyword来把suggestion中的内容高亮
    cHightLight () {
      // g: 全局匹配
      // i: 忽略大小写（大写，小写都可以匹配）
      const reg = new RegExp(this.keyword, 'gi')
      return this.suggestion.map(item => {
        return item.replace(reg, function (val) {
          return `<span style="color:red">${val}</span>`
        })
      })
    }
  },
      
      
 <div v-html="item"></div>
```

搜索关键词高亮其实就是关键词替换,首先我们通过正则来进行关键词匹配,之后进行全局忽略大小写的替换即可,注意在数据渲染的时候我们不能使用插值表达式,因为插值表达式是默认使用v-text来进行数据渲染,无法解析其中的html标签,所以我们需要使用v-html指令





#### 11.对于input框input事件的防抖节流处理

debounce防抖

```js
async f () {
      // 没有关键字
      if (!this.keyword) {
        this.suggestion = []
        return
      }
      const res = await getSuggetion(this.keyword)
      console.log(res)
      this.suggestion = res.data.data.options
    },
    
// 只要用户在录入内容就会触发inpput，从而执行这个函数
    hInput_debounce () {
      // 对f进行0.4秒防抖处理。
      // 目标：如果0.4秒内没有再次调用它，则顺利执行这个函数，否则，再等0.4s。
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        this.f()
      }, 0.4 * 1000)
    },
        
        
        
        
        
//另一种实现
 function debounce(func, delay) {
    let timer
    return function() {
        clearTimeout(timer)
        timeout = setTimeout(function(){
          func()
        },delay)
    }
}
```

throttle节流

```js
hInput_throttle () {
      console.log('hInput_throttle.....')
      // 对f进行0.4秒节流处理。
      // 目标：如果0.4秒内没有再次调用它，则顺利执行这个函数，否则，再等0.4s。
      if (Date.now() - this.lastCallTimestamp >= 0.4 * 1000) {
        this.f()
        this.lastCallTimestamp = Date.now()
      } else {
        console.log('没有间隔0.4s,不能调用f()')
      }
    },
        
        
        
 //另一种实现
 function throttle(fn, threshhold) {
    let start = new Date
    return function () {
      let curr = new Date() - 0
      if (curr - start >= threshhold) {
        fn() 
        start = curr
      }
    }
}
```

页面常见高频操作

> - 鼠标移动。
> - 窗口缩放。
> - input文本输入
> - scroll