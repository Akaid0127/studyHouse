# react-router-dom@5

## 一、路由基本使用

### 1.1 相关理解

#### SPA的理解

- 单页Web应用
- 整个页面只有一个完整的页面
- 点击页面中的导航链接不会刷新页面，只会做页面的局部更新
- 数据需要通过ajax请求获取



#### 路由的理解

什么是路由：

- 一个路由（route）就是一组映射关系（key - value）
- key为路径，value可能是function或component



后端路由：

- value就是function，用来处理客户端提交的请求
- 注册路由：`router.get(path, function(req,res))`
- 工作过程：当node接收到一个请求的时候，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据



前端路由：

- 浏览器端路由，value就是component，用于展示页面内容
- 注册路由：`<Route path='/test' component={test}>`
- 工作过程：当浏览器的path变为`/test`时候，当前路由组件就会变成Test组件



#### react-router-dom

- react的一个插件库
- 专门用来实现一个SPA应用
- 基于react的项目基本都会用到此库
- react-router分为三种，我们学的是react-router-dom，为Web实现



### 1.2 路由基本使用

安装库（此时学习的是第5版本）

```shell
npm install react-router-dom@5
```



路由的基本使用

    1.明确好界面中的导航区、展示区
    2.导航区的a标签改为Link标签
    	<Link to="/xxxx">Demo</Link>
    3.展示区写Route标签进行路径的匹配
    	<Route path='/xxxx’ component={Demo}/>
    4. <App>的最外侧包襄了一个<BrowserRouter>或<HashRouter>



首先创建两个组件，然后在App.js文件中应用并使用,

接着在到index.js文件中注册App组件，最后用index.html文件渲染到页面上

`App.js`

```react
import React, { Component } from 'react'
import { Link, Route } from 'react-router-dom'
import About from './Components/About';
import Home from './Components/Home';
import './App.scss';

export default class App extends Component {
	render() {
		return (
			<div className='App'>
				<div className='app-content'>
					<div className='title'>
						<h1>React Router Demo</h1>
					</div>
					<div className='main-content'>
						<div className='left-list'>
							{/* 在react中靠路由链接实现切换组件 */}
							<Link className='list1' to="/about">About</Link>
							<Link className='list2' to="/home">Home</Link>
						</div>
						<div className='right-content'>
							{/* 注册路由 */}
							<Route path="/about" component={About} />
							<Route path="/home" component={Home} />
						</div>
					</div>
				</div>
			</div>
		)
	}
}
```



`index.js`

```react
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom'
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<React.StrictMode>
		{/* // <App>的最外侧包襄了一个<BrowserRouter>或<HashRouter> */}
		<BrowserRouter>
			<App />
		</BrowserRouter>
	</React.StrictMode>
);

reportWebVitals();
```



## 二、路由组件

### 2.1 路由组件与一般组件

- 写法不同
  - 一般组件：`<Demo>`
  - 路由组件：`<Route path="/about" component={About} />`
- 存放位置不同
  - 一般组件：`components`
  - 路由组件：`pages`
- 接收到的props不同
  - 一般组件：写组件标签时传递什么，就能收到什么
  - 路由组件：接收到三个固定的属性（`history`  `location`  `match`）



接收到的props详情：

1. **history**: 

2. 1. **go**: *ƒ go(n)*
   2. **goBack**: *ƒ goBack()*
   3. **goForward**: *ƒ goForward()*
   4. **push**: *ƒ push(path, state)*
   5. **replace**: *ƒ replace(path, state)*

3. **location**: 

4. 1. **pathname**: "/about"
   2. **search**: ""
   3. **state**: undefined

5. **match**: 

6. 1. **params**: {}
   2. **path**: "/about"
   3. **url**: "/about"



### 2.2 NavLink

`NavLink`标签比`link`标签多一层正在显示组件的css控制

多一个属性`activeClassName='blue-demo'`

```react
export default class App extends Component {
	render() {
		return (
			<div className='App'>
				<div className='app-content'>
					<div className='title'>
						<h1>
							<Header></Header>
						</h1>
					</div>
					<div className='main-content'>
						<div className='left-list'>
							{/* 在react中靠路由链接实现切换组件 */}
							<NavLink
								activeClassName='blue-demo'
								className='list1'
								to="/about">About</NavLink>
							<NavLink
								activeClassName='blue-demo'
								className='list2'
								to="/home">Home</NavLink>
						</div>
						<div className='right-content'>
							{/* 注册路由 */}
							<Route path="/about" component={About} />
							<Route path="/home" component={Home} />
						</div>
					</div>
				</div>
			</div>
		)
	}
}
```



### 2.3 封装NavLink组件

`NavLink`

- `NavLink`可以实现路由链接的高亮，通过`activeClassName`指定样式类名
- 标签体内容是一个特殊的标签属性
- 通过`this.props.childern`可以获取组件标签标签体内容



新建`MyNavLink`组件

```react
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom'

import './index.scss';

export default class MyNavlink extends Component {
	render() {
		return (
			<NavLink
				activeClassName='list-item-active'
				className='list-group-item'
				{...this.props} />
		)
	}
}
```



app中引入

```react
export default class App extends Component {
	render() {
		return (
			<div className='App'>
				<div className='app-content'>
					<div className='title'>
						<h1>
							<Header></Header>
						</h1>
					</div>
					<div className='main-content'>
						<div className='left-list'>
							{/* 在react中靠路由链接实现切换组件 */}
							<MyNavLink to="/about">About</MyNavLink>
							<MyNavLink to="/home">Home</MyNavLink>
						</div>
						<div className='right-content'>
							{/* 注册路由 */}
							<Route path="/about" component={About} />
							<Route path="/home" component={Home} />
						</div>
					</div>
				</div>
			</div>
		)
	}
}
```



### 2.4 Switch

通常情况下，path和component是一一对应的关系

Switch可以提高路由匹配效率（单一匹配）



Switch包裹的路由将不会继续向下匹配

下方/home将直接匹配Home，而不会继续向下匹配

```react
{/* 注册路由 */}
<Switch>
	<Route path="/about" component={About} />
	<Route path="/home" component={Home} />
    <Route path="/home" component={Test} />
</Switch>
```



### 2.5 解决样式丢失问题

解决方法：

- `public/index.html` 中引入样式时不写 `./` 写 `/ `（常用）
- `public/index.html` 中引入样式时不写 `./` 写 `%PUBLIC_URL%`
- 使用`HashRouter`



### 2.6 模糊匹配和严格匹配

- 默认使用的是模糊匹配（输入的路径必须包含匹配的路径，且顺序要一致）
- 开启严格匹配`<Route exact path="/about" component={About} />`
- 严格匹配不要随便开启，需要再开，有些时候开启会导致无法继续匹配二级路由



模糊匹配（home可以显示）

```react
<div className='main-content'>
	<div className='left-list'>
		{/* 在react中靠路由链接实现切换组件 */}
		<MyNavLink to="/about">About</MyNavLink>
		<MyNavLink to="/home/123/456">Home</MyNavLink>
	</div>
	<div className='right-content'>
		{/* 注册路由 */}
		<Route path="/about" component={About} />
		<Route path="/home" component={Home} />
	</div>
</div>
```



严格匹配（home无法显示）

```react
<div className='main-content'>
	<div className='left-list'>
		{/* 在react中靠路由链接实现切换组件 */}
		<MyNavLink to="/about">About</MyNavLink>
		<MyNavLink to="/home/123/456">Home</MyNavLink>
	</div>
	<div className='right-content'>
		{/* 注册路由 */}
		<Route exact path="/about" component={About} />
		<Route exact path="/home" component={Home} />
	</div>
</div>
```



### 2.7 Redirect重定向

一般写在所有路由注册的最下方

当所有路由都无法匹配的时候，跳转到Redirect指定的路由                                                                                                                                                                                                  

```react
<div className='main-content'>
	<div className='left-list'>
		{/* 在react中靠路由链接实现切换组件 */}
		<MyNavLink to="/about">About</MyNavLink>
		<MyNavLink to="/home">Home</MyNavLink>
	</div>
	<div className='right-content'>
		{/* 注册路由 */}
		<Route path="/about" component={About} />
		<Route path="/home" component={Home} />
		<Redirect to="/about" />
	</div>
</div>
```





## 三、嵌套路由

### 3.1 嵌套路由

注册子路由时候要写上父路由的path值

路由的匹配是按照注册路由的顺序进行的



### 3.2 传参params

向路由组件传递params参数

路由连接（携带参数）

```react
<Link to={`/home/message/detail/${item.id}`}>
	message{item.id}
</Link>
```

注册路由（声明接收）

```react
<Route path="/home/message/detail/:id" component={Detail}></Route>
```

接收参数

```react
const { id } = this.props.match.params
```



父组件代码

```react
import React, { Component } from 'react'
import { Link } from 'react-router-dom';
import { Route } from 'react-router-dom'

import Detail from './Detail';

export default class Message extends Component {
	state = {
		messageArr: [
			{ id: 1, title: "消息1" },
			{ id: 2, title: "消息2" },
			{ id: 3, title: "消息3" },
		]
	}
	render() {
		const { messageArr } = this.state
		return (
			<div className='Message'>
				<div className='message-content'>
					{
						messageArr.map((item) => {
							return (
								<li key={item.id}>
									<Link to={`/home/message/detail/${item.id}`}>
										message{item.id}
									</Link>
								</li>
							)
						})
					}
					{/* 注册路由 */}
					<Route path="/home/message/detail/:id" component={Detail}></Route>
				</div>
			</div>
		)
	}
}
```



子组件代码

```react
import React, { Component } from 'react'

// 后台拿到的数据
const detailData = [
	{ id: 1, content: "你好,中国" },
	{ id: 2, content: "132123" },
	{ id: 3, content: "你好,asd" },
]

export default class Detail extends Component {
	render() {
		const { id } = this.props.match.params
		const findResult = detailData.find((item) => {
			return item.id.toString() === id
		})
		return (
			<div className='Detail'>
				<div className='detail-content'>
					<ul>
						<li>{findResult.id}</li>
						<li>{findResult.content}</li>
					</ul>
				</div>
			</div>
		)
	}
}
```



### 3.3 传参search

路由链接（携带参数）

```react
<Link to={`/home/message/detail/?id=${item.id}&title=${item.title}`}>
	message{item.id}
</Link>
```

注册路由（无需声明，正常注册即可）

```react
{/* search参数无需声明接收 */}
<Route path="/home/message/detail" component={Detail}></Route>
```

接收参数

```react
// 接收search参数
const { search } = this.props.location
const { id, title } = qs.parse(search.slice(1))
```

获取到的search是urlencoded编码字符串，需要借助qs解析



父组件

```react
import React, { Component } from 'react'
import { Link } from 'react-router-dom';
import { Route } from 'react-router-dom'

import Detail from './Detail';

export default class Message extends Component {
	state = {
		messageArr: [
			{ id: 1, title: "消息1" },
			{ id: 2, title: "消息2" },
			{ id: 3, title: "消息3" },
		]
	}
	render() {
		const { messageArr } = this.state
		return (
			<div className='Message'>
				<div className='message-content'>
					{
						messageArr.map((item) => {
							return (
								<li key={item.id}>
									<Link to={`/home/message/detail/?id=${item.id}&title=${item.title}`}>
										message{item.id}
									</Link>
								</li>
							)
						})
					}
					{/* 注册路由 */}
					{/* search参数无需声明接收 */}
					<Route path="/home/message/detail" component={Detail}></Route>
				</div>
			</div>
		)
	}
}
```



子组件

```react
import React, { Component } from 'react'
import qs from 'qs';
// 新版本已被弃用
// import qs from 'querystring';

// 后台拿到的数据
const detailData = [
	{ id: 1, content: "你好,中国" },
	{ id: 2, content: "132123" },
	{ id: 3, content: "你好,asd" },
]

export default class Detail extends Component {
	render() {
		// 接收search参数
		const { search } = this.props.location
		const { id, title } = qs.parse(search.slice(1))

		const findResult = detailData.find((item) => {
			return item.id.toString() === id
		})
		return (
			<div className='Detail'>
				<div className='detail-content'>
					<ul>
						<li>{id}</li>
						<li>{title}</li>
						<li>{findResult.content}</li>
					</ul>
				</div>
			</div>
		)
	}
}
```



### 3.4 传参state

没有在url地址栏上体现

刷新也可以保留住参数

父组件

```react
<div className='message-content'>
	{
		messageArr.map((item) => {
			return (
				<li key={item.id}>
					<Link to={{
						pathname: '/home/message/detail',
						state: {
							id: item.id,
							title: item.title,
						}
					}}>
						message{item.id}
					</Link>
				</li>
			)
		})
	}
	{/* 注册路由 */}
	{/* search参数无需声明接收 */}
	<Route path="/home/message/detail" component={Detail}></Route>
</div>
```



子组件

```react
export default class Detail extends Component {
	render() {
		// 接收state参数
        // 防止undefined使用 || {}
		const { id, title } = this.props.location.state || {}

		const findResult = detailData.find((item) => {
			// 这里传递的对象，number类型的id，不用转换
			return item.id === id
		}) || {}
		return (
			<div className='Detail'>
				<div className='detail-content'>
					<ul>
						<li>{id}</li>
						<li>{title}</li>
						<li>{findResult.content}</li>
					</ul>
				</div>
			</div>
		)
	}
}
```





## 四、编程式路由

### 4.1 push与replace

push模式是**栈的常规模式**，可以回到上一级，会留下痕迹

replace模式是**替换模式**，会替换掉栈顶的路由，回不到上一级，不会留下痕迹（无痕模式），适用于登录后，不需要重新回到登录页

开启方法：

```react
<Link 
	replace={true} 
	to={{ pathname: '/home/message/detail', state: { id: msgObj.id, title: msgObj.title } }}>
	{msgObj.title}
</Link>
```



### 4.2 编程式路由

- 编程式路由导航：通过JS路由对象的方式来实现页面跳转（push、replace、go）
- 声明式路由导航：`Link`和`NavLink`实现路由的跳转



随着`react-router`，可以使用`Link`元素创建的原生处理反应路由器链接。

但是，我不想点击链接进行导航，想通过点击按钮自动实现页面跳转。实现方法如下

```react
// push跳转 + 携带params参数
this.props.history.push(`/home/message/detail/${id}/${title}`)

// push跳转 + 携带search参数
this.props.history.push(`/home/message/detail?id=${id}&title=${title}`)

// push跳转 + 携带state参数
this.props.history.push(`/home/message/detail`, { id: id, title: title })

// replace跳转 + 携带params参数
this.props.history.replace(`/home/message/detail/${id}/${title}`)

// replace跳转 + 携带search参数
this.props.history.replace(`/home/message/detail?id=${id}&title=${title}`)

// replace跳转 + 携带state参数
this.props.history.replace(`/home/message/detail`, { id: id, title: title })

// 前进
this.props.history.goForward()

// 回退
this.props.history.goBack()

// 前进或回退(go)
this.props.history.go(-2)  //回退到前2条的路由
```



Message->index.jsx：

```react
import React, { Component } from 'react'
import { Link, Route } from 'react-router-dom'
import Detail from './Detail';

export default class Message extends Component {
  state = {
    messageArr: [
      { id: '01', title: '消息1' },
      { id: '02', title: '消息2' },
      { id: '03', title: '消息3' }
    ]
  }

  replaceShow = (id, title) => {
    // 编写一段代码，让其实现跳转到Detail组件，且为replace跳转 +携带params参数
    // this.props.history.replace(`/home/message/detail/${id}/${title}`)

    // replace跳转 +携带search参数
    // this.props.history.replace(`/home/message/detail?id=${id}&title=${title}`)

    // replace跳转 +携带state参数
    this.props.history.replace(`/home/message/detail`, { id: id, title: title })
  }

  pushShow = (id, title) => {
    // 编写一段代码，让其实现跳转到Detail组件，且为push跳转 +携带params参数
    // this.props.history.push(`/home/message/detail/${id}/${title}`)

    // push跳转 +携带search参数
    // this.props.history.push(`/home/message/detail?id=${id}&title=${title}`)

    // push跳转 +携带state参数
    this.props.history.push(`/home/message/detail`, { id: id, title: title })
  }

  back = () => {
    this.props.history.goBack()
  }

  forward = () => {
    this.props.history.goForward()
  }

  go = () => {
    this.props.history.go(-2)
  }

  render() {
    const { messageArr } = this.state
    return (
      <div>
        <ul>
          {
            messageArr.map((msgObj) => {
              return (
                <li key={msgObj.id}>
                  {/* 向路由组件传递params参数 */}
                  {/* <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>
                  {msgObj.title}
                  </Link> */}

                  {/* 向路由组件传递search参数 */}
                  {/* <Link to={`/home/message/detail/?id=${msgObj.id}&title=${msgObj.title}`}>
                  {msgObj.title}
                  </Link> */}

                  {/* 向路由组件传递state参数 */}
                  <Link to={{ pathname: '/home/message/detail',
                              state: { id: msgObj.id, title: msgObj.title } }}>
                  		{msgObj.title}
                  </Link>

                  <button onClick={() => { this.pushShow(msgObj.id, msgObj.title) }}>
                  	push查看
                  </button>
                      
                  <button onClick={() => { this.replaceShow(msgObj.id, msgObj.title) }}>
                  	replace查看
                  </button>
                </li>
              )
            })
          }
        </ul>
        <hr />
        {/* 注册路由 */}
        {/* 声明接收params参数 */}
        {/* <Route path="/home/message/detail/:id/:title" component={Detail} /> */}

        {/* search参数无需声明接收，正常注册路由即可 */}
        {/* <Route path="/home/message/detail" component={Detail} /> */}

        {/* state参数无需声明接收，正常注册路由即可 */}
        <Route path="/home/message/detail" component={Detail} />
            
        <button onClick={this.back}>回退</button>&nbsp;
        <button onClick={this.forward}>前进</button>&nbsp;
        <button onClick={this.go}>go</button>
            
      </div>
    )
  }
}

```



Detail->index.jsx:

```react
import React, { Component } from 'react'
// 引入query-string库
// import qs from 'qs'

const DetailData = [
  { id: '01', content: '你好，中国' },
  { id: '02', content: '你好，程序员' },
  { id: '03', content: '你好，csdn' }
]
export default class Detail extends Component {
  render() {
    console.log(this.props)
    // 接收params参数
    // const { id, title } = this.props.match.params

    // 接收search参数
    // const { search } = this.props.location
    // const { id, title } = qs.parse(search.slice(1))

    // 接收state参数
    const { id, title } = this.props.location.state || {}

    const findResult = DetailData.find((detailObj) => {
      // 如果某一项对象的id和我传过来的Id相等，findResult就等于这一项对象
      return detailObj.id === id
    }) || {}
    
    return (
      <ul>
        <li>ID: {id}</li>
        <li>TITLE: {title}</li>
        <li>CONTENT: {findResult.content}</li>
      </ul>
    )
  }
}
```



借助this.props.history对象上的API对操作路由跳转、前进、后退：

- this.props.history.push()

- this.props.history.replace()

- this.props.history.goBack()

- this.props.history.goForward()

- this.props.history.go()
  

> 疑问：这个注册路由能不能另外写一个router文件？



### 4.3 withRouter的使用

由于路由组件的props中是有history属性的，而一般组件（非路由组件）是没有history属性

所以在一般组件中，是不能使用history属性身上的API的（push/replace/goBack等）

但是，`WithRouter`可以解决上述问题

```react
class Header extends Component {
  // withRouter(Header)后，就可以在一般组件内部使用 this.props.history 
}
export default withRouter(Header)
```

```react
import React, { Component } from 'react'
import { withRouter } from 'react-router-dom'

class Header extends Component {

  back = () => {
    this.props.history.goBack()
  }
  
  forward = () => {
    this.props.history.goForward()
  }

  go = () => {
    this.props.history.go(-2)
  }

  render() {
    console.log(this.props)
    return (
      <div className="page-header">
        <h2>React Router Demo</h2>
        <button onClick={this.back}>回退</button>&nbsp;
        <button onClick={this.forward}>前进</button>&nbsp;
        <button onClick={this.go}>go</button>
      </div>
    )
  }
}
export default withRouter(Header)
```

这样一般组件里也能使用路由组件所特有的API



### 4.4 BrowserRouter

BrowserRouter与HashRouter的区别

底层原理不一样：

- BrowserRouter使用的是H5的history API，不兼容IE9及以下版本
- HashRouter使用的是URL的哈希值



path表现形式不一样：

- BrowserRouter的路径中没有#，例如：localhost:3000/demo/test

- HashRouter的路径包含#，例如：localhost:3000/#/demo/test




刷新后对路由state参数的影响：

- BrowserRouter没有任何影响，因为state保存在history对象中

- HashRouter刷新后会导致路由state参数的丢失
