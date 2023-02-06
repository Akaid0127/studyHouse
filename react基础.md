# React入门

学习目标：

- React基础
- React-Router路由
- PubSub消息管理
- Redux状态集中管理
- Ant-Design组件库



## 一、React简介

### 1.1 React定义

用于构建用户界面的JavaScript库

- 发送请求获取数据
- 处理数据（过滤、整理表格等）
- 操作DOM呈现页面

React是一个将数据渲染为HTML视图的开源JavaScript库



### 1.2 React开发者

Facebook



### 1.3 学习意义

- 原生JavaScript操作DOM繁琐、效率低（DOM-API操作UI）
- 使用JavaScript直接caozuoDOM，浏览器会进行大量的重绘重排
- 原生JavaScript没有组件化编码方案，代码复用率低



### 1.4 React特点

- 采用组件化模式、声明式编码，提高开发效率及组件复用率
- 在React Native中可以使用React语法进行移动端开发
- 使用虚拟DOM+优秀的Diffing算法，尽量减少与真实DOM的交互



## 二、React的基本使用

### 2.1 使用相关js库

- react.js 核心库
- react-dom.js 提供操作DOM的react扩展库
- babel.min.js 解析JSX语法代码转换为JS代码的库



### 2.2  第一个React

```react
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>Hello World</title>
	<!-- 引入顺序需按照下列顺序 -->
	<script src="./js/react.development.js"></script>
	<script src="./js/react-dom.development.js"></script>
	<script src="./js/babel.min.js"></script>
</head>

<body>
	<div id="root"></div>
	<script type="text/babel">

		// 创建虚拟DOM
		function MyApp() {
			return <h1>Hello, world!</h1>;
		}

		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(<MyApp />);

	</script>
</body>

</html>
```



### 2.3 虚拟DOM

使用`jsx`创建虚拟DOM

```react
<body>
    <!-- 创建一个容器 -->
	<div id="root"></div>
	<script type="text/babel">

		// 创建虚拟DOM
		function MyApp() {
			return <h1 id="title">Hello, world!</h1>;
		}

		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(<MyApp />);

	</script>
</body>
```



使用`js`创建虚拟DOM

```html
<body>
	<div id="root"></div>
	<script type="text/javascript">

		// 创建虚拟DOM
		const MyApp = React.createElement('h1', { id: 'title' }, React.createElement('span', {}, 123));


		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(MyApp);

	</script>
</body>
```



使用`JS`和`JSX`都可以创建虚拟DOM，但是可以看出`JS`创建虚拟DOM比较繁琐

尤其是标签如果很多的情况下，所以还是比较推荐使用`JSX`来创建



关于虚拟DOM

本质是Object类型的对象（一般对象）

虚拟DOM比较轻，真实DOM比较重，因为虚拟DOM是React内部在用，无需真实DOM上那么多属性

虚拟DOM最终会被React转换为真实DOM ，呈现在页面上



### 2.4 JSX

- 全称：JavaScript XML
- react定义一种类似XML的JS扩展语法
- 本质是`React.createElement(component,props,...children)`方法的语法糖
- 作用：用来简化创建虚拟DOM
  - 写法：`var ele = <h1>hello!</h1>`
  - 注意点1：它不是自妇产，也不是HTML/XML标签
  - 注意点2：它最终产生的就是一个JS对象
- 标签名任意：HTML标签或者其他标签



XML早期用于存储和传输数据

目前使用JSON

```js
// 实现从JSON字符串转换为JS对象
var str = '{"name": "兮动人","age":22}';
var obj = JSON.parse(str);
console.log(obj);

// 实现从JS对象转换为JSON字符串
var str = '{"name": "兮动人","age":22}';
var obj = JSON.parse(str);
console.log(obj);
var jsonstr = JSON.stringify(obj);
console.log(jsonstr);
```



语法规则：

- 定义虚拟DOM，不能使用`''`
- 标签中混入JS表达式的时候使用`{}`
- 样式的类名指定不要使用`class`，使用`className`
- 内敛样式要使用双大括号包裹
- 不能有多个根标签，只能有一个根标签
- 标签必须闭合
- 标签首字母
  - 若小写字母开头，则将改标签转为html中同名元素，若html中无该标签对应同名元素，则报错
  - 若大写字母开拓，react就去渲染对应的组件，若组件没有定义，则报错


```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 数据
		const myID1 = '123'
		const myID2 = '666'
		const myData = "string123"

		// 创建虚拟DOM
		const VDOM = (
			<div>
				<h2 id={myID1} className="title">
					<span style={{ color: 'white', fontSize: '38px' }}>{myData}</span>
				</h2>
				<h2 id={myID2} className="title">
					<span style={{ color: 'white', fontSize: '38px' }}>{myData}</span>
				</h2>
				<input type="text" />
				<good>123</good>
			</div>
		);

		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(VDOM);

	</script>
</body>
```



### 2.5 JSX小练习

一定注意区分：`js语句（代码）`与`js表达式`

- 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方（一个函数也是一个表达式）
- 语句：条件语句、循环语句、选择语句

code中的`key`设置为`index`是有问题的，后期再说

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 数据
		const data = ['Angular', 'Vue', 'react']
		// 创建虚拟DOM
		const VDOM = (
			<div>
				<h1>前端js框架</h1>
				<ul>
					{
						data.map((item, index) => {
							return <li key="index">{item}</li>
						})
					}
				</ul>
			</div>
		);
		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(VDOM);

	</script>
</body>
```



### 2.6 组件与模块

**模块**

- 理解：向外提供特定功能的`js程序`，一般就是一个`js文件`
- 为什么要拆分成模块：随着业务逻辑增加，代码越来越多且复杂
- 作用：复用`js`，简化`js`的编写，提高`js`运行效率



**组件**

- 理解：用来实现局部功能效果的代码和资源的集合（html、css、js等等）
- 为什么：一个界面的功能复杂
- 作用：复用代码，简化项目编码，提高运行效率



**模块化**

- 当应用的`js`都以模块来编写，这个应用就是一个模块化的应用



**组件化**

- 当应用是以多组件的方式实现，这个应用就是一个组件化的应用



### 2.7 React使用CSS

https://blog.csdn.net/kongcheng_001/article/details/100017716

#### 正常CSS写法

```css
.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
```



#### 组件直接使用style

不需要组件从外部引入css文件，直接在组件中书写

注意事项：

- 驼峰法命名属性
- 属性值双引号包裹
- 只适用于当前组件

```react
import React, { Component } from "react";

const div1 = {
  width: "300px",
  margin: "30px auto",
  backgroundColor: "#44014C",  //驼峰法
  minHeight: "200px",
  boxSizing: "border-box"
};

class Test extends Component {
  constructor(props, context) {
    super(props);
  }
  render() {
    return (
     <div>
       <div style={div1}>123</div>
       <div style="background-color:red;">
     </div>
    );
  }
}
            
export default Test;
```



#### 引入[name].css

需要在当前组件开头使用import引入css文件

标签属性为`className`

这种方式引入的css样式，会作用于当前组件及其所有后代组件

```react
import React, { Component } from "react";
import TestChidren from "./TestChidren";
import "@/assets/css/index.css";
class Test extends Component {
  constructor(props, context) {
    super(props);
  }
  render() {
    return (
      <div>
        <div className="link-name">123</div>
        <TestChidren>测试子组件的样式</TestChidren>
      </div>
    );
  }
}
export default Test;
```



#### [name].module.css

将css文件作为一个模块引入，这个模块中的所有css，只作用于当前组件。不会影响当前组件的后代组件

这种方式可以看做是前面第一种在组件中使用style的升级版。完全将css和组件分离开，又不会影响其他组件

```react
import React, { Component } from "react";
import TestChild from "./TestChild";
import moduleCss from "./test.module.css";

class Test extends Component {
  constructor(props, context) {
    super(props);
  }  
  render() {
    return (
     <div>
       <div className={moduleCss.linkName}>321321</div>
       <TestChild></TestChild>
     </div>
    );
  }
}

export default Test;
```





## 三、React面向组件编程

### 3.1 基本理解与使用

已学完



### 3.2 React开发者工具

React Developer Tools

去google应用商店下载



### 3.3 组件分类

#### 函数式组件

适用于简单组件的定义

- 执行了`render...`之后，发生了什么
  1. react解析组件标签，找到了`MyComponent`组件
  2. 发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM，随后呈现在页面中

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 创建虚拟DOM
		function MyComponent() {
			// 原因：babel翻译完后开启了严格模式，this不再指向window
			console.log(this) // undefine
			return <h1>Hello, world!</h1>;
		}

		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(<MyComponent />);
	</script>
</body>
```



#### 类式组件

适用于复杂组件的定义

复习类：

```html
<body>
	<script type="text/javascript">
		// 创建一个Person类
		class Person {
			// 构造器方法
			constructor(name, age) {
				// this指的是类的实例对象
				this.name = name
				this.age = age
			}
			// 一般方法 位于类的原型对象上，供实例使用
			// 通过Peron实例调用speak时，speak中的this就是person实例
			speak() {
				console.log(this.name, this.age)
			}
		}
		// 创建一个Person的实例对象
		const p1 = new Person('tom', 18)
		const p2 = new Person('jerry', 19)
		console.log(p1)
		p1.speak()
		console.log(p2)
		p2.speak()
	</script>
</body>
```



#### 复习继承

```html
<body>
	<script type="text/javascript">
		// 创建一个Person类
		class Person {
			// 构造器方法
			constructor(name, age) {
				// this指的是类的实例对象
				this.name = name
				this.age = age
			}
			// 一般方法 位于类的原型对象上，供实例使用
			// 通过Peron实例调用speak时，speak中的this就是person实例
			speak() {
				console.log(this.name, this.age)
			}
		}
		// 创建一个Student类，继承Person类
		class Student extends Person {
			constructor(name, age, grade) {
				super(name, age)
				this.grade = grade
			}
			// 重写从父类继承过来的方法
			speak() {
				console.log(this.name, this.age, this.grade)
			}
		}
		const s1 = new Student("Andy", 23, "大学生")
		console.log(s1)
		s1.speak()
	</script>
</body>
```



#### 总结

- 类中的构造器不是必须写的，要对实例进行一些初始化操作，如添加指定属性时才写
- 如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的
- 类种所定义的方法，都是放在了类的原型对象上，供实例去使用

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 创建类式组件
		// React.Component为内置组件
		class MyComponent extends React.Component {
			// render放在哪里的：MyComponent的原型对象上，供实例使用
			// render中的this：MyComponent的实例对象，MyComponent组件实例对象
			render() {
				return (
					<h1>Hello, world!</h1>
				)
			}
		}

		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(<MyComponent />);

		// 上行代码执行之后
		/* 
			1、React解析组件标签，找到了MyComponent组件
			2、发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法
			3、将render返回的虚拟DOM转化为真实DOm，随后呈现到页面中
		*/
	</script>
</body>
```



### 3.4 state

> 组件实例的三大核心属性：state

理解：

- state是组件对象最重要的属性，值是对象（可以包含多个`key-value`的组合）
- 组件被称为`状态机`，通过更新组件的state来更新对应的页面显示（重新渲染组件）


注意：

- 组件中render方法中的this为组件实例对象
- 组件自定义的方法中`this`为`undefined`，如何解决
  - 强制绑定this；通过函数对象的bind()
  - 箭头函数
- 状态函数，不能直接修改数据或更新



```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 构造器调用几次？——1次
		// 创建组件
		class Weather extends React.Component {
			constructor(props) {
				super(props)
				// 数据
				this.state = {
					isHot: true,
					wind: "大风"
				}
				// 解决this指向问题，为事件处理函数绑定实例
				this.changeWeather = this.changeWeather.bind(this)
			}
			// render调用几次？——1+n次
			render() {
				const { isHot, wind } = this.state
				return (
					<h1 onClick={this.changeWeather}>今天天气很{isHot ? "炎热" : "凉爽"}，而且{wind}</h1>
				)
			}
			// 方法
			// changeWeather调用几次？——n次
			changeWeather() {
				console.log(this.state.isHot)
				// 状态不可直接更更改,要借助一个内置的API去更改
				// 装填必须通过setState进行更新，且更新是一种合并，不是替换
				const isHot = this.state.isHot
				this.setState({
					isHot: !isHot,
				})
			}
		}
		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(<Weather />);

	</script>
</body>
```



精简组件写法：

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Weather extends React.Component {
			// 初始化状态
			state = {
				isHot: true,
				wind: "大风"
			}
			// 渲染虚拟DOM
			render() {
				const { isHot, wind } = this.state
				return (
					<h1 onClick={this.changeWeather}>今天天气很{isHot ? "炎热" : "凉爽"}，而且{wind}</h1>
				)
			}
			// 自定义方法：一定要使用赋值语句加箭头函数
			changeWeather = () => {
				const isHot = this.state.isHot
				this.setState({
					isHot: !isHot,
				})
			}
		}
		// 渲染虚拟DOM到页面
		const container = document.getElementById('root');
		const root = ReactDOM.createRoot(container);
		root.render(<Weather />);
	</script>
</body>
```



### 3.5 props

理解：

- 每一个组件对象都会有props属性
- 组件标签的所有属性都保存在props中



#### props简单使用

```react
<body>
	<div id="root1"></div>
	<div id="root2"></div>
	<div id="root3"></div>
	<script type="text/babel">
		class Persons extends React.Component {
			render() {
				const { name, sex, age } = this.props
				return (
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age}</li>
					</ul>
				)
			}
		}
		// 渲染虚拟DOM到页面
		const root1 = ReactDOM.createRoot(document.getElementById('root1'));
		root1.render(<Persons name="jerry" age="19" sex="男" />);
		const root2 = ReactDOM.createRoot(document.getElementById('root2'));
		root2.render(<Persons name="harry" age="25" sex="男" />);
		const root3 = ReactDOM.createRoot(document.getElementById('root3'));
		root3.render(<Persons name="andy" age="19" sex="女" />);
	</script>
</body>
```



#### 展开运算符

```html
<body>
	<script type="text/javascript">
		// 展开数组
		let arr1 = [1, 3, 5, 7, 9]
		let arr2 = [2, 4, 6, 8, 10]
		console.log(...arr1, ...arr2)

		// 拼接数组
		let arr3 = [...arr1, ...arr2]
		console.log(arr3)

		// 函数中使用
		function sum(...numbers) {
			// 连续操作reduce
			return numbers.reduce((preValue, currentValue) => {
				return preValue + currentValue
			})
		}
		console.log(sum(1, 2, 2, 3, 5))

		// 构造字面量对象时使用展开语法
		// 展开运算符不能展开对象
		let person = { name: "tom", age: 18 }
		let person2 = { ...person } // 深度复制一个对象
		console.log(person2)

		// 对象属性合并
		let person3 = { ...person, name: "jack", address: "nanjing" }
		console.log(person3)
	</script>
</body>
```



#### 批量传递标签属性

```react
// 原数据
const p = { name: '老六', age: 18, sex: "女" }
const root3 = ReactDOM.createRoot(document.getElementById('root3'));
// react中展开运算符仅仅适用于标签属性展开
root3.render(<Persons {...p}/>);
```



#### 标签属性限制

```react
<body>
	<div id="root1"></div>
	<div id="root2"></div>
	<div id="root3"></div>
	<script type="text/babel">
		class Persons extends React.Component {
			render() {
				const { name, sex, age } = this.props
				return (
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age + 1}</li>
					</ul>
				)
			}
		}
		// 对标签属性进行类型、必要性的限制
		Persons.propTypes = {
			name: PropTypes.string.isRequired, // 限制name必传，且为字符串
			sex: PropTypes.string, // 限制sex必传为字符串
			age: PropTypes.number, // 限制age为数值
			speak: PropTypes.func, // 限制speak为函数
		}

		// 指定默认标签属性值
		Persons.defaultProps = {
			sex: "不男不女",
			age: 18
		}

		// 渲染组件到页面
		const root1 = ReactDOM.createRoot(document.getElementById('root1'));
		root1.render(<Persons name="jerry" age={19} sex="男" />);
		const root2 = ReactDOM.createRoot(document.getElementById('root2'));
		root2.render(<Persons name="harry" age={25} sex="男" />);

		const p = { name: '老六', age: 18, sex: "女" }
		const root3 = ReactDOM.createRoot(document.getElementById('root3'));
		root3.render(<Persons {...p} />);
	</script>
</body>
```



#### 配置简写属性

```react
<body>
	<div id="root1"></div>
	<div id="root2"></div>
	<div id="root3"></div>
	<script type="text/babel">
		// 创建组件
		// 被static修饰的属性和方法都是静态方法和属性, 只能被类名调用, 不能被实例化对象调用,同时也不能被子类继承
		class Persons extends React.Component {
			render() {
				const { name, sex, age } = this.props
				return (
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age + 1}</li>
					</ul>
				)
			}
			
			// 对标签属性进行类型、必要性的限制
			static propTypes = {
				name: PropTypes.string.isRequired, // 限制name必传，且为字符串
				sex: PropTypes.string, // 限制sex必传为字符串
				age: PropTypes.number, // 限制age为数值
				speak: PropTypes.func, // 限制speak为函数
			}

			// 指定默认标签属性值
			static defaultProps = {
				sex: "不男不女",
				age: 18
			}
		}

		// 渲染组件到页面
		const root1 = ReactDOM.createRoot(document.getElementById('root1'));
		root1.render(<Persons name="jerry" age={19} sex="男" />);
		const root2 = ReactDOM.createRoot(document.getElementById('root2'));
		root2.render(<Persons name="harry" age={25} sex="男" />);
		const p = { name: '老六', age: 18, sex: "女" }
		const root3 = ReactDOM.createRoot(document.getElementById('root3'));
		root3.render(<Persons {...p} />);
	</script>
</body>
```



### 3.6 构造器与props

使用构造器仅用于以下两种情况：

- 通过给`this.state`赋值对象来初始化内部`state`
- 为事件处理函数绑定实例

```js
constructor(props){
// 构造器是否接收props，是否传递给super，取决于：是否希望在构造器中通过this访问props
    super(props)
    console.log('constructor',this.props)
}
```





### 3.7 函数式组件props

理论上函数式组件只能使用三大属性（state，props，refs）中的props

```react
<body>
	<div id="root1"></div>
	<script type="text/babel">
		function Person(props) {
			const { name, sex, age } = props
			return (
				<ul>
					<li>姓名：{name}</li>
					<li>性别：{sex}</li>
					<li>年龄：{age + 1}</li>
				</ul>
			)
		}

		Person.propTypes = {
			name: PropTypes.string.isRequired,
			sex: PropTypes.string,
			age: PropTypes.number,
		}

		Person.defaultProps = {
			sex: "不男不女",
			age: 18
		}

		const root1 = ReactDOM.createRoot(document.getElementById('root1'));
		root1.render(<Person name="jerry" age={19} sex="男" />);

	</script>
</body>
```



### 3.8 refs

#### refs简介

https://zh-hans.reactjs.org/docs/refs-and-the-dom.html#gatsby-focus-wrapper

理解：

- 组件内的标签可以定义ref属性来标识自己             
- 如果使用 `this.refs.textInput` 这种方式访问 refs ，议用`回调函数`或`createRef API `的方式代替
- 现在基本都使用回调函数                                                                                                                                                                                                                       



#### 字符串refs

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Demo extends React.Component {
			render() {
				return (
					<div>
						<input ref="input1" type="text" placeholder="点击按钮显示数据" />
						<br /><br />
						<button ref="btn1" onClick={this.showData}>点我显示数据</button>
						<br /><br />
						<input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点显示数据" />
					</div>
				)
			}
			// 方法
			showData = () => {
				// 解构赋值
				const { input1 } = this.refs
				console.log(input1.value)
			}
			showData2 = () => {
				const { input2 } = this.refs
				console.log(input2.value)
			}
		}
		// 渲染虚拟DOM到页面
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Demo />);
	</script>
</body>
```



> React已弃用字符串形式的ref，建议使用回调函数或者createRef API代替



#### 回调refs

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Demo extends React.Component {
			render() {
				return (
					<div>
						<input ref={(currentNode) => {
							console.log(currentNode) //拿到是ref当前所处的节点
							this.input1 = currentNode
						}} type="text" placeholder="点击按钮显示数据" />
						<br /><br />
						<button onClick={this.showData}>点我显示数据</button>
					</div>
				)
			}
			// 方法
			showData = () => {
				console.log(this)
				const { input1 } = this
				console.log(input1.value)
			}
		}
		// 渲染虚拟DOM到页面
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Demo />);
	</script>
</body>
```



#### 回调ref中执行次数

如果ref回调函数是以内联函数的方式定义的，在更新过程中它会被执行两次，第一次传入参数null，第二次传入参数DOM元素

这是因为在每次渲染时会创建一个新的函数实例，所以 React 清空旧的 ref 并且设置新的

通过将 ref 的回调函数定义成 class 的绑定函数的方式可以避免上述问题，但是大多数情况下它是无关紧要的

点击改变天气的时候，页面重新解析DOM时，ref内联回调函数会调用两次

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Demo extends React.Component {
			render() {
				const { isHot } = this.state
				return (
					<div>
						<h2>今天天气很{isHot ? "炎热" : "凉爽"}</h2>
						<input ref={(currentNode) => {
							console.log(currentNode) //拿到是ref当前所处的节点
							this.input1 = currentNode
						}} type="text" placeholder="点击按钮显示数据" />
						<br /><br />
						<button onClick={this.showData}>点我显示数据</button>
						<button onClick={this.changeWeather}>点我改变天气</button>
					</div>
				)
			}
			// data
			state = {
				isHot: true
			}
			// methods
			showData = () => {
				console.log(this)
				const { input1 } = this
				console.log(input1.value)
			}
			changeWeather = () => {
				const isHot = this.state.isHot
				this.setState({
					isHot: !isHot,
				})
			}
		}
		// 渲染虚拟DOM到页面
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Demo />);
	</script>
</body>
```



#### createRef()

React.createRef调用后返回一个容器，该容器可以存储被ref所标识的节点

该容器是专节点专用（一次只能存一个及节点）

可以定义多个`React.createRef()`容器

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Demo extends React.Component {
			render() {
				return (
					<div>
						<input ref={this.myRef} type="text" placeholder="点击按钮显示数据" />
						<input ref={this.myRef2} type="text" placeholder="点击按钮显示数据2" />
						<br /><br />
						<button onClick={this.showData}>点我显示数据1</button>
						<button onClick={this.showData2}>点我显示数据2</button>
					</div>
				)
			}
			// React.createRef调用后返回一个容器，该容器可以存储被ref所标识的节点
			// 该容器是专人专用（一次只能存一个）
			myRef = React.createRef()
			myRef2 = React.createRef()
			// 方法
			showData = () => {
                // 访问refs
				console.log(this.myRef.current)
			}
			showData2 = () => {
				console.log(this.myRef2.current)
			}
		}
		// 渲染虚拟DOM到页面
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Demo />);
	</script>
</body>
```



官网中使用refs写在构造器中

```react
// 定义
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```

```react
// 访问
const node = this.myRef.current;
```



### 3.9 事件处理

#### 简介

- 通过`onXxx`属性指定事件处理函数（注意大小写）
  - React使用的是自定义（合成）事件，而不是使用的原生DOM事件 —— 为了更好的兼容性
  - React中的事件是通过事件委托方式处理的（委托给组件最外层的元素）—— 为了高效
- 通过`event.target`得到发生事件的DOM元素对象

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Demo extends React.Component {
			render() {
				return (
					<div>
						<input ref={this.myRef} type="text" placeholder="点击按钮显示数据" />
						<input onBlur={this.showData2} type="text" placeholder="点击按钮显示数据2" />
						<br /><br />
						<button onClick={this.showData}>点我显示数据1</button>
					</div>
				)
			}
			// ref容器
			myRef = React.createRef()
			myRef2 = React.createRef()
			// 方法
			showData = () => {
				console.log(this.myRef.current)
			}
			showData2 = (event) => {
				console.log(event.target.value)
			}
		}
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Demo />);
	</script>
</body>
```



#### DOM 事件

https://www.w3school.com.cn/jsref/dom_obj_event.asp



### 3.10 收集表单数据

#### 理解

包含表单的组件分类

- 非受控组件
- 受控组件（建议写，避免大量写ref）（这里非常类似vue中的双向数据绑定）



#### 非受控组件

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 组件
		class Login extends React.Component {
			render() {
				return (
					<div>
						<form action="#" onSubmit={this.handleSubmit}>
							<span>用户名</span>
							<input type="text" name="userName" ref={c => this.userName = c} />
							<br /><br />
							<span>密码</span>
							<input type="password" name="password" ref={c => this.password = c} />
							<button>登录</button>
						</form>
					</div>
				)
			}
			// 方法
			handleSubmit = (event) => {
				// 表单的提交跳转是默认事件
				event.preventDefault()
				const { userName, password } = this
				alert(`${userName.value}, ${password.value}`)
			}
		}
		// 渲染组件
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Login />);
	</script>
</body>
```



#### 受控组件

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 组件
		// 数据存储在state中存取
		class Login extends React.Component {
			render() {
				return (
					<div>
						<form action="#" onSubmit={this.handleSubmit}>
							<span>用户名</span>
							<input type="text" name="userName" onChange={this.saveUserName} />
							<br /><br />
							<span>密码</span>
							<input type="password" name="password" onChange={this.savepPassword} />
							<button>登录</button>
						</form>
					</div>
				)
			}
			// data
			state = {
				userName: "",
				password: "",
			}
			// methods
			handleSubmit = (event) => {
				event.preventDefault()
				const { userName, password } = this.state
				console.log(userName, password)
			}
			saveUserName = () => {
				this.setState({ userName: event.target.value })
			}
			savepPassword = () => {
				this.setState({ password: event.target.value })
			}
		}
		// 渲染组件
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Login />);
	</script>
</body>
```



#### 高阶函数函数柯里化

高阶函数：

- 如果一个函数符合下面2个规范中的任何一个，那么该函数就是高阶函数
  - 若A函数，接收到的参数是一个函数，那么A函数就可以称之为高阶函数
  - 若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数



函数的柯里化

- 通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码方式



```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		// 组件
		// 数据存储在state中存取
		class Login extends React.Component {
			render() {
				return (
					<div>
						<form action="#" onSubmit={this.handleSubmit}>
							<span>用户名</span>
							 {/* 这里其实传递两个参数userName与event */}
							<input type="text" name="userName" onChange={this.saveUserInfo('userName')} />
							<br /><br />
							<span>密码</span>
							<input type="password" name="password" onChange={this.saveUserInfo('password')} />
							<button>登录</button>
						</form>
					</div>
				)
			}
			// data
			state = {
				userName: "",
				password: "",
			}
			// methods
			handleSubmit = (event) => {
				event.preventDefault()
				const { userName, password } = this.state
				console.log(userName, password)
			}
			// 这里的saveUserInfo就是高阶函数
			saveUserInfo = (dataType) => {
				// 第一参数是dataType，第二参数是event，两个函数统一处理
				return (event) => {
					this.setState({ [dataType]: event.target.value })
				}
			}

		}
		// 渲染组件
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Login />);
	</script>
</body>
```



### 3.11 生命周期（旧）

#### 引入生命周期

组件的生命周期：

组件对象从创建到死亡它会经历的阶段

组件的**挂载**与**销毁**

```js
// 组件挂载完毕
componentDidMount() {
    this.startClock()
}
// 组件将要卸载
componentWillUnmount() {
    this.stopClock()
}
```



```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class Clock extends React.Component {
			// render调用的时机：初始化渲染、状态更新之后
			render() {
				return (
					<div>
						<h1>Hello, world!</h1>
						<h2>It is</h2>
						<h2>{this.state.date.toLocaleTimeString()}</h2>
						<button onClick={this.stopClock}>stop the clock</button>
						<button onClick={this.startClock}>start the clock</button>
					</div>
				);
			}
			// 数据
			state = {
				date: new Date()
			}
			// 组件挂载完毕
			componentDidMount() {
				this.startClock()
			}
			// 组件将要卸载
			componentWillUnmount() {
				this.stopClock()
			}

			// 停止clock
			stopClock = () => {
				clearInterval(this.timer)
				console.log("stopClock")
			}
			// 开始clock
			startClock = () => {
				// 设置定时器
				this.timer = setInterval(() => {
					let date = new Date()
					this.setState({ date })
				}, 1000);
				console.log("startClock")
			}
		}
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<Clock />);
	</script>
</body>
```



#### 组件挂载流程

组件挂载时：

1. `constructor`
2. `componentWillMount`
3. `render`
4. `componentDidMount`
5. `componentWillUnmount`



#### setState流程

普通方法中通过`this.setState({ date })`使用

1. `componentWillReceiveProps`
2. `shouldComponentUpdate`<------`setState()`  控制组件更新的阀门
3. `componentWillUpdate`<------`forceUpdate()`   组件将要更新的函数
4. `render`
5. `componentDidUpdate`  组件更新完毕的函数
6. `componentWillUnmount`



#### forceUpdate流程

普通方法中通过`forceUpdate()`使用

`forceUpdate()`强制更新就是比正常更新少走一步

1. `componentWillReceiveProps`
2. `shouldComponentUpdate`<------`setState()`
3. `componentWillUpdate`<------`forceUpdate()`
4. `render`
5. `componentDidUpdate`
6. `componentWillUnmount`



#### 父组件render流程

这里注意一个生命周期函数`componentWillReceiveProps`

注意事项：

- 组件初次渲染时不会执行`componentWillReceiveProps`
- 当`props`发生变化时执行`componentWillReceiveProps`

- 在这个函数里面，旧的属性仍可以通过`this.props`来获取


使用场景：

- 此函数可以作为`react`在`prop`传入之后， `render()`渲染之前更新`state`的机会
- 即可以根据属性的变化，通过调用`this.setState()`来更新组件状态，在该函数中调用`this.setState()`将不会引起第二次渲染
- 也可在此函数内根据需要调用自己的自定义函数，来对`props`的改变做出一些响应


课堂例子：

```react
<body>
	<div id="root"></div>
	<script type="text/babel">
		class A extends React.Component {
			state = {
				carName: true
			}
			changeCar = () => {
				this.setState({
					carName: !this.state.carName
				})
			}
			render() {
				return (
					<div>
						<div>我是A组件</div>
						<button onClick={this.changeCar}>换车</button>
						<B carName={this.state.carName ? "奔驰" : "奥拓"}>换车</B>
					</div>
				)
			}
		}

		class B extends React.Component {
			// 第一次传递props不执行
			// 第二次之后传递props才执行
			// component Will Receive New Props
			componentWillReceiveProps() {
				console.log("componentWillReceiveProps done")
			}
			render() {
				return (
					<div>
						<div>我是B组件</div>
						<div>接收到信息就是{this.props.carName}</div>
					</div>
				)
			}
		}
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(<A />);
	</script>
</body>
```



#### 总结生命周期

初始化阶段：

由`ReactDOM.render()`触发---初次触发

- `constructor()`

- `componentWillMount()`

- `render()`

- `componentDidMount()`

  一般在这个函数里做一些初始化的操作

更新阶段：

由组件内部`this.setState()`或父组件`render`渲染

- `shouldComponentUpdate`
- `componentWillUpdate`
- `render`
- `componentDidUpdate`

卸载阶段：

由`ReactDOM.unmountComponentAtNode()`触发---初次触发

- `componentWillUnmount`

  一般在这个函数中做一些收尾的操作



### 3.12 生命周期（新）

#### 新旧版本对比

需要添加`UNSAFE_`前缀的三个生命周期函数

```js
// 挂载时render之前
UNSAFE_componentWillMount(){
    console.log("componentWillMount")
}

// 父组件传递的props发生变化时执行
UNSAFE_componentWillReceiveProps(){
    console.log("componentWillReceiveProps")
}

// 更新之前
UNSAFE_componentWillUpdate(){
    console.log("componentWillUpdate")
}
```

原因：https://zh-hans.reactjs.org/blog/2018/03/27/update-on-async-rendering.html

我们得到最重要的经验是，过时的组件生命周期往往会带来不安全的编码实践，具体函数如下：

- `componentWillMount`
- `componentWillReceiveProps`
- `componentWillUpdate`

这些生命周期方法经常被误解和滥用；此外，我们预计，在异步渲染中，它们潜在的误用问题可能更大

我们将在即将发布的版本中为这些生命周期添加`UNSAFE_`前缀

这里的`unsafe`不是指安全性，而是表示使用这些生命周期的代码在 React 的未来版本中更有可能出现 bug，尤其是在启用异步渲染之后



#### 生命周期图谱

https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

即将废弃三个生命周期函数

- `componentWillMount`
- `componentWillReceiveProps`
- `componentWillUpdate`



引入了两个生命周期函数

- `static getDerivedStateFromProps()`
- `getSnapshotBeforeUpdate()`



#### 得到派生状态

`static getDerivedStateFromProps()`

从props那里得到一个派生的状态

会在调用`render`方法之前调用，并且在初始挂载及后续更新时都会被调用

它应返回一个对象来更新`state`，如果返回`null`则不更新任何内容

此方法适用于罕见的用例，即`state`的值在任何时候都取决于`props`

派生状态会导致代码冗余，并使组件难以维护

```js
static getDerivedStateFromProps(props, state) {
    console.log("getDerivedStateFromProps", props, state)
    return props
}
```



#### 更新前快照

`getSnapshotBeforeUpdate()`

在最近一次渲染输出（提交到 DOM 节点）之前调用

它使得组件能在发生更改之前从 DOM 中捕获一些信息（例如，滚动位置）

此生命周期方法的任何返回值将作为参数传递给 `componentDidUpdate()`

此用法并不常见，但它可能出现在 UI 处理中，如需要以特殊方式处理滚动位置的聊天线程等

应返回 snapshot 的值（或 `null`）

```react
class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // 我们是否在 list 中添加新的 items ？
    // 捕获滚动位置以便我们稍后调整滚动位置。
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // 如果我们 snapshot 有值，说明我们刚刚添加了新的 items，
    // 调整滚动位置使得这些新 items 不会将旧的 items 推出视图。
    //（这里的 snapshot 是 getSnapshotBeforeUpdate 的返回值）
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}
```

比如页面有十个人，页面添加了一个人，此时有十一个人

这是十一个人生成了，之前十个人的列表有多高呢

此时就可以用这个生命周期函数可以获取之前十个人的列表高度

更新之前来个快照



## 四、React脚手架

### 4.1 react脚手架搭建

#### 脚手架介绍

- react提供了一个用于创建react项目的脚手架库：`create-react-app`
- 项目的整体技术架构为：`react`、`webpack`、`es6`、`eslint`
- 使用脚手架开发的项目的特点：模块化，组件化，工程化



#### 创建项目

1、全局安装

```shell
npm install -g create-react-app
```

2023-1-25：version18.4.0

 2、创建项目

```shell
create-react-app hello-react
```

如果创建没有权限导致失败，用管理员模式打开cmd

不知道为什么clash在shell里无法全局代理导致速度太慢，这里切换为淘宝镜像

查看当前下载环境镜像

```shell
npm config get registry
```

切换为淘宝镜像

```shell
npm config set registry https://registry.npm.taobao.org
```

切换为国外镜像

```shell
npm config set registry https://registry.npmjs.org/
```

3、进入项目文件夹

```shell
cd hello-react
```

4、启动项目

```shell
npm start
```



### 4.2 脚手架文件分析

`robots.txt` 爬虫规则文件

`manifest.json` 应用加壳时候的配置文件

`App.js` `App.css` 组件App

`App.test.js` 用于测试App（几乎不用）

`index.css` index.html的css

 `index.js`  项目入口文件

`reportWebVitals.js` [检测用户体验的标准](https://blog.csdn.net/qiuqiu1894/article/details/123976582)

`setupTests.js` 主要是针对当前项目编写测试代码



### 4.3 一个简单的组件

tips：如何开启vscode的jsx语法自动补全

在setting里搜索`includeLanguages`

添加`javascript:javascriptreact`



在src文件夹下新建components文件夹

在components文件夹下新建Hello和Welcome文件夹，各自创建index.jsx和index.css

注意：组件类必须命名

```jsx
import React, { Component } from "react";
import HelloCSS from './index.module.css'

export default class Hello extends Component {
	render() {
		return (
			<div className={HelloCSS.title}>
				<h2>Hello react!</h2>
			</div>
		)
	}
}
```



在App中引入

```jsx
import './App.css';
import Hello from './components/Hello';
import Welcome from './components/Welcome';

function App() {
	return (
		<div className="App">
			<Hello></Hello>
			<Welcome></Welcome>
		</div>
	);
}

export default App;
```



### 4.4 样式的模块化

防止CSS全局污染，采取样式的模块化

1、CSS文件命名为`[name].module.css`

2、引入和使用CSS

```jsx
import React, { Component } from "react";
import HelloCSS from './index.module.css'

class Hello extends Component {
	render() {
		return (
			<div className={HelloCSS.title}>
				<h2>Hello react!</h2>
			</div>
		)
	}
}

export default Hello
```



tips：一般情况下采用less的嵌套写法的话，就不太会用到上述方法

tips：`ES7+ React/Redux/React-Native snippets` 插件，创建index.jsx时候直接输入`rcc`，`rfc`创建类组件或函数式组件



### 4.5 组件化编码流程

1. 拆分组件：拆分界面抽取组件
2. 实现静态组件：使用组件实现静态页面效果
3. 实现动态组件：动态显示初始化数据（数据类型、数据名称、数据保存）与交互



### 4.6 组件的组合使用

TodoList实现

功能：组件化实现此功能

1. 显示所有todo列表
2. 输入文本，点击按钮显示到列表的首位，并清除输入的文本



在决定css选择的时候

Less和Sass的主要不同就是他们的实现方式

Less是基于JavaScript，是在客户端处理的

Sass是基于Ruby的，是在服务器端处理的



学成sass归来~~

react项目安装sass

```shell
npm install node-sass
```

清除npm缓存

```shell
npm cache clean --force
```

安装npm

```shell
npm install
```



数据传递

父传子：自定义属性

子传父：自定义方法



做完，记得复习一下ES6数组方法



## 五、React ajax

### 5.1 理解

- React本身只关注于界面，不包含发送ajax请求的代码
- 前端应用需要通过ajax请求与后天进行交互（json数据）
- react应用中需要集成第三方ajax库或自己封装



### 5.2 axios

#### axios安装

```shell
npm install axios
```



#### 请求封装

react中可以将axios封装成一个文件，通过控制操作，可以实现错误、逻辑、和验证统一处理，降低代码的冗余度和可读性

```js
/**
 * 网络请求配置
 */
import axios from "axios";
 
axios.defaults.timeout = 100000;
axios.defaults.baseURL = "http://test.mediastack.cn/";
 
/**
 * http request 拦截器
 */
axios.interceptors.request.use(
  (config) => {
    config.data = JSON.stringify(config.data);
    config.headers = {
      "Content-Type": "application/json",
    };
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);
 
/**
 * http response 拦截器
 */
axios.interceptors.response.use(
  (response) => {
    if (response.data.errCode === 2) {
      console.log("过期");
    }
    return response;
  },
  (error) => {
    console.log("请求出错：", error);
  }
);
 
/**
 * 封装get方法
 * @param url  请求url
 * @param params  请求参数
 * @returns {Promise}
 */
export function get(url, params = {}) {
  return new Promise((resolve, reject) => {
    axios.get(url, {
        params: params,
      }).then((response) => {
        landing(url, params, response.data);
        resolve(response.data);
      })
      .catch((error) => {
        reject(error);
      });
  });
}
 
/**
 * 封装post请求
 * @param url
 * @param data
 * @returns {Promise}
 */
 
export function post(url, data) {
  return new Promise((resolve, reject) => {
    axios.post(url, data).then(
      (response) => {
        //关闭进度条
        resolve(response.data);
      },
      (err) => {
        reject(err);
      }
    );
  });
}
 
/**
 * 封装patch请求
 * @param url
 * @param data
 * @returns {Promise}
 */
export function patch(url, data = {}) {
  return new Promise((resolve, reject) => {
    axios.patch(url, data).then(
      (response) => {
        resolve(response.data);
      },
      (err) => {
        msag(err);
        reject(err);
      }
    );
  });
}
 
/**
 * 封装put请求
 * @param url
 * @param data
 * @returns {Promise}
 */
 
export function put(url, data = {}) {
  return new Promise((resolve, reject) => {
    axios.put(url, data).then(
      (response) => {
        resolve(response.data);
      },
      (err) => {
        msag(err);
        reject(err);
      }
    );
  });
}
 
//统一接口处理，返回数据
export default function (fecth, url, param) {
  let _data = "";
  return new Promise((resolve, reject) => {
    switch (fecth) {
      case "get":
        console.log("begin a get request,and url:", url);
        get(url, param)
          .then(function (response) {
            resolve(response);
          })
          .catch(function (error) {
            console.log("get request GET failed.", error);
            reject(error);
          });
        break;
      case "post":
        post(url, param)
          .then(function (response) {
            resolve(response);
          })
          .catch(function (error) {
            console.log("get request POST failed.", error);
            reject(error);
          });
        break;
      default:
        break;
    }
  });
}
 
//失败提示
function msag(err) {
  if (err && err.response) {
    switch (err.response.status) {
      case 400:
        alert(err.response.data.error.details);
        break;
      case 401:
        alert("未授权，请登录");
        break;
 
      case 403:
        alert("拒绝访问");
        break;
 
      case 404:
        alert("请求地址出错");
        break;
 
      case 408:
        alert("请求超时");
        break;
 
      case 500:
        alert("服务器内部错误");
        break;
 
      case 501:
        alert("服务未实现");
        break;
 
      case 502:
        alert("网关错误");
        break;
 
      case 503:
        alert("服务不可用");
        break;
 
      case 504:
        alert("网关超时");
        break;
 
      case 505:
        alert("HTTP版本不受支持");
        break;
      default:
    }
  }
}
 
/**
 * 查看返回的数据
 * @param url
 * @param params
 * @param data
 */
function landing(url, params, data) {
  if (data.code === -1) {
  }
}
```



#### 组件调用

```react
import React, { Component } from "react";
import { getArticleList } from "~/api/blog";
 
class Home extends Component {
    constructor(props) {
        super(props);
    } 
 
    componentDidMount() {
       getArticleList().then(
          (res) => {
              console.log("get article response:", res);
          },
         (error) => {
              console.log("get response failed!");
          }
       );
    }
 
 ......
}
 
 
export default Home;
```



### 5.3 脚手架配置代理

- 这是前端解决跨域问题
- 一般用不到
- 用到再学



## 六、组件间通信

### 6.1 方法概述

父传子：自定义属性

子传父：自定义事件

兄弟之间：消息订阅与发布、redux



### 6.2 消息订阅发布

工具库：PubSubJS

下载：

```shell
npm install pubsub-js --save
```

使用：

```js
// 引入
import PubSub from 'pubsub-js' 
// 订阅
PubSub.subsribe('delete',function(data){}); 
// 发布消息
PubSub.publish('delete',data)
```



