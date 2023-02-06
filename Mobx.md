



# Mobx



**这是我参与「第五届青训营 」伴学笔记创作活动的第 1 天**

我们组的项目是基于NextJS搭建仿掘金站点

我的任务是搭建仿掘金站点的CMS，状态集中管理技术选择简单易上手的Mobx

之前一直用的Vue，和Vue配套的状态集中管理工具是Vuex，Vuex拥有非常实用状态流程和模块化管理

这个寒假才刚刚接触react，学到redux的时候，发现其流程繁琐，并且不支持模块化

这才选择Mobx作为项目的状态集中管理工具



## 一、Mobx了解

### 1.1 Mobx介绍

官方文档：http://cn.mobx.js.org

- Mobx是一个功能强大，上手非常容易的状态管理工具
- Mobx背后的哲学很简单：任何源自应用状态的东西都应该自动地获得
- Mobx利用getter和setter来收集组件的数据依赖关系

![](https://cn.mobx.js.org/flow.png)



### 1.2 与redux的区别

区别：

- Mobx写法上偏向于OOP
- 对一份数据直接进行修改操作，不需要时钟返回一个新的数据
- 并非单一store，可以多个store
- redux默认一JavaScript原生对象形式存储数据，而Mobx使用可观察对象

优点：

- 学习成本小
- 面向对象编程，并且对TS友好

缺点：

- 过于自由：Mobx提供的约定以及模板代码很少，代码编写很自由，如果不做一些约定，比较容易导致是团队代码风格不一致
- 相关的中间件很少，逻辑层业务整合是问题





## 二、Mobx的基本使用

### 2.1 NextJS配置mobx

安装:

```shell
npm install mobx
```

```shell
npm install mobx-react
```



eslint安装

```shell
npm install eslint
```

在nextjs项目中要配置修饰符的话，直接在eslint中配置

```json
{
	"extends": "next/core-web-vitals",
	"ecmaFeatures": {
		"legacyDecorators": true // 主要是这个选项
	}
}
```



vscode编辑器打开setting

搜索`experimentalDecorators`

出来的选项`Implicit Project Config: Experimental Decorators`直接勾选



在jsconfig下添加`"experimentalDecorators": true`

```js
{
  "compilerOptions": {
	"experimentalDecorators": true, // 修饰符
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```



### 2.2 基本使用

在src文件夹下创建mobx文件夹

在mobx文件夹下创建store.js

```js
import { observable, configure, action } from 'mobx'
// 开启严格模式（外界不能修改数据）
configure({
	enforceActions: 'always'
})

class Store {
	@observable name = "123"
	@observable list = []
	@action.bound changeName() {
		console.log("456")
		this.name = "456"
	}
}

const store = new Store()

export default store
```



在index页面使用

注意：@observer修饰符下必须是类，不能是`export default class...`简写形式（这个简简单单问题困住了我一晚上）

```react
import React, { Component } from 'react'
import store from '../mobx/store'
import indexCss from '@/styles/Home.module.css'
import { observer } from 'mobx-react'
import { autorun } from 'mobx'

autorun(() => {
	console.log(store.name)
})

@observer
class Home extends Component {
	changeName = () => {
		setTimeout(() => {
			store.changeName()
		}, 2000)
	}

	render() {
		return (
			<div>
				<div className={indexCss.main}>
					{store.name}
				</div>
				<button onClick={this.changeName}>2000ms change isTabbarShow</button>

			</div>
		)
	}
}

export default Home
```



### 2.3 observable

Observable值可以是

- 基本数据类型
- 引用类型
- 普通对象
- 类实例
- 数组和映射



建议直接使用修饰符编写容器

```js
class Store {
    @observable name = "test"
	@observable age = 12
    @observable list = [1,2,3]
}
```



### 2.4 computed

computed计算属性

基于存储的观察状态衍生出的业务逻辑状态

相当于对源数据进行加工并传递，封装重复的逻辑

```js
class Store {
	@observable age = 12
	@computed get doubleAge() {
		return this.age + this.age 
	}
}
```



计算属性还会缓存第一次的执行结果

当数据未改变的时候调用的数据仍为第一次执行的结果

例如下面的代码片段只执行一次，高效且简便

```html
...
<p>{store.doubleAge}</p>
<p>{store.doubleAge}</p>
<p>{store.doubleAge}</p>
...
```



### 2.5 action

action方法

对原始数据的修改方法

可以通过配置mobx，可以让组件使用者强制通过action才能修改mobx中的值

```js
configure({
	enforceActions:'observed'
})
class store {
	...
}
```



### 2.6 action.bound

为了保证action的this指向的永远是容器的实例对象 

在添加action修饰器的时候，最好使用.bound

```js
@action.bound change(){
    console.log(this)
}
```



### 2.7 runInAction

适用于容器调用对数据的修改

```js
runInAction(()=>{
	store.count = 10
	store.foo = "hello"
})
```



### 2.8 异步action

异步操作之后，修改容器状态

当启动了严格模式之后，action就不允许在异步回调函数中对数据修改

```js
// error
@action.bound asyncChange(){
    setTimeout(()=>{
    	this.count = 100
    },100)
}
```



第一种方式：定义action函数

业务逻辑复杂情况下推荐使用

```js
@action.bound asyncChange(){
    setTimeout(()=>{
    	this.changeCount()
    },100)
}

@action.bound changeCount(){
    this.count = 20
}
```



第二种方式：直接调用action函数

```js
@action.bound asyncChange(){
    setTimeout(()=>{
    	action('changeFoo',()=>{
            this.foo = 'hello'
        })() 
    },100)
}
```



第三种方式：runInAction

业务逻辑简单的情况下推荐使用

```js
@action.bound asyncChange(){
    setTimeout(()=>{
    	runInAction(()=>{
            this.foo = 'hello'
        })
    },100)
}
```





## 三、Mobx数据监视

### 3.1 使用computed

当我们需要根据某个数据发生改变的时候，要得到一个新的业务数据，可以使用computed



### 3.2 autorun

autorun默认会执行一次

然后当内部所依赖的被观测的数据发生改变的时候，重新执行

```js
autorun(()=>{
	console.log(store.count)
})
```



### 3.3 when

when只有当第一个参数函数返回条件为真的时候，第二个参数函数才会执行

而且只执行一次，当符合某个条件才会去执行

如果初始化条件就满足，此时when只执行一次

要求：当count>100的时候，只执行一次自定义逻辑

```js
when(
    () => {
        return store.count > 100
    },
    () => {
        console.log("when run ", store.count)
    }
)
```



### 3.4 reaction

reaction不同于autorun和when

reaction只有当被观测的数据发生改变的时候才会执行

第一个参数函数执行一些业务逻辑操作，返回值交给第二个参数函数使用

而且执行次数是被观测的数据发生改变就会触发

```js
reaction(
    () => {
        // 执行一些业务逻辑操作，返回数据给下一个函数使用
        return store.count
    },
    (data, reaction) => {
        console.log("reaction run ", data)
        
        // 手动停止当前reaction的监听，只执行一次
        reaction.dispose()
    }
)
```























