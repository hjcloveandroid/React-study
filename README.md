# React-study

> React：

https://react-cn.github.io/react/docs/tutorial.html

https://zh-hans.reactjs.org/tutorial/tutorial.html

https://reactjs.org/docs/getting-started.html


------KaiOS react study-------

yarn global add create-kai-app </br>
yarn create kai-app kai-app </br>
yarn start    </br>// 如果没有启动浏览器就直接手动输入： http://localhost:3000/
:~/kai-app$ yarn build
yarn push

如果yarn install

ES6 study:
各大浏览器的最新版本,对 ES6 的支持可以查看 kangax.github.io/es5-compat-table/es6/

## Babel

>Babel is a JavaScript compiler. 

转码器 :https://babeljs.io/


Babel 是一个广泛使用的 ES6 转码器,可以将 ES6 代码转为 ES5 代码,从而在现有环境执行。这意味着,你可以用 ES6 的方式编写程序,又不用担心现有环境是否支持。
下面是一个例子。

```
// 转码前
input.map(item => item + 1);
// 转码后
input.map(function(item) {
     return item + 1
})
```
Babel 提供一个 REPL 在线编译器,可以在线将 ES6 代码转为 ES5 代码。转换后的代码,可以直接作为 ES5 代码插入网页运行
NODEjs
https://nodejs.org/en/

Node.js 是 JavaScript 语言的服务器运行环境,对 ES6 的支持度比浏览器更高。通过 Node ,可以体验更多 ES6 的特性。建议使用版本管理工具 nvm ,来安
装 Node ,因为可以自由切换版本。

ESLint 用于静态检查代码的语法和风格

Mocha 则是一个测试框架,如果需要执行使用 ES6 语法的测试脚本,可以修改package.json 的scripts.test

Traceur 转码器 ()
Google 公司的 Traceur 转码器,也可以将 ES6 代码转为 ES5 代码。
Traceur 允许将 ES6 代码直接插入网页。首先,必须在网页头部加载 Traceur 库文件。
<script src="https://google.github.io/traceur-compiler/bin/traceur.js"></script>
<script src="https://google.github.io/traceur-compiler/bin/BrowserSystem.js"></script>
<script src="https://google.github.io/traceur-compiler/src/bootstrap.js"></script>
<script type="module"> 
import './Greeter.js';</script>
上面代码中,一共有 4 个script 标签:
第一个是加载 Traceur 的库文件,
第二个和第三个是将这个库文件用于浏览器环境,
第四个则是加载用户脚本,
这个脚本里面可以使用 ES6 代码。
注意,第四个script 标签的type 属性的值是module ,而不是text/javascript 。这是 Traceur 编译器识别 ES6 代码的标志,编译器会自动将所有type=module 的代码编译为 ES5 ,然后再交给浏览器执行

## 2 let 和 const 命令
作用域（代码块）
```
for(vari=0;i<arr.length;i++)  
vs 
for(let i=0;i<arr.length;i++)
```
### 变量提升

在代码块内,使用 let 命令声明变量之前,该变量都是不可用的。这在语法上,称为 “ 暂时性死区 ” ( temporal dead zone ,简称 TDZ )
“ 暂时性死区 ” 也意味着typeof 不再是一个百分之百安全的操作。
typeof x; // ReferenceError
let x;

### 2.2 块级作用域

>块级作用域的出现,实际上使得获得广泛应用的立即执行匿名函数( IIFE )不再必要了。

IIFE 写法块级作用域写法: 
```
(function () {
    var tmp = ...;
    ...
}());
{
    let tmp = ...;
    ...
}

// ES6 严格模式
'use strict';
if (true) {
    function f() {}
}
// 不报错
```
并且 ES6 规定,块级作用域之中,函数声明语句的行为类似于let ,在块级作用域之外不可引用。
const 的作用域与let 命令相同:只在声明所在的块级作用域内有效。
如果真的想将对象冻结,应该使用Object.freeze 方法。
const foo = Object.freeze({});
// 常规模式时,下面一行不起作用;
// 严格模式时,该行会报错
foo.prop = 123;
上面代码中,常量foo 指向一个冻结的对象,所以添加新属性不起作用,严格模式时还会报错。

ES5 只有两种声明变量的方法:var 命令和function 命令。 ES6 除了添加let 和const 命令,后面章节还会提到,另外两种声明变量的方法:import 命令和class 命令。所以, ES6 一共有 6 种声明变量的方法。
除此之外,你甚至可以使用标签模板,在 JavaScript 语言之中嵌入其他语言。
>jsx语法
```
<div>
    <input 
        ref='input' 
        onChange='${this.handleChange}' 
        defaultValue='${this.state.value}' 
    />
    ${this.state.value}
</div>
```
## 7 数组的扩展

> **Array.from**
```
let arrayLike = {
    '0': 'a','1': 'b','2': 'c',
    length: 3
};
ES5 的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']
ES6 的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

分类|例子
--|--
匿名函数|具名函数
var func1 = function () {};|const func1 = function baz() {};
ES5| ES6
func1.name // ""|func1.name // "func1"
const func1 = function baz() {};

// ES5
bar.name // "baz"
// ES6
bar.name // "baz"

## call、apply和bind方法的用法以及区别
>call、apply、bind的作用是改变函数运行时this的指向，所以先说清楚this。
以下是函数的调用方法：


### 方法调用模式

当一个函数被保存为对象的一个方法时
```
    var a = 1
    var obj1 = {
      a:2,
      fn:function(){
        console.log(this.a)
      }
    }
    obj1.fn()//2  
    document.addEventListener('click', function(e){
        console.log(this);
        setTimeout(function(){
            console.log(this);
        }, 200);
    }, false);
```
此时的this是指obj1这个对象，obj1.fn()实际上是obj1.fn.call(obj1)，事实上谁调用这个函数，this就是谁点击页面，依次输出：document和window对象
---
## 函数调用模式

>## 最普通的函数调用
就是普通函数的调用，此时的this被绑定到window
```
function fn1(){
      console.log(this)//window
    }
fn1()
    // 1. 函数嵌套
function fn1(){
    function fn2(){
        console.log(this)//window
    }
    fn2()
}
fn1()
    // 1. 把函数赋值之后再调用
var a = 1
var obj1 = {
    a:2,
    fn:function(){
        console.log(this.a)
    }
}
var fn1 = obj1.fn;
fn1();//打印出1  如果需要打印2，怎么修改？fn1.call(obj1);
    //1. 回调函数
var a = 1
function f1(fn){
    fn()
    console.log(a)//1
}
f1(f2)

function f2(){
    var a = 2
}

var a = 1
function f1(){
    (function (){var a = 2})()
    console.log(a)//1
}
f1()
```
>## 构造器调用模式:
### new()
new一个函数时，背地里会将创建一个连接到prototype成员的新对象，同时this会被绑定到那个新对象上
```
function Person(name,age){
// 这里的this都指向实例
    this.name = name
    this.age = age
    this.sayAge = function(){
        console.log(this.age)
    }
}

var dot = new Person('Dot',2)
dot.sayAge()//2
```
### call()

call 方法第一个参数是要绑定给this的值，后面传入的是一个参数列表。当第一个参数为null、undefined的时候，默认指向window。
```
var arr = [1, 2, 3, 89, 46]
var max = Math.max.call(null, arr[0], arr[1], arr[2], arr[3], arr[4])//89
var max = Math.max.call(null, ...arr)//89
//可以这么理解：
obj1.fn() --->obj1.fn.call(obj1);
fn1()--->fn1.call(null)
f1(f2)--->f1.call(null,f2)
var obj = {
    message: 'My name is'
}

function getName(firstName, lastName) {
    console.log(this.message + “: ”+firstName + ' ' + lastName)
}
getName('Dot', 'Dolby')
getName.call(obj, 'Dot', 'Dolby')
------------------------------------------------------
Print:
undefined: Dot Dolby
My name is: Dot Dolby
```
### apply()

apply接受两个参数，第一个参数是要绑定给this的值，第二个参数是一个参数数组。当第一个参数为null、undefined的时候，默认指向window。
```
var arr = [1,2,3,89,46]
var max = Math.max.apply(null,arr)//89
obj1.fn() --->obj1.fn.apply(obj1);
fn1() --→ fn1.apply(null)
f1(f2) --→ f1.apply(null,f2)
getName('Dot', 'Dolby')
getName.apply(obj, ['Dot', 'Dolby'])
Print:
undefined: Dot Dolby
My name is: Dot Dolby
```
是不是觉得和前面写的call用法很像，事实上apply 和 call 的用法几乎相同, 
apply vs call 唯一的差别在于：当函数需要传递多个变量时, apply 可以接受一个数组作为参数输入, call 则是接受一系列的单独变量。

### Bind() 

bind返回值是函数
和call很相似，第一个参数是this的指向，从第二个参数开始是接收的参数列表。区别在于bind方法返回值是函数以及bind接收的参数列表的使用。
```
var obj = {
    name: 'Dot'
}

function printName() {
    console.log(this.name)
}

var dot = printName.bind(obj)
console.log(dot) // function () { … }
dot()  // Dot
Print:
function () { … }
Dot
```

说明：bind 方法不会立即执行，而是返回一个改变了上下文 this 后的函数。而原函数 printName 中的 this 并没有被改变，依旧指向全局对象 window。
---


## 一、使用 JXS 报错
>Uncaught SyntaxError: Unexpected token <

原因：凡是在页面中直接使用 JSX 的地方,都要加上 type="text/babel"，在引用 JS 文件的地方加上 type="text/babel"
## 二、表达式引号
>Minified React error #94;
```
// 错误
<h1 onClick="{this.handleClickOnTitle}">React</h1>
// 正确
<h1 onClick={this.handleClickOnTitle}>React</h1>

{}表达式不需要引号括起来
```
## 三、static defaultProps
```
static defaultProps = {
    likedText: '取消',
    unlikedText: '点赞'
}
```
//由于是用ES6 class语法创建组件，其内部只允许定义方法，而不能定义属性，class的属性只能定义在class之外。所以defaultProps要写在**组件外部**
```
LikeButton.defaultProps = {
        likedText: '取消',
        unlikedText: '点赞'
    }
```
## 四、代码书写不对
 >Uncaught TypeError: Super expression must either be null or a function, not undefined

这个错误一般是 某个地方书写不对 例如：React.component     //  首字母应该大写
## 五、输入值属性

Failed prop type: You provided a `value` prop to a form field without an `onChange` handler. This will render a read-only field. If the field should be mutable use `defaultValue`. Otherwise, set either `onChange` or `readOnly`
---
>原因：在输入上设置了一个值属性，但是不提供任何处理程序来更新它
1. 设置默认值--defaultValue
2. 设置只读--readOnly
3. 设置更改函数--onChange

## 六、table属性
```
Warning: validateDOMNesting(...): <tr> cannot appear as a child of <table>

原因：在React中<tr>元素不可以作为<table>元素的直接子元素
解决方法：加入thead/tbody即可
```
## 七、遍历数组元素
>Warning:Each child in an array or iterator should have a unique "key" prop

原因：在React中数组遍历返回元素或组件时需加上key属性作为唯一标识
解决：
```
address.map((item, index) => {
    return (
        <ul class="items">
            <li class="item" key={index}>{item}</li>
        </ul>
    )
});
```
## 八、constructor无法使用this.props

super(props)的目的：在constructor中可以使用this.props

## 九、react中父级props改变，更新子级state

原因：父组件传递给子组件的props发生改变时，state不会自动更新，并没有执行子组件的constructor函数,同时引发子组件的render，子组件的this.props的值也是从render函数开始执行的时候开始更新的，render之前生命周期函数中都是获取不到最新的this.props的.子组件没有被卸载自然不会重新加载，只会重新render,我们需要重新处理下，将props转换成自己的state，使用componentWillReceiveProps(nextProps)
父组件的props传递给子组件的state只会在第一次加载的时候被赋值，后续的父组件props变化并不会被赋值到子组件的state上

## 十、react router BrowserRouter 的坑
```
1、刷新非首页出现Cannot get Page
原因：自身的特性
解决：
devServer: {
   historyApiFallback: true,
}

//第二种方法
BrowserRouter 改为 HashRouter
2、打包后绝对路径有问题
需要服务端配置或改为HashRouter
```

------------------------------------------------------------------



# Introducing Web Activities
Getting started with Web Activities
There are a few ways you can work with Web Activities:
1. Call an activity and get presented with apps that can handle that 
2. Register your activity support for your web app in the manifest file 
3. Register activity support on-the-fly 
4. Attach a handler to your app for when that activity occurs 


Caller|Callee
--|--
Calling an activity|Register your app for an activity
Handling the response|







## Calling an activity
Let’s say you have a button in your app, and you want to be able to get a picture – either from the Gallery, Camera or any other app in Firefox OS that supports that activity. You can then call the pick activity, like this:
```
var pick = new MozActivity({
   name: "pick",
   data: {
       type: ["image/png", "image/jpg", "image/jpeg"]
   }
});
```
As a user, you choose the app you want to pick an image from – or take a picture with the Camera – and once you’ve done so, the result will be posted back to the requesting app


## Handling the response
or most WebAPIs, including Web Activities, you will have onsuccess and onerror event handlers. In the case of an image/file you will get a blob back. You can then represent that returned image visually directly in your app:
```
pick.onsuccess = function () {
    // Create image and set the returned blob as the src
    var img = document.createElement("img");
    img.src = window.URL.createObjectURL(this.result.blob);
 
    // Present that image in your app
    var imagePresenter = document.querySelector("#image-presenter");
    imagePresenter.appendChild(img);
};
 
pick.onerror = function () {
    // If an error occurred or the user canceled the activity
    alert("Can't view the image!");
};
```
## Register your app for an activity

As mentioned above, you can also set your app as a handler for certain activities. There are two ways to do that:
Through the manifest file – declaration registration
```
{
    "name": "My App",
    "description": "Doing stuff",
    "activities": {
       "view": {
            "filters": {
                "type": "url",
                "url": {
                    "required": true,
                    "regexp":"/^https?:/"
                }
            }
        }
    }
}
```
## Register an activity handler – dynamic registration
```
var register = navigator.mozRegisterActivityHandler({
    name: "view",
    disposition: "inline",
    filters: {
        type: "image/png"
    }
});
 
register.onerror = function () {
    console.log("Failed to register activity");
}
```
### and then handle the activity:
```
navigator.mozSetMessageHandler("activity", function (a) {
    var img = getImageObject();
    img.src = a.source.url;
    /*
      Call a.postResult() or a.postError() if
      the activity should return a value
    */
});
```
>## Available activities
The available activities to choose from at this time are:
```
    • configure 
    • costcontrol/balance 
    • costcontrol/data_usage 
    • costcontrol/telephony 
    • dial 
    • new(e.g.type:“websms/sms”,“webcontacts/contact”) 
    • open 
    • pick (e.g. type: “image/png”) 
    • record 
    • save-bookmark 
    • share 
    • test 
    • view 
```
A few examples:
>## Dial
```
var call = new MozActivity({
    name: "dial",
    data: {
        number: "+46777888999"
    }
});
```
>## New SMS
```
var sms = new MozActivity({
    name: "new",
    data: {
        type: "websms/sms",
        number: "+46777888999"
    }
});
```
>## New Contact
```
var newContact = new MozActivity({
    name: "new",
    data: {
        type: "webcontacts/contact",
        params: { // Will possibly move to be direct properties under "data"
            giveName: "Robert",
            familyName: "Nyman",
            tel: "+44789",
            email: "robert@mozilla.com",
            address: "Sweden",
            note: "This is a note",
            company: "Mozilla"
        }
    }
});
```
>## View URL
```
var openURL = new MozActivity({
    name: "view",
    data: {
        type: "url", // Possibly text/html in future versions
        url: "http://robertnyman.com"
    }
});
```
>## Save bookmark
```
var savingBookmark = new MozActivity({
    name: "save-bookmark",
    data: {
        type: "url",
        url: "http://robertnyman.com",
        name: "Robert's talk",
        icon: "http://robertnyman.com/favicon.png"
    }
});
```
