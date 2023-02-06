# redux

## 一、理解

### 1.1 学习文档

- 英文文档：http://redux.js.org
- 中文文档：http://www.redux.org.cn
- Github：http://github.com/reactjs/redux



### 1.2 redux概念

- redux是一个专门用于做状态管理的JS库
- 它可以用在多个不同的前端框架等项目中，但是基本与react配合使用
- 作用：集中式管理react应用中多个组件共享的状态



### 1.3 使用redux时机

- 某个组件的状态，需要让其他组件可以随时拿到（共享）
- 一个组件需要改变另一个组件的状态（通信）
- 总体原则：能不用就不用，如果不用比较吃力才考虑使用



### 1.4 redux工作流程

![](https://img-blog.csdnimg.cn/4dc246049eac4c53b137608994ea44cc.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjQzNTIzNA==,size_16,color_FFFFFF,t_70)

Action：动作的对象，有两个属性

- type：标识属性，值为字符串，唯一，必选参数
- data：数据属性，值类型任意，可选参数



Reducer：用于初始化状态和加工状态

- 加工时根据旧的state值和传过来的action
- 生成新的state的值，是一个纯函数




Store：将state、action、reducer联系在一起的对象，相当于指挥者

- 创建store对象：createStore(reducer);
- 获取state的值：getState()
- 派发动作：dispatch(action)
- 注册监听：subscribe() 当产生新的 state 时，自动调用
  

Redux 的流程

- store 通过 reducer 创建了初始状态
- view 通过 store.getState() 获取到了 store 中保存的 state，挂载在了自己的状态上
- 用户产生了操作，调用了actions 的方法
- actions 的方法被调用，创建了带有标识性信息的action
- actions 将 action 通过调用 store.dispatch 方法发送到了reducer
- reducer 接收 到 action 并根据标识信息判断之后返回了新的 state
- store 的 state 被 reducer 更新为新的 state 的时候，store.subscribe 方法里的回调函数会执行，此时就可以通知 view 去重新获取 state



### 1.5 count案例-react

Count-->index.jsx

```react
import React, { Component } from 'react'

export default class Count extends Component {
	state = {
		count: 0
	}

	inc = () => {
		const { value } = this.selectNumber
		const { count } = this.state
		this.setState({
			count: count + parseInt(value)
		})
	}

	dec = () => {
		const { value } = this.selectNumber
		const { count } = this.state
		this.setState({
			count: count - parseInt(value)
		})
	}

	incOdd = () => {
		const { value } = this.selectNumber
		const { count } = this.state
		if (parseInt(value) % 2 !== 0) {
			this.setState({
				count: count + parseInt(value)
			})
		}
	}

	incAsync = () => {
		const { value } = this.selectNumber
		const { count } = this.state
		setTimeout(()=>{
			this.setState({
				count: count + parseInt(value)
			})
		},500)
	}

	render() {
		const { count } = this.state
		return (
			<div className='Count'>
				<div className='count-content'>
					<div>
						<h1>当前求和为：{count}</h1>
						<select ref={c => this.selectNumber = c}>
							<option value="1">1</option>
							<option value="2">2</option>
							<option value="3">3</option>
						</select>&nbsp;&nbsp;

						<button onClick={this.inc}>+</button>&nbsp;&nbsp;
						<button onClick={this.dec}>-</button>&nbsp;&nbsp;
						<button onClick={this.incOdd}>当前求和为奇数再加</button>&nbsp;&nbsp;
						<button onClick={this.incAsync}>异步加</button>&nbsp;&nbsp;

					</div>
				</div>
			</div>
		)
	}
}
```



### 1.6 count案例-精简

流程：

- 去除Count组件自身的状态
  - 在src下建立：
  - redux
  - store.js
  - count-reducer.js
- store.js
  - 引入redux中的createStore函数，创建一个store
  - createStore调用时要传入一个为其服务的reducer
  - 记得暴露store对象
- count-reducer.js
  - reducer的本质是一个函数，接收：`preState,action`，返回加工后的状态
  - reducer有两个作用：初始化状态，加工状态
  - reducer被第一次调用时候，是store自动触发的
    - 传递的preState是undefined
    - 传递的action是一个对象`{type:@@redux随机}`
- 在index.js中检测store中状态的改变，一旦发生改变重新渲染
  - 备注：reducer只负责管理状态，至于状态的改变驱动着页面的展示，要靠我们自己完成



安装redux

```
npm install redux
```



在src文件夹下新建store文件夹

`store.js`

```js
import { createStore } from 'redux';
import countReducer from './count_reducer';

export default createStore(countReducer);
```

`count-reducer.js`

```js
const initState = 0 // 初始化状态

export default function countReducer(preState = initState, action) {
	const { type, data } = action
	switch (type) {
		case 'inc':
			return preState + data
		case 'dec':
			return preState - data
		default:
			return preState
	}
}
```



`Count-->index.jsx`

```react
import React, { Component } from 'react'
import store from '../../redux/store';

export default class Count extends Component {
	state = {
		count: 0
	}

	// componentDidMount() {
	// 	// 检测redux中状态的变化，只要变化，就调用render
	// 	store.subscribe(() => {
	// 		this.setState({})
	// 	})
	// }

	inc = () => {
		const { value } = this.selectNumber
		// redux只是维护状态，并不是可以render更新页面状态
		store.dispatch({
			type: "inc",
			data: parseInt(value)
		})
	}

	dec = () => {
		const { value } = this.selectNumber
		store.dispatch({
			type: "dec",
			data: parseInt(value)
		})
	}

	incOdd = () => {
		const { value } = this.selectNumber
		if (parseInt(value) % 2 !== 0) {
			store.dispatch({
				type: "inc",
				data: parseInt(value)
			})
		}
	}

	incAsync = () => {
		const { value } = this.selectNumber
		setTimeout(() => {
			store.dispatch({
				type: "inc",
				data: parseInt(value)
			})
		}, 500)
	}

	render() {
		return (
			<div className='Count'>
				<div className='count-content'>
					<div>
						<h1>当前求和为：{store.getState()}</h1>
						<select ref={c => this.selectNumber = c}>
							<option value="1">1</option>
							<option value="2">2</option>
							<option value="3">3</option>
						</select>&nbsp;&nbsp;

						<button onClick={this.inc}>+</button>&nbsp;&nbsp;
						<button onClick={this.dec}>-</button>&nbsp;&nbsp;
						<button onClick={this.incOdd}>当前求和为奇数再加</button>&nbsp;&nbsp;
						<button onClick={this.incAsync}>异步加</button>&nbsp;&nbsp;
					</div>
				</div>
			</div>
		)
	}
}
```



index.js也需要修改

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import store from './redux/store';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <App />
);
store.subscribe(()=>{
	root.render(
		<App />
	);
})
```



### 1.7 count案例-完整

就是加了个action流程

count_action.js

```react
import { INC, DEC } from './constant';

export const createIncAction = data => ({
	type: INC,
	data: data
})

export const createDecAction = data => ({
	type: DEC,
	data: data
})
```



constant.js

```js
// 定义aciton对象中type类型的常量值
// 目的：便于管理的同时，防止程序员单词写错
export const INC = 'inc'
export const DEC = 'dec'
```



组件中使用

```react
// 引入actionCreator，专门用于创建action对象
import { createIncAction, createDecAction } from '../../redux/count_action'
export default class Count extends Component {
	...
    inc = () => {
        const { value } = this.selectNumber
        store.dispatch(createIncAction(parseInt(value)))
    }

    dec = () => {
        const { value } = this.selectNumber
        store.dispatch(createDecAction(parseInt(value)))
    }
    ...   
}
```



### 1.8 count案例-异步

求和案例-异步action版

- 明确：延迟的动作不想交给组件自身，想交给action
- 何时需要异步action：想对状态进行操作，但是具体的数据靠异步任务返回
- 备注：异步action不是必须要写的，完全可以自己等待异步任务的结果了再去分发同步action



需要安装中间件thunk

```shell
npm install redux-thunk
```

store.js中引入并使用

```react
import { createStore, applyMiddleware } from 'redux';
import countReducer from './count_reducer';
import thunk from 'redux-thunk'

export default createStore(countReducer, applyMiddleware(thunk));
```

异步操作

```react
import { INC, DEC } from './constant';

// 加
export const createIncAction = data => ({
	type: INC,
	data: data
})

// 减
export const createDecAction = data => ({
	type: DEC,
	data: data
})

// 异步加，异步action中一般都会调用同步action
export const createIncAsyncAction = data => {
	return (dispatch) => {
		setTimeout(() => {
			// dispatch({
			// 	type: INC,
			// 	data: data
			// })
			dispatch(createIncAction(data))
		}, 500);
	}
}
```



### 1.9 react-redux

用到再学



### 1.10  





## 二、三个核心概念













## 三、核心API





## 四、编写应用





## 五、redux异步编程





## 六、redux调试工具





## 七、纯函数和高阶函数















































































