# NextJS

## 一、NextJS

### 1.1 简介

NextJS：the react framework for production

- NextJS用于生产的React框架
- NextJS是ReactJS的**全栈**框架
- NextJS建立在ReactJS之上，通过添加许多核心功能来增强ReactJS

  

### 1.2 关键特性

- 拥有内置的服务端渲染支持（Server-side Rendering）
  - 搜索引擎优化（great for SEO）
  - 解决用户因页面加载时产生不好的用户体验
  - 很好的融合客户端和服务端
- 基于文件的路由
  - 将使用文件和文件夹定义页面和路由
  - 代码量减少，提高工作量，且易读
- 完整的堆栈框架
  - 容易添加后端代码到项目中（Nodejs）
  - 允许添加代码来存储数据到数据库或文件等等
  - 不必单独搭建一个REST API后端



## 二、环境搭建

**脚手架安装**

先安装NodeJS

使用脚手架前，需要先进行全局安装

```
npm install -g create-next-app
```



Nextjs创建项目（执行下面命令行之前记得安装nodejs）

```shell
npx create-next-app nextjs-demo
```



启动服务器（内置服务器，服务于NextJS页面和整个应用程序），支持热更新

运行完成后会在`http://localhost:3000`端口显示

```
npm run dev
```



部署应用程序，为生产构建，为部署生成优化的输出的服务器

```
npm run build
```



启动优化的服务器

```
npm run start
```



## 三、课程概述

### 3.1 基础内容与功能

- 基于文件的路由
- 页面预渲染与服务端渲染
- 结合标准的`React`与`NextJS`
- API路由与构架全栈程序



### 3.2 高级理念

- 优化的可能性，例如如何设置页面源数据、如何优化图像
- 框架背后理论
- 部署与配置如何添加身份认证到NextJS项目中



### 3.3 总结复习

- ReactJS进修模块
- NextJS总结模块





## 四、React 复习

### 4.1 React概念

客户端JavaScript库构建用户界面

局部更新



## 五、NextJS 路由

学习目标

- 基于文件的路由架构
- 静态路由和动态路由
- 页面导航




### 5.1 理解

#### 对比ReactJS路由

- 不用安装react-router-dom，不用花费额外的jsx代码编写页面路由

- 根据特殊的文件夹结构，推断路由路线




#### NextJS路由如何工作

我们最常使用的文件夹是`pages`

在 NextJS 中`xxx.js`内部定义的每个文件都pages映射到一个类似命名的路由：

- pages/about.js将映射到/about
- pages/contact.js将映射到/contact
- pages/blog.js将映射到/blog



### 5.2 静态路由

Next.js中的路由系统不同于您在React-router中使用的路由系统

路由是**基于目录的** ，无需键入任何代码即可创建路由

 如果在项目根目录中查找，则可以找到一个名为**“ pages”**的文件夹

 应用程序的路由与该文件夹及其中的文件完全相关



### 5.3 动态路由

采用中括号命名文件或者文件夹`[name] or [name].jsx`

可以在`[country]`文件夹中创建` index.js`，

因此`http://localhost:3000/italy`也是有效的路由，并呈现`index.js`文件的内容







































































