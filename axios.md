#  Axios



## 一、HTTP相关

### 1.1 MDN文档

大概率不会去看。。



### 1.2 HTTP请求的基本过程

```
客户端-->服务器：请求行、请求头、请求体
服务器-->客户端：响应行、响应头、响应体
```

1. 浏览器向服务器发送HTTP请求（请求报文）
2. 后台服务器收到请求后，处理请求，向浏览器端返回HTTP响应（响应报文）
3. 浏览器端接收到响应，解析**显示响应体**或**调用回调函数**



### 1.3 HTTP请求报文

1、请求行

```
格式：method/url
例如：GET/product_detail?id=2 或 POST/login
```

2、请求头（一般有多个请求头）

```
host:www.baidu.com
Cookie:BAIDUID=AD3B0FA706E;BIDUPDIF=AD3B0FA706
Content-Type:application/x-www-form-urlencoded或者application/json
```

3、请求体

`get`请求没有请求体

```
username=tom&pwd=123
{"username":"tom","pwd":123}
```



### 1.4 HTTP响应报文

1、响应行

```
格式：status statusText
例如：200 OK 或 404 Not Found
```

2、响应头（一般有多个）

```
Content-Type:text/html;charset=utf-8
Set-Cookie:BD_CK_SAM=1;path=/
```

3、响应体

```
html/json/js/css/图片
```



### 1.5 常见的响应状态码

| 状态码 | 返回                  | 备注                               |
| ------ | --------------------- | ---------------------------------- |
| 200    | OK                    | 请求成功，一般用于GET或POST请求    |
| 201    | Create                | 已创建，成功请求并创建了新的资源   |
| 401    | Unauthorized          | 未授权/请求要求用户的额身份认证    |
| 404    | Not Found             | 服务器无法根据客户端的请求找到资源 |
| 500    | Internal Server Error | 服务器内部错误，无法完成请求       |



### 1.6 请求方式和请求参数

**请求方式**

1. GET（索取）：从服务器读取数据
2. POST：向服务器端添加新数据
3. PUT：更新服务器端已存在的数据
4. DELETE：删除服务器端的数据



**请求参数**

（1）`query`参数（查询字符串参数）

1. 参数包含在请求地址中，格式为`:/xxxx?name=tom&age=18`
2. 敏感数据不要用`query`参数，因为参数是地址的一部分，比较危险
3. 备注：`query`参数又称查询字符串参数，编码方式为`urlencoded`



（2）`params`参数

1. 参数包含在请求地址中，格式为`http://localhost:3900/add_person/tom/18`
2. 敏感数据不要用params参数，因为参数是地址的一部分，比较危险



（3）请求体参数

1. 参数包含在请求体中，可通过浏览器开发工具查看

2. 常见的两种格式

   ```
   格式一:urlencoded格式
       例如:name=tom&age=19
       对应请求头:Content-Type:application/x-www-form-urlencoded
   
   格式二:json格式
       例如:{"name":"tom","age":12}
       对应的请求头:Content-Type:application/json
   ```



**注意**

1. GET请求不能携带请求体参数，因为GET请求没有请求体

2. 理论上一次请求可以随意使用上述3种类型参数中的任何一种，甚至一次请求的3个参数可以用3种形式携带，但一般不这样做

3. 一般来说我们有一些约定俗成的**规矩**：

   例如`form`表单发送`post`请求时：自动使用请求体参数，用`urlencoded`编码

   例如`jQuery`发送`ajax=post`请求时：自动使用请求体参数，用`urlencoded`编码

4. 开发中请求到底发送给谁，用什么请求方式，携带什么参数？需要参考项目的API接口文档




## 二、API相关

### 2.1 API的分类

1、REST API（restful风格的API）

- 发送请求进行CRUD（增删改查）哪个操作由请求方式来决定
- 同一请求路径可以进行多个操作
- 请求方式会用到GET/POST/PUT/DELETE

2、非REST API（restless风格的API）

- 请求方式不决定请求的CRUD操作
- 一个请求路径只对应一个操作
- 一般只有GET/POST



### 2.2 json-server使用

1、 json-server是什么？

用来快速搭建REST API的工具包

2、使用json-server

在线文档

```
http://github.com/typicode/json-server
```

下载（全局安装）

```
npm install -g json-server
```

目标根目录下创建数据库json文件db.json

```json
{
  "posts": [
    {
      "id": 1,
      "title": "json-server",
      "author": "typicode"
    }
  ],
  "comments": [
    {
      "id": 1,
      "body": "some comment",
      "postId": 1
    }
  ],
  "profile": {
    "name": "typicode"
  }
}
```



### 2.3 Postman接口测试工具

Param选项卡里调整的是query参数

如果需要调整params参数直接在上面地址写



### 2.4 一般http请求与ajax请求

1. ajax请求是一种特别的http请求

2. 对于服务端来说，没有任何区别，区别在浏览器端

3. 浏览器端发送请求：只有XHR或fetch发送的才是ajax请求，其他所有的都是非ajax请求

4. 浏览端接收到响应

   - 一般请求：浏览器一般会显示响应体数据，也就是我们常说的自动刷新/跳转页面

   - ajax请求：浏览器不会对界面进行任何更新操作，只是调用监视的回调函数并传入响应相关数据



## 三、axios的理解与使用

### 3.1 axios概念

前端最流行的ajax请求库

react/vue官方都推荐使用axios发ajax请求

文档

```
http://github.com/axios/axios
```



### 3.2 axios特点

1. 基于Promise的异步ajax请求库
2. 浏览器端/Node端都可以使用
3. 支持请求/响应拦截器
4. 支持请求取消
5. 请求/响应数据转换
6. 批量发送多个请求



### 3.3 axios发送GET请求

使用axios发送一个简单的GET请求

axios调用的返回值是promise实例

成功的值叫做response，失败的值叫做error

axios成功的值是一个axios封装的response对象，服务器返回的真正数据在response.data中

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>axios-get</title>
	<script src="./js/axios.min.js"></script>
</head>

<body>
	<button id="btn01">get请求获取数据完整版</button>
	<button id="btn02">get请求获取数据精简版</button>
	<script>
		const btn01 = document.getElementById("btn01")
		const btn02 = document.getElementById("btn02")
		// 完整版
		// 发送GET请求---不携带参数
		btn01.onclick = () => {
			const result = axios({
				url: 'http://localhost:3000/posts', // 请求地址
                timeout:2000, // 设置超时时间
				methods: 'GET', // 请求方式
			})
			result.then(
				response => {
					console.log("请求成功", response.data)
				},
				error => {
					console.log("请求失败", response.error)
				}
			)
		}
		// 精简版
		// 发送GET请求---不携带参数
		btn02.onclick = () => {
			axios.get('http://localhost:3000/posts').then(
				response => {
					console.log("请求成功", response.data)
				},
				error => {
					console.log("请求失败", response.error)
				}
			)
		}
	</script>
</body>

</html>
```



query参数查询指定id

携带query参数时，编写的配置项叫做params，但携带的是query参数

```js
// 获取某个人
btn03.onclick = () => {
	// 完整版
	axios({
		url: 'http://localhost:3000/person', // 请求地址
		methods: 'GET', // 请求方式
		params: {
			id: personId.value
		}
	}).then(
		response => {
			console.log("请求成功", response.data)
		},
		error => {
			console.log("请求失败", error)
		}
	)
	// 精简版
	axios('http://localhost:3000/person', { params: { id: personId.value } }).then(
		response => {
			console.log("请求成功", response.data)
		},
		error => {
			console.log("请求失败", error)
		}
	)
}
```



### 3.4 axios发送POST请求

axios发送POST请求，添加一个人

发送POST请求，携带请求体参数（json编码/urlencoded编码）

```js
// 完整版 
axios({
	url: 'http://localhost:3000/person', // 请求地址
	methods: 'POST', // 请求方式
	data: {
		name: personName.value,
		age: personAge.value
	} // 携带请求体参数（json编码）
	// data:`name=${personName.value}&age=${personAge.value}` // 携带请求体参数（urlencoded编码）
}).then(
	response => {
		console.log("请求成功", response.data)
	},
	error => {
		console.log("请求失败", error)
	}
)

// 精简版
// 如果需要携带请求体参数（urlencoded编码），第二个参数传入模板字符串写法
axios.post('http://localhost:3000/person', {
	name: personName.value,
	age: personAge.value
}).then(
	response => {
		console.log("请求成功", response.data)
	},
	error => {
		console.log("请求失败", error)
	}
)
```



### 3.5 axios发送put请求

```js
btn06.onclick = () => {
	const result = axios({
		url: `http://localhost:3000/person/${personUpdataId.value}`, // 请求地址
		method: 'PUT', // 请求方式
		data: {
			name: personUpdataName.value,
			age: personUpdataAge.value
		},
	})
	result.then(
		response => {
			console.log("请求成功", response.data)
		},
		error => {
			console.log("请求失败", error)
		}
	)
}
```



### 3.6 axios发送DELETE请求

```js
// 删除一个人
btn05.onclick = () => {
	axios({
		url: `http://localhost:3000/person/${personDeleteId.value}`, // 请求地址
		method: 'DELETE', // 请求方式
	}).then(
		response => {
			console.log("请求成功", response.data)
		},
		error => {
			console.log("请求失败", error)
		}
	)
}
```



## 四、axios常用配置项

### 4.1 axios配置项

axios有37个配置选项

给axios配置默认属性

```html
<body>
	<button id="btn01">点我获取所有人</button>
	<button id="btn02">点我获取测试数据</button>
	<script>
		const btn01 = document.getElementById("btn01")
		const btn02 = document.getElementById("btn02")

		// 给axios配置默认属性
		axios.defaults.timeout = 2000
		axios.defaults.headers = { demo: 123 }
		axios.defaults.baseURL = 'http://localhost:3000' //统一配置默认地址

		btn01.onclick = () => {
			axios({
				// 一共有37个配置项
				url: '/person', // 请求地址
				method: 'GET', // 请求方式
				//params:{a:1.b:2} // 配置query参数
				//data:{c:3,d:3} // 配置请求体参数（json编码）
				//data:'e=5&f=6', // 配置请求体参数（urlencoded编码）
				//timeout:2000, // 配置超时时间
				//headers:{demo:123}, // 配置请求头信息
				//responseType:'json', // 配置响应数据的格式（默认值为json）

			}).then(
				response => {
					console.log("请求成功", response.data)
				},
				error => {
					console.log("请求失败", error)
				}
			)
		}
	</script>
</body>

```



### 4.2 token请求头

todo



## 五、axios.create方法

### 5.1 axios.create

axios.create(config) 对axios请求进行二次封装

1. 根据指定配置创建一个新的`axios`，也就是每个新`axios`都有自己的配置

2. 新`axios`只是没有取消请求和批量发请求的方法，其它所有语法都是一致的

3. 为什么要设计这个语法?

   - 需求：项目中有部分接口需要的配置与另一部分接口需要的配置不太一样，如何处理

   - 解决：创建2个新`axios`，每个都有自己特有的配置，分别应用到不同变求的接口请求中

```html
<body>
	<button id="btn01">点我获取所有人</button>
	<script>
		const btn01 = document.getElementById("btn01")

		const axios2 = axios.create({
			timeout: 2000,
			headers: { demo: 123 },
			baseURL: 'http://localhost:3000',

		})

		btn01.onclick = () => {
			axios2({
				url: '/person', // 请求地址
				method: 'GET', // 请求方式
			}).then(
				response => {
					console.log("请求成功", response.data)
				},
				error => {
					console.log("请求失败", error)
				}
			)
		}
	</script>
</body>
```



## 六、axios拦截器

### 6.1 官网实例

在请求或响应被 `then` 或 `catch` 处理前拦截它们

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
	// 在发送请求之前做些什么
	return config;
}, function (error) {
	// 对请求错误做些什么
	return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
	// 对响应数据做点什么
	return response;
}, function (error) {
	// 对响应错误做点什么
	return Promise.reject(error);
});
```



### 6.2 axios请求拦截器

axios请求拦截器

概念：在真正发送请求之前执行的一个回调函数

作用：对所有请求做统一的处理：追加请求头、追加参数、界面loading提示等等

```html
<body>
	<button id="btn01">点我获取所有人</button>
	<script>
		const btn01 = document.getElementById("btn01")

		// 请求拦截器的本质就是一个函数
		// 每一次调用axios发送请求的时候，都会调用请求拦截器
		axios.interceptors.request.use((config) => {
			// 如果token与服务器token一致，才有权限操作
			if (1) {
				config.headers.token = 'atguigu'
			}
			// config 当前axios配置项
			console.log(config)
			return config
		})

		btn01.onclick = () => {
			axios({
				url: 'http://localhost:3000/person', // 请求地址
				method: 'GET', // 请求方式
			}).then(
				response => {
					console.log("请求成功", response.data)
				},
				error => {
					console.log("请求失败", error)
				}
			)
		}
	</script>
</body>
```



### 6.3 axios响应拦截器

axios响应拦截器

概念：得到响应之后执行的一个回调函数

作用：若成功失败，对成功的数据进行处理；若请求失败，对失败进行进一步操作

```html
<body>
	<button id="btn01">点我获取所有人</button>
	<script>
		const btn01 = document.getElementById("btn01")

		// 请求拦截器的本质就是一个函数
		// 每一次调用axios发送请求的时候，都会调用请求拦截器
		axios.interceptors.request.use((config) => {
			// 如果token与服务器token一致，才有权限操作
			if (1) {
				config.headers.token = 'atguigu'
			}
			// config 当前axios配置项
			console.log(config)
			return config
		})

		// 响应拦截器
		// 只要网络状态码不是2开头的，都定义为错误回调
		axios.interceptors.response.use(
			response => {
				// 进行响应拦截操作
				console.log("响应拦截器成功的回调执行了", response)
				// 必须要有返回值
				return response.data
			},
			error => {
				console.log("响应拦截器失败的回调执行了", error)
				alert(error)
				return new Promise(()=>{})
			}
		)

		btn01.onclick = async() => {
			const result = await axios.get('http://localhost:3000/person')
			console.log(result)
		}
	</script>
</body>
```





## 七、axios取消请求

todo用到再学



## 八、axios批量发送请求

### 8.1 点我批量发送请求

```html
<body>
	<button id="btn01">点我批量发送请求</button>
	<script>
		const btn01 = document.getElementById("btn01")
		btn01.onclick = () => {
			// axios批量发送请求
			axios.all([
				axios.get('http://localhost:3000/person'),
				axios.get('http://localhost:3000/comments'),
				axios.get('http://localhost:3000/profile'),
			]).then(
				response => {
					console.log("请求成功", response)
				},
				error => {
					console.log("请求失败", error)
				}
			)
		}
	</script>
</body>
```



## 九、结课小结

### 9.1 axios解决问题

1. 解决回调地狱
2. 拦截器
3. 批量发送请求











































