# Sass



## 一、概述

### 1.1 预处理器概念 

#### 出现背景

CSS基本上是设计师的工具，不是程序员的工具。在程序员的眼里，CSS是很头痛的事情，它并不像其它程序语言，比如说PHP、Javascript等等，有自己的变量、常量、条件语句以及一些编程语法，只是一行行单纯的属性描述，写起来相当的费事，而且代码难易组织和维护。

很自然的，有人就开始在想，能不能给CSS像其他程序语言一样，加入一些编程元素，让CSS能像其他程序语言一样可以做一些预定的处理。这样一来，就有了“CSS预处理器（CSS Preprocessor）”。



#### 定义

CSS预处理器基本思想是，用一种专门的编程语言，为CSS增加了一些编程的特性

将CSS作为目标生成文件，然后开发者就只要使用这种语言进行编码工作



#### 优势

- 更加简洁
- 适应性更强
- 可读性更佳
- 更易于代码的维护



### 1.2 预处理器介绍

#### Sass

Sass是对CSS（层叠样式表）的语法的一种扩充，诞生于2007年，最早也是最成熟的一款CSS预处理器语言，它可以使用变量、常量、嵌套、混入、函数等功能，可以更有效有弹性的写出CSS。Sass最后还是会编译出合法的CSS让浏览器使用，也就是说它本身的语法并不太容易让浏览器识别，因为它不是标准的CSS格式，在它的语法内部可以使用动态变量等，所以它更像一种极简单的动态语言。

其实现在的Sass已经有了两套语法规则：一个依旧是用缩进作为分隔符来区分代码块的；另一套规则和CSS一样采用了大括号（｛｝）作为分隔符。后一种语法规则又名SCSS，在Sass3之后的版本都支持这种语法规则。

注：Sass的官网：[http://sass-lang.com](http://sass-lang.com/)



#### LESS

2009年开源的一个项目，受Sass的影响较大，但又使用CSS的语法，让大部分开发者和设计师更容易上手。LESS提供了多种方式能平滑的将写好的代码转化成标准的CSS代码，在很多流行的框架和工具中已经能经常看到LESS的身影了（例如Twitter的Bootstrap框架就使用了LESS）。

根据维基百科上的介绍，其实LESS是Alexis Sellier受Sass的影响创建的一个开源项目。当时SASS采用了缩进作为分隔符来区分代码块，而不是CSS中广为使用的大括号（｛｝）。为了让CSS现有的用户使用起来更佳方便，Alexis开发了LESS并提供了类似CSS的书写功能。

注：LESS的官网：[http://lesscss.org](http://lesscss.org/)



#### Stylus

Stylus，2010年产生，来自于Node.js社区，主要用来给Node项目进行CSS预处理支持，在此社区之内有一定支持者，在广泛的意义上人气还完全不如Sass和LESS。

Stylus被称为是一种革命性的新语言，提供一个高效、动态、和使用表达方式来生成CSS，以供浏览器使用。Stylus同时支持缩进和CSS常规样式书写规则。

注：Stylus官网：http://learnboost.github.com/stylus



## 二、Sass语法

### 2.1 `.sass`与`.scss`

`Sass`和`SCSS`其实是同一种东西，我们平时称之为`Sass`，两者之间不同之处有以下两点：

1. 文件扩展名不同，Sass是以`.sass`后缀为扩展名，而SCSS是以`.scss`后缀为扩展名
2. 语法书写方式不同，Sass是以严格的缩进式语法规则来书写，不带大括号`{}`和分号`;`，而SCSS的语法书写和我们的CSS语法书写方法非常类似。

**Sass语法**

```scss
/*	Sass基础教程
	by sass

//	白日依山尽
	黄河入海流
```

```scss
@import base

=alert
	color: #fff
	background: #666

.alert-waring
	+alert

ul
	font-size: 15px
	li
		list-style:none
```

**SCSS语法**

```scss
/*	Sass基础教程
	by sass		*/

//	白日依山尽
//	黄河入海流
```

```scss
@import "base";

@mixin alert {
    color: #fff;
	background: #666;
}

.alert-warning {
    @include alert;
}

ul {
    font-size: 15px;
    li {
        list-style: none;
    }
}
```



### 2.2 变量

定义/声明一个变量

```scss
$primary-color: #1269b5;
```

使用变量

```scss
$primary-color: #1269b5;
$primary-border: 1px solid $primary-color;

div.box{
    background-color: $primary-color;
}

h1.page-header{
    border: $primary-border;
}
```



### 2.3 嵌套

Nesting

原始css

```css
.nav {
    height: 100px;
}

.nav ul {
    margin: 0;
}

.nav ul li {
    float:left;
    list-style: none;
    padding: 5px;
}
```

嵌套后

```scss
.nav {
    height: 100px;
    ul {
    	margin: 0;
        li {
            float:left;
            list-style: none;
            padding: 5px;
        }
	}
}
```



### 2.4 嵌套时调用父选择器

`&`

```scss
.nav {
    height: 100px;
    ul {
    	margin: 0;
        li {
            float:left;
            list-style: none;
            padding: 5px;
        }
        a {
            display: block;
            color: #000;
            padding: 5px;
            &:hover { 
                 background-color: #999;
		         color: #fff;
            }
        }
	} 
    & &-text {
        font-size: 15px;
    }
}
```

这里的`&`相当于给a定义hover

```css
.nav ul a:hover {
    background-color: #999;
    color: #fff;
}
```

```css
.nav .nav-text {
	font-size: 15px;
}
```

  

### 2.5 嵌套属性

多属性可嵌套

```scss
body {
    font: {
        family: Helvetica, Arial, sans-serif;
        size: 15px;
        weight: normal;
    }
}

.nav {
    border: 1px solid #000 {
        left: 0;
        right: 0;
    }
}
```

```css
body {
    font-family: Helvetica, Arial, sans-serif;
    font-size: 15px;
    font-weight: normal;
}
.nav {
    border: 1px solid #000;
    border-left: 0;
    border-right: 0;
}
```



### 2.6 Mixins

在sass中可以声明@mixin来使用sass的一个规则集中

```scss
@mixin name (param1, param2...) {
	...
}
```



定义@mixin

```scss
@mixin alert{
    background-color: #999;
    color: #fff;
}
```

使用@mixin时候，使用`@include`

```scss
.alert-warning {
	@include alert;
}
```



@mixin定义可使用嵌套

```scss
@mixin alert{
    background-color: #999;
    color: #fff;
    a {
    	color: #664c2b
    }
}
```

@mixin定义参数

```scss
@mixin alert($text-color, $background-color) {
    background-color: $background-color;
    color: $text-color;
    a {
        // 颜色函数：加深百分之十
    	color: darken($text-color, 10%);
    }
}

.alert-warning {
    // 参数顺序须一致
	@include alert(#666, #999);
}

.alert-info {
    @include alert($background-color:#999, $text-color:#666);
}
```



### 2.6 继承/扩展

功能：让一个选择器去继承/扩展另一个选择器中的所有样式

```scss
@extend name
```



例如

```scss
.alert {
	padding: 15px
}

.alert-info {
	@extend .alert;
    background-color: #999;
}
```

转化为css是群组选择器

```css
.alert, .alert-info {
	padding: 15px
}

.alert-info {
    background-color: #999;
}
```



相关样式也会被继承

```scss
.alert {
	padding: 15px
}

.alert a {
	font-weight: bold;
}

.alert-info {
	@extend .alert;
    background-color: #999;
}
```

```css
.alert, .alert-info {
	padding: 15px
}

.alert, .alert-info a {
	font-weight: bold;
}

.alert-info {
    background-color: #999;
}
```



### 2.7 `@import`

#### 区别

CSS中的`@import`

- 它更多是用来做媒体查询的
- 它每引入一个文件，都会向服务器发送一次请求
- 它并不是把引入的文件和当前文件进行融合
- 引入文件中定义的变量不能在当前文件中使用



Sass 拓展了 @import 的功能，允许其导入 SCSS 或 Sass 文件

被导入的文件将合并编译到同一个 CSS 文件中

被导入的文件中所包含的变量或者混合指令 (mixin) 都可以在导入的文件中使用



#### 命名规则

不过Sass拓展的@import不能包含以下信息：

- 文件拓展名是.css
- 文件名以http://开头；
- 文件名是url();
- 不能包含媒体查询 media queries。



#### 导入

@import 可以导入拓展名是.scss 和.sass的文件

如果没有指定拓展名，Sass将会尝试寻找文件名相同，拓展名为.scss 或 .sass的文件并将其导入

```scss
@import "style.scss"
或
@import "style"
```



**Partials**

Sass可以把Sass文件当做一个组件引入而不会把这个组件单独编译成css文件

而想要实现这个功能只需要在文件名前面加上一个下划线就可以了

比如_components.scss这时候编辑器不会自动编译这个文件

而只有当我们在另一个scss文件里引入这个文件之后，才会把这个文件里的内容编译到引入的文件里

这种组件，Sass称之为 Partials



#### 嵌套

在Sass中，@import还可以用于嵌套：

```scss
.example {
  color: red;
}
 
#main {
  @import "example";
}
 
编译之后：
#main .example {
  color: red;
}
```



#### 媒体查询

Sass的嵌套体系中还有一个比较好用的东西 @media .

这个指令的基本用法和css中的用法基本一样，只是增加了一点额外的功能：允许其在css规则中嵌套。

```scss
//  选择器sidebar 宽度为 300 当媒询条件满足时，宽度为500 
.sidebar {
  width: 300px;
  @media screen and (orientation: landscape) {
    width: 500px;
  }
}
```



#### 媒体查询互相嵌套使用

甚至 @media 的 queries 允许互相嵌套使用，编译时，Sass 自动添加 and

```scss
@media screen {
  .sidebar {
    @media (orientation: landscape) {
      width: 500px;
    }
  }
}
 
编译之后：
@media screen and (orientation: landscape) {
  .sidebar {
    width: 500px; 
  } 
}
```



### 2.8 `interpolation`

把变量或者表达式插入到`#{}`中

类似模板字符串



## 三、Sass数据类型

### 3.1 注释

```scss
// 定义一个占位符
/* 调用一个占位符 */
```



### 3.2 数据类型

Sass 语言中支持的数据类型有下面几种：

- numbers：表示整数类型。
- strings：在单引号 '' 或双引号 "" 内定义的字符序列。
- booleans：布尔类型，有 true 和 false 两个值。
- colors：用于定义颜色值。
- nulls：指定空值，是未知数据。
- lists：值列表类型，表示由空格或逗号分隔的值。
- maps：从一个值映射到另一个值。



### 3.3 数字

数字在 CSS 中应用的很广泛，大多数都是结合单位一起使用的

但是在技术上依然算是数字，例如字体大小、长高、外边距内边距等

Sass 中也有数字（numbers ）类型，数字类型的值可以做一些加减乘除的运算



示例：

例如定义一个变量 `$num`，给这个变量赋一个数字类型的值：

```scss
$num:24px;

.xkd{
    font-size: $num - 4;
    padding: $num + 6px;
    width: $num * 5;
    border-radius: $num / 6;
}
```

编译成css：

```css
.xkd {
  font-size: 20px;
  padding: 30px;
  width: 120px;
  border-radius: 4px;
}
```



### 3.4 字符串

Sass 中的字符串可以使用单引号 `''` 或者双引号 `""` 包围

例如 `"hello"` 或 `'hello'`，即使包围的是一个空格，也算是字符串

字符串也可以不使用引号包围，例如 `hello`，也表示一个字符串

不带引号则省去空格

示例：

我们定义一个字符串类型的变量：

```scss
$msg:"hello";

.one{
    content: $msg;
    .two{
        content: $msg + ' ' + summer;
    }
}
```

编译成 CSS 代码：

```css
.one {
  content: "hello";
}
.one .two {
  content: "hello summer";
}
```



**单位不兼容**

上述代码中，我们可以对这个变量进行加减乘除运算。但是需要注意，在使用数字类型进行计算时，如果值的单位不兼容会导致报错，例如 `12px + 2em` ，执行代码后会报错 `Error: Incompatible units: 'em' and 'px'.`，告诉我们单位不兼容。



### 3.5 颜色

Sass 中的 color 类型表示颜色类型，可以包括所有的颜色值，例如十六进制颜色值、颜色名称、rgb、rgba、hsl、hsla 等。

示例：

```scss
$color1:pink;
.one{
    color: $color1;
    background-color: $color1 + blue;
}
```

编译成 CSS 代码：

```css
.one {
  color: pink;
  background-color: #ffc0ff;
}
```

从上述代码中可以看出，颜色值也是可以计算的，在进行计算时会先将颜色值转换为十六进制值，然后进行计算。



### 3.6 列表

Sass 中的列表类型是由空格或者逗号分隔的一系列的值

示例：

```
$padding: 10px 20px 30px 40px;
$font:Arial,sans-serif,Helvetica;
.one{
    padding: $padding;
    font-family: $font;
}
```


编译成 CSS 代码：

```
.one {
  padding: 10px 20px 30px 40px;
  font-family: Arial, sans-serif, Helvetica;
}
```

列表中除了可以包含简单的值，还可以嵌套列表，例如下面这个列表就表示含有三个值，而不是四个值：

```
$list: 1, 2 100, 3;
```


等同于：

```
$list: 1, (2 100), 3;
```



### 3.7 Map

在 Sass 中，maps 类型表示映射类型。常以键值对（key/value）的形式出现

在定义映射时，整个映射必须通过小括号() 括起来，值与值之间使用逗号分隔

在 maps 中，一个给定的 key 只能有一个相关的 value，但一个给定的 value 可以被映射到许多不同的 key上

value 值可以是任何数据类型，包括 maps

示例：

```
$color-map: (color1: #fa0000, color2: #fbe200, color3: #95d7eb);
.one{
    color: map-get($color-map,color1);
    background-color: map-get($color-map, color2);
}
```

编译成 CSS 代码：

```
.one {
  color: #fa0000;
  background-color: #fbe200;
}
```

上述代码中，创建了一个名为 $color-map 的映射，这个映射中有三个键值对，分别为不同的 CSS 颜色值

其中 map-get 函数用于提供映射的值，可以接受两个参数，第一个参数为映射名称，第二个参数为需要取的 key 值



### 3.8 布尔值

booleans 类型为布尔类型，此类型只有两个值，即 true 和 false

在 Sass 中，只有当值为 false 或者 null 时，才会返回 false。其他的一切值都会返回 true 

支持与或非，and、or、not

示例：

```scss
.one{
    a:type-of(true);
    b:type-of(false);
    c:type-of(10);
    d:type-of(null);
}
```


编译成 CSS 代码：

```css
.one {
  a: bool;
  b: bool;
  c: number;
  d: null;
}
```



与

```
(5px > 3px) and (5px > 10px)
// false
```



或

```
(5px > 3px) or (5px > 10px)
// true
```



非

```
not(5px > 3px)
// false
not(5px < 3px)
// true
```



## 四、Sass函数



### 4.1 数字函数

常用的sass数字函数：

| 函数         | 描述                                     |
| ------------ | ---------------------------------------- |
| abs()        | 返回一个数值的绝对值                     |
| ceil()       | 向上取整                                 |
| floor()      | 向下取整                                 |
| comparable() | 返回一个布尔值，判断两个参数是否可以比较 |
| max()        | 返回最大值                               |
| min()        | 返回最小值                               |
| percentage() | 将数字转化为百分比的表达形式             |
| random()     | 返回 0-1 区间内的小数                    |
| round()      | 返回最接近该数的一个整数，四舍五入       |



#### abs()函数

`abs()` 函数用于返回一个数值的绝对值

示例：

```scss
.func {
    font-size: abs(-14px);
    padding: abs(10px);
}
```

编译成 CSS 代码：

```css
.func {
  font-size: 14px;
  padding: 10px;
}
```



#### ceil()函数

`ceil() ` 函数用于小数的向上取整，不用遵循四舍五入，例如 3.1 向上取整为 4

示例：

```scss
.func {
    width: ceil(10.1px);
    height: ceil(10.9px);
}
```

编译成 CSS 代码：

```css
.func {
  width: 11px;
  height: 11px;
}
```



#### floor()函数

`floor()` 函数的使用和 `ceil()` 函数差不多，但是 floor() 是用于向下取整

示例：

```scss
.func {
    width: floor(5.1px);
    height:floor(5.9px);
}
```

编译成 CSS 代码：

```css
.func {
  width: 5px;
  height: 5px;
}
```



#### comparable()函数

`comparable()` 函数判断两个参数是否可以进行比较，结果返回一个布尔值，如果可以进行比较则返回 true，否则返回 false。

示例：

```scss
.func {
    content1: comparable(10px, 20px);
    content2: comparable(10px, 20em);
    content3: comparable(10px, 20);
}
```

编译成 CSS 代码：

```css
.func {
  content1: true;
  content2: false;
  content3: true;
}
```

从编译后的 CSS 代码可以看出，不同单位的数值是不可以进行比较的，会返回 false。



#### max()/min()函数

max() 函数用于返回最大值，min() 函数用于返回最小值。

示例：

```scss
.max{
    content: max(1, 2, 10, 21, -19);
  }
.min{
    content: min(1, 2, 10, 21, -19);
}
```


编译成 CSS 代码：

```css
.max{
  content: -19;
}
.min{
  content: 21;
}
```



#### percentage() 函数

percentage() 函数用于将数字转化为百分比的表达形式。

示例：

```scss
.num{
    per1: percentage(28);
    per2: percentage(0.1);
}
```

编译成 CSS 代码：

```css
.num {
  per1: 2800%;
  per2: 10%;
}
```



#### random() 函数

random() 函数用于返回 0到1 区间内的小数 

函数中带有一个参数 number 时，返回 1 至 number 之间的整数，包括 1 和 limit。

示例：
例如获取 0 到 1 之间的五个随机数，可以使用 Sass 中的循环语句来实现：

```scss
@for $i from 1 through 5{
    .num#{$i} {
        width: random();
    }
}
```

编译成 CSS 代码：

```css
.num1 {
  width: 0.9782531648;
}

.num2 {
  width: 0.7659667301;
}

.num3 {
  width: 0.5846525783;
}

.num4 {
  width: 0.954587481;
}

.num5 {
  width: 0.7133921463;
}
```



如果我们想获取某个范围内的随机整数，可以在 random() 函数中指定一个参数。

如果我们想获取某个范围内的随机整数，可以在 random() 函数中指定一个参数。

示例：

例如生成1到10之间的一个随机数：

```scss
.num{
    width: random(10);
}
```

编译后的 CSS 代码：

```css
.num {
  width: 7;
}
```

可以看到在编译后的 CSS 代码中，生成的随机数为 7。如果我们再次执行编译命令，则又会重新生成一个随机数。



#### round()函数

round() 函数用于返回最接近该数的一个整数，四舍五入

示例：

```scss
.num{
    width: round(10.4px);
    height: round(39.6px);
}
```


编译后的 CSS 代码：

```css
.num {
  width: 10px;
  height: 40px;
}
```





### 4.2 字符串函数

Sass中的字符串函数用于处理字符串并获取相关信息

有一点需要注意，一般编程语言中字符串的索引都是从 0开始的，但Sass中字符串的索引是从 1 开始的

Sass 字符串函数如下所示：

| 函数          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| quote         | 给字符串添加引号                                             |
| unquote       | 移除字符串的引号                                             |
| str-length    | 返回字符串的长度                                             |
| str-index     | 返回 substring 子字符串第一次在 string 中出现的位置          |
| str-insert    | 在字符串 string 中指定索引位置插入内容                       |
| str-slice     | 从字符串中截取子字符串，允许设置始末位置，未指定结束索引值则默认截取到字符串末尾 |
| to-upper-case | 将字符串转成大写                                             |
| to-lower-case | 将字符串转成小写                                             |
| unique-id     | 返回一个无引号的随机字符串作为 id                            |



#### quote函数

quote 函数主要用来给字符串添加引号，如果字符串本身就带有引号，则会默认变为双引号

示例：

下面这个例子中，定义了两个变量，这两个变量的值都为字符串，其中一个没有带引号，一个带有单引号：

```scss
$str1: java;
$str2: 'python'; 
.func1{
    content: quote($str1);
}
.func2{
    content: quote($str2);
}
```

编译成 CSS 代码：

```css
.func1 {
  content: "java";
}
.func2 {
  content: "python";
}
```

使用 quote() 函数给上述两个字符串添加引号后，不管原来的字符串是带有单引号还是不带引号，最终两个字符串输出后都默认带有双引号



#### unquote函数

unquote 函数与 quote 函数功能相反，用于移除字符串所带的引号

示例：

```scss
$str1: "hello,xkd";
.func1{
    content: unquote($str1);
}
```

编译成 CSS 代码：

```css
.func1 {
  content: hello,xkd;
}
```

从输出的 CSS 代码可以看出，经过 unquote() 函数处理的字符串，所带的双引号会被移除


#### str-length函数

str-length 函数用于返回字符串的长度

示例：

```
.func{
    content: str-length("hello, xkd");
}
```

编译成 CSS 代码：

```
.func {
  content: 10;
}
```


从输出的 CSS 代码可以看出，字符串 hello,xkd 的长度为 10，这里需要注意，空格也占一个长度



#### str-index函数

str-index 函数用于返回 substring 子字符串第一次在 string 中出现的位置

其中 substring 和 string 都为函数参数。如果没有匹配到子字符串，则返回 null

示例：

```
.func{
    content1: str-index(hello, o);
    content2: str-index(abc, a);
    content3: str-index(kiki, i);
}
```

编译成 CSS 代码：

```
.func {
  content1: 5;
  content2: 1;
  content3: 2;
}
```

当查询字符串在字符串中出现多次时，例如 kiki 中 i 出现了两次，使用 str-index() 函数后会返回子字符串第一次出现时所在位置



#### str-insert 函数

str-insert 函数用于在字符串 string 中指定索引位置插入内容

第一个参数为字符串，第二个参数为要插入的内容，第三个参数为要插入的位置

示例：

例如要在 hello, 后面插入 xkd：

```
.func {
    content: str-insert("hello,", "xkd", 7);
}
```

编译成 CSS 代码：

```
.func {
  content: "hello,xkd";
}
```

上述代码中，因为 "hello," 字符串的长度为6，如果我们要在后面插入xkd，就要在 7 的位置插入



#### str-slice 函数

str-slice 函数用于从字符串中截取子字符串，允许设置开始和结束位置，当未指定结束索引值时，会默认截取到字符串末尾

示例：

```
.func {
    content: str-slice("abcdefg,", 1, 3);
}
```

编译成 CSS 代码：

```
.func {
  content: "abc";
}
```

上述代码中，截取字符串中1到3之间的子字符串，1表示截取字符串的开始位置，3表示截取字符串结束位置



#### to-[]-case 函数

to-upper-case 函数用于将字符串转成大写

to-lower-case 函数用于将字符串转成小写。

示例：

```
$str:"Hello, XKD";

.func {
    content1: to-upper-case($str);
    content2: to-lower-case($str);
}
```

编译成 CSS 代码：

```
.func {
  content1: "HELLO, XKD";
  content2: "hello, xkd";
}
```



#### unique-id函数

unique-id 函数返回一个无引号的随机字符串作为 id。

示例：

```
.func {
    content: unique-id();
}
```

编译成 CSS 代码：

```
.func {
  content: uo50mf1eb;
}
```



### 4.3 颜色函数

颜色函数可以分为三部分，分别是颜色设置、颜色获取以及颜色操作

Sass 中的颜色函数有很多，下面是一些 Sass 中常用的颜色函数：

| 函数       | 描述                                            |
| ---------- | ----------------------------------------------- |
| rgb()      | 创建一个 Red-Green-Blue（RGB） 色               |
| rgba()     | 创建一个带有透明度值的颜色                      |
| hsl()      | 通过色相、饱和度和亮度的值创建一个颜色          |
| hsla()     | 通过色相、饱和度、亮度和透明的值创建一个颜色    |
| red()      | 从一个颜色中获取其中红色值                      |
| lightness  | 获取一个颜色的亮度值(0% - 100%)                 |
| alpha      | 将颜色的 alpha 通道返回为介于 0 和 1 之间的数字 |
| opacity    | 获取颜色透明度值(0-1)                           |
| mix()      | 把两种颜色混合起来                              |
| fade-in()  | 降低颜色的透明度，取值在 0-1 之                 |
| fade-out() | 提升颜色的透明度，取值在 0-1 之间               |



#### rgb()函数

rgb() 函数创建一个 Red-Green-Blue（RGB） 色，其中 R 表示红色，G表示绿色，B表示蓝色。RGB的取值范围在 0 到 255 之间

示例：

```scss
.xkd{
    background: rgb(240, 236, 122);
    color: rgb(15, 88, 96);
}
```

编译成 CSS 代码：

```css
.xkd {
  background: #f0ec7a;
  color: #0f5860;
}
```

需要注意的是 rgb() 函数中的参数值范围在 0 到 255 之前，不能超过 255，否则会失效



#### rbga()函数

rbga() 函数的使用和 rgb() 函数差不多，都是用于创建颜色

但是 rgba() 中多了一个 alpha，也就是颜色透明度

颜色透明度的取值范围为 0 到 1 之间的小数，例如 0.1、0.2 0.3 等， 值越小颜色越透明

示例：

例如我们给一个黑色设置透明度为 0.6：

```scss
.xkd{
    background: rgba(0, 0, 0, 0.6);
    color: rgb(0, 0, 0);
}
```

编译成 CSS 代码：

```css
.xkd {
  background: rgba(0, 0, 0, 0.6);
  color: black;
}
```



#### hsl()函数

hsl() 函数可以通过色相（hue）、饱和度(saturation)和亮度（lightness）的值创建一个颜色

示例：

```scss
.xkd{
    color: hsl(100, 100%, 60%);
    a{
        color: hsl(255, 80%, 70%);
    }
}
```

编译成 CSS 代码：

```css
.xkd {
  color: #77ff33;
}
.xkd a {
  color: #9475f0;
}
```



#### hsla()函数

hsla() 函数可以通过色相（hue）、饱和度(saturation)、亮度（lightness）和透明（alpha）的值创建一个颜色

示例：

```scss
.xkd{
    color: hsla(100, 100%, 60%, 0.8);
    a{
        color: hsla(255, 80%, 70%, 0.3);
    }
}
```

编译成 CSS 代码：

```css
.xkd {
  color: rgba(119, 255, 51, 0.8);
}
.xkd a {
  color: rgba(148, 117, 240, 0.3);
}
```



#### red()函数

red() 函数用于从一个颜色中获取其中红色值，取值范围为 0 到 255

除了 red() 函数，还有 green() 函数和 blue() 函数

示例：

例如获取一个颜色中的红色值、绿色值、蓝色值：

```scss
.xkd{
    content: red(#fecefc);
    content: green(#fecefc);
    content: blue(#fecefc);
}
```


编译成 CSS 代码：

```css
.xkd {
  content: 254;
  content: 206;
  content: 252;
}
```

上述代码中，red() 函数用于从一个颜色中获取红色值，同理，green() 函数用于获取绿色值，blue() 函数用于获取蓝色值

我们可以试一下在 rgb() 函数中使用这三个获取到的数值，看看创建的颜色是否同 #fecefc 一样：

```
rgb(254, 206, 252)
```



#### lightness()函数

lightness() 函数获取一个颜色的亮度值，取值范围为0% 到 100%

示例：

例如获取不同颜色值的亮度：

```scss
.xkd{
    content:lightness(#cccccc);
    content:lightness(#ff0000);
}
```

编译成 CSS 代码：

```css
.xkd {
  content: 80%;
  content: 50%;
}
```

根据输出结果可以看出，#cccccc 颜色的亮度为 80%，#ff0000 的亮度为 50% 



#### alpha()函数

alpha() 函数将颜色的 alpha 通道返回为介于 0 和 1 之间的数字

示例：

```scss
.xkd{
    content:alpha(pink);
    content:alpha(rgba(125, 125, 125, 0.6));
}

```

编译成 CSS 代码：

```css
.xkd {
  content: 1;
  content: 0.6;
}
```



#### opacity()函数

opacity() 函数用于获取颜色透明度值，取值范围在 0 到 1 之间

示例：

```scss
.xkd{
    content:opacity(rgba(212, 234, 124, 0.1));
    content: opacity(red);
}
```

编译成 CSS 代码：

```css
.xkd {
  content: 0.1;
  content: 1;
}
```



#### mix()函数

mix() 函数用于将两种颜色混合起来，可以组成一个新的颜色值

示例：

例如我们将蓝色和绿色混合起来：

```scss
.xkd{
    content:mix(blue, green);
}
```


编译成 CSS 代码：

```css
.xkd {
  content: #004080;
}
```

编译后，组成了一个新的颜色 #004080



#### fade-in()函数

fade-in() 函数降低颜色的透明度，取值在 0 到 1 之间

示例：

```scss
.xkd{
    content:fade-in(rgba(100, 100, 255, 0.7), 0.1);
}
```

编译成 CSS 代码：

```css
.xkd {
  content: rgba(100, 100, 255, 0.8);
}
```


可以看到，编译后的代码中，透明度由原来的 0.7 变为了 0.8。因为值越小透明度越高，反之值越大，透明度越低



#### fade-out()函数

fade-out() 函数提升颜色的透明度，取值在 0 到 1 之间

示例：

```scss
.xkd{
    content:fade-out(rgba(100, 100, 255, 0.7), 0.1);
}
```

编译成 CSS 代码：

```css
.xkd {
  content: rgba(100, 100, 255, 0.6);
}
```



### 4.4 HSL函数

| 函数                                     | 描述                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| hsl($hue,$saturation,$lightness)         | 通过色相（hue）、饱和度(saturation)和亮度（lightness）的值创建一个颜色 |
| hsla($hue,$saturation,$lightness,$alpha) | 上述添加透明度                                               |
| hue($color)                              | 从一个颜色中获取色相（hue）值                                |
| saturation($color)                       | 从一个颜色中获取饱和度（saturation）值                       |
| lightness($color)                        | 从一个颜色中获取亮度（lightness）值                          |
| adjust-hue($color,$degrees)              | 通过改变一个颜色的色相值，创建一个新的颜色                   |
| lighten($color,$amount)                  | 通过改变颜色的亮度值，让颜色变亮，创建一个新的颜色           |
| darken($color,$amount)                   | 通过改变颜色的亮度值，让颜色变暗，创建一个新的颜色           |
| saturate($color,$amount)                 | 通过改变颜色的饱和度值，让颜色更饱和，从而创建一个新的颜色   |
| desaturate($color,$amount)               | 通过改变颜色的饱和度值，让颜色更少的饱和，从而创建出一个新的颜色 |
| grayscale($color)                        | 将一个颜色变成灰色，相当于desaturate($color,100%)            |
| complement($color)                       | 返回一个补充色，相当于adjust-hue($color,180deg)              |
| invert($color)                           | 反回一个反相色，红、绿、蓝色值倒过来，而透明度不变           |



在命令行中做简单的测试

```
>> hsl(200,30%,60%) //通过h200,s30%，l60%创建一个颜色
#7aa3b8
 

>> hsla(200,30%,60%,.8)//通过h200,s30%，l60%,a80%创建一个颜色
rgba(122, 163, 184, 0.8)
 

>> hue(#7ab)//得到#7ab颜色的色相值
195deg
 

>> saturation(#7ab)//得到#7ab颜色的饱和度值
33.33333%
 

>> lightness(#7ab)//得到#7ab颜色的亮度值
60%
 

>> adjust-hue(#f36,150deg) //改变#f36颜色的色相值为150deg
#33ff66
 

>> lighten(#f36,50%) //把#f36颜色亮度提高50%
#ffffff
 

>> darken(#f36,50%) //把#f36颜色亮度降低50%
#33000d
 

>> saturate(#f36,50%) //把#f36颜色饱和度提高50%
#ff3366
 

>> desaturate(#f36,50%) //把#f36颜色饱和度降低50%
#cc667f
 

>> grayscale(#f36) //把#f36颜色变成灰色
#999999
 

>> complement(#f36)
#33ffcc
 

>> invert(#f36)
#00cc99
```



note：

- 在 HSL 函数中，hsl() 和 hsla() 函数主要是通过颜色的 H、S、L 或者 A 几个参数获取一个 rgb 或 rgba 表达的颜色
- 这两个函数与 CSS 中的无太大区别，只是使用这两个函数能帮助您知道颜色的十六进制表达式和 rgba 表达式
- 而 hue()、saturation() 和 lightness() 函数主要是用来获取指定颜色中的色相值、饱和度和亮度值

- HSL 函数中最常见的应该是 lighten()、darken()、saturate()、desaturate()、grayscale()、complement()和 invert() 几个函数



### 4.5 列表函数

函数	描述
append()	将单个值添加到列表尾部
index()	返回元素在列表中的索引
length()	返回列表的长度
is-bracketed()	判断列表中是否有中括号
join()	合并两列表，
list-separator()	返回一列表的分隔符类型，可以是空格
nth()	获取第 n 项的值
set-nth()	设置列表第 n 项的值为 value
zip()	将多个列表按照以相同索引值为一组，重新组成一个新的多维度列表



| 函数             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| append()         | 将单个值添加到列表尾部                                       |
| index()          | 返回元素在列表中的索引                                       |
| length()         | 返回列表的长度                                               |
| is-bracketed()   | 判断列表中是否有中括号                                       |
| join()           | 合并两列表                                                   |
| list-separator() | 返回一列表的分隔符类型，可以是空格                           |
| nth()            | 获取第 n 项的值                                              |
| set-nth()        | 设置列表第 n 项的值为 value                                  |
| zip()            | 将多个列表按照以相同索引值为一组，重新组成一个新的多维度列表 |



#### append()函数

append() 函数可以用于向列表中添加一个新的元素，此函数的语法如下所示：

```
append(list, value, [separator])
```

其中 list 为列表、value 为要新增的元素值，separator 是可选参数，可以指定分隔符，值为comma 表示使用逗号分隔列表

示例：

```
.one{
    content: append((Tom Mark), XKD);
}
.two{
    content: append((a b c), d, comma);  // 使用逗号分隔列表
}
```

编译成 CSS 代码：

```
.one {
  content: Tom Mark XKD;
}

.two {
  content: a, b, c, d;
}
```

可以看到，在上述两个选择器中，.one 中没有指定第三个参数，输出的代码中是以空格分隔列表

而 .two 中给列表添加元素时带有第三个参数 comma，所以输出的 CSS 代码中是以逗号分隔列表



#### index()函数

index() 函数可以用于返回元素在列表中的索引，注意哟，Sass 中的索引是从 1 开始的。

示例：

例如我们定义一个列表 $lst，然后分别获取列表中 a 和 d 两个值的索引：

```
$lst:a b c d e;
.one{
    content: index($lst, a);
}
.two{
    content: index($lst, d);
}
```

编译成 CSS 代码：

```
.one {
  content: 1;
}

.two {
  content: 4;
}
```

从输出代码中可以看到， a 的索引为 1， d 的索引为 4



#### length()函数

length() 函数可以获取列表的长度

示例：

例如我们定义两个列表，分别获取两个列表的长度：

```
$lst1:a b c d e;
$lst2:10 15 21 36 17 6 18;
.one{
    content: length($lst1);
}
.two{
    content: length($lst2);
}
```

编译成 CSS 代码：

```
.one {
  content: 5;
}

.two {
  content: 7;
}
```

从输出的 CSS 代码中可以看到 $lst1 的长度为 5，$lst2 的长度为7

其实获取长度很简单，就是列表中有多少个元素，列表的长度就为几



#### is-bracketed()函数

is-bracketed() 函数用于判断列表中是否有中括号。如果有中括号则返回 true，如果没有中括号则返回 false

示例：

```
.one{
    content: is-bracketed([a b c]);
}
.two{
    content: is-bracketed(xkd summer iven);
}
```

编译成 CSS 代码：

```
.one {
  content: true;
}

.two {
  content: false;
}
```

结果很明显，.one 选择器内带有中括号的列表返回的是 true，.two 内没有中括号的列表返回 false。



#### join()函数

join() 函数用于合并两个列表。函数中带有四个参数，前面个参数为要合并的列表，将第二个参数添加到第二个参数末尾

后两个是可选参数，第三个参数为指定分隔符，第四个参数为判断是否有中括号，可以设置为 true 或 false 两个值

示例：

```
$lst1: a b c;
$lst2: 1 2 3;

.one{
    content: join($lst1, $lst2, comma);
}
.two{
    content: join($lst1, $lst2);
}
```

编译成 CSS 代码：

```
.one {
  content: a, b, c, 1, 2, 3;
}

.two {
  content: a b c 1 2 3;
}
```



#### list-separator() 函数

list-separator() 函数用于返回列表的分隔符类型，可以是逗号或者空格

示例：

```
$lst1: a b c;
$lst2: 1,2,3;

.one{
    content: list-separator($lst1);
}
.two{
    content: list-separator($lst2);
}
```

编译成 CSS 代码：

```
.one {
  content: space;
}

.two {
  content: comma;
}
```

从输出的 CSS 代码中可以看出，列表 $lst1 中的分隔符类型为空格，$lst2 中的分隔符类型为列表



#### nth() 函数

nth() 函数用于获取列表中指定索引的值

示例：

```
$lst1: a b c;
$lst2: 1,2,3;

.one{
    content: nth($lst1, 2);
}
.two{
    content: nth($lst2, 2);
}

```

编译成 CSS 代码：

```
.one {
  content: b;
}

.two {
  content: 2;
}
```

$lst1 中第二项列表的值为 b，$lst2 中第二项列表的值为 2



#### set-nth()函数

set-nth() 函数用于设置列表中指定索引的值。将会覆盖原有元素的值

示例：

例如设置列表中索引为 3 位置的值为 xkd：

```
.one{
    content: set-nth([a b c], 3, xkd);
}
```

编译后的 CSS 代码：

```
.one {
  content: [a b xkd];
}
```

可以看到输出结果中，xkd 覆盖了原本的元素值 c



#### zip()函数

zip() 函数用于将多个列表按照以相同索引值为一组，重新组成一个新的多维度列表

示例：

```
.one{
    border:zip(1px 2px 3px,solid dashed dotted,red yellow blue);
}
```


编译后的 CSS 代码：

```
.one {
  border: 1px solid red, 2px dashed yellow, 3px dotted blue;
}
```





### 4.6 Map函数

前面介绍了使用 map 来管理变量，但要在 Sass 中获取变量，或者对 map 做更多有意义的操作

我们必须借助于 map 的函数功能。在 Sass 中 map 自身带了七个函数：

- **map-get($map,$key)**：根据给定的 key 值，返回 map 中相关的值。
- **map-merge($map1,$map2)**：将两个 map 合并成一个新的 map。
- **map-remove($map,$key)**：从 map 中删除一个 key，返回一个新 map。
- **map-keys($map)**：返回 map 中所有的 key。
- **map-values($map)**：返回 map 中所有的 value。
- **map-has-key($map,$key)**：根据给定的 key 值判断 map 是否有对应的 value 值，如果有返回 true，否则返回 false。
- **keywords($args)**：返回一个函数的参数，这个参数可以动态的设置 key 和 value。



## 五、sass控制指令

控制指令主要有：@if 、@for 、@while 、@each 四种

控制指令是一种高级功能， 主要与混合指令（mixin）配合使用 

尤其是在 Compass 库中 



### 5.1 @if

@if 跟 if 条件语句一样，也可以跟多个 @else if ，用返回值来判断输出的代码

当返回值为 true 时候输出后面 { } 中的代码

当返回值是 false 时，表示该条件不成立，将逐条执行 @else if 声明

如果全部不成立，最后执行 @else 声明 

例如：

```scss
$name: cmy
p {
    @if $name == c {
     color : red ;
　　} @else if $name == m {
　　　color : blue ;
　　} @else if $name == y {
　　　color : green ;
　　} @else if $name == cmy {
　　　color : gold ;
　　}@else {
　　　color : yellow ;
　　}
}     

// 编译为：
p {    
    color : gold ;
} 
```



### 5.2 @for

在Sass的 @for 循环中有两种方式：

- @for $cmy from <start> through <end>
- @for $cmy from <start> to <end>

```scss
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}

// 编译为:

.item-1 {
  width: 2em;
}
.item-2 {
  width: 4em;
}
.item-3 {
  width: 6em;
}
```

```scss
@for $i from 1 to 3 {
  .item-#{$i} { width: 2em * $i; }
}
 
// 编译为:
 
.item-1 {
  width: 2em;
}
.item-2 {
  width: 4em;
}
```



### 5.3 @while

@while 指令重复输出格式直到表达式返回结果为 false 

这个和 @for 指令很相似，只要 @while 后面的结果为 true 就会执行

```scss
$i:4;    //变量赋值用 ： 而不是想js一样用 =
$i_width:100px;
@while $i>0 {
    .item-#{$i}{ width:$i_width+$i}
    $i:$i-1;
}
 
// 编译为：
.item-1{
    width:104px;
}
.item-2{　　
    width:103px;
}
.item-3{    
    width:102px;
}
.item-4{　　
    width:101px;
}
```



### 5.4 @each

@each 指令就是便利一个值列表，然后将变量作用于值列表中每一个项目，输出结果

```scss
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}
 
// 编译后：
 
.puma-icon {
  background-image: url('/images/puma.png'); 
}
.sea-slug-icon {
  background-image: url('/images/sea-slug.png'); 
}
.egret-icon {
  background-image: url('/images/egret.png'); 
}
.salamander-icon {
  background-image: url('/images/salamander.png');
}
```



























