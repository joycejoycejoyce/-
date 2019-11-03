# JavaScript 的练习题看这里

## 异步编程方案
JavaScript 语言的执行环境是“单线程” （single thread）
所谓"single thread" 就是一个只能完成一个任务。如有多个任务，必须排队。
这种模式的好处是实现起来比较简单。执行环境相对单纯。坏处是只要有一个任务耗时很长，后面的任务都必须排队等着。
常见的问题就是浏览器无响应（假死），往往就是某一段代码长时间运行，导致页面卡在这个地方，其他任务无法执行。

为了解决这个问题，JS 语言讲任务的执行分成了两种： 同步 （synchronous） 和 异步 (Asynchronous)
所有的长耗时的任务都应该使用异步执行。
在服务器端，“异步模式”是唯一的模式。因为执行环境是单线程的，如果允许同步执行所有http请求，服务器性能会急剧的下降，
很快就会失去响应。
异步编程的核心是现在运行的部分和未来运行的部分之间的关系
`
  now 
    |    
    |   This gap is the core of asynchronism  
    |
  future

`

### 分块的程序
### 事件循环
### 并行线程
### 并发
#### 非交互
#### 交互 
#### 协作
### 任务
### 语句顺序 



### 方案
1. callback function 
2. event listening 
3. public / subscribe 
4. Promise 对象
### 回调函数

### Promise 
promise 相当于一个状态机
promise 的三种状态
* pending 
* fulfilled, 当调用resolve function 
* rejected, 当调用 rejected function 
promise状态只能由pending -> fulfilled / rejected 一旦修改就不能再变

`
按照顺序写出下列console的值
const pro = new Promise((resolve, reject)=>{
    const innerpro = new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(1);
        }, 0);
        console.log(2);
        resolve(3);
    });
    innerpro.then(res=>console.log(res));
    resolve(4);
    console.log("pro");
})
pro.then(res=>console.log(res));
console.log("end"); 


`

## Axios 
Axios 是一个基于Promise 的HTTP库，可以用于Browser和 node.js里面

### 

## 跨域问题 jsonp
### jsonp 的概念
jsonp 是解决跨域问题的办法之一。原理在于虽然我们由于同源策略不能够从另外的domain上请求file，可是我们可以请求script.  
JSONP 就是利用了这个特点，所以它并不使用XMLHTTPRequest 而是使用了 `<script>` 标签.  
使用JSONP的原理是： 
1. 利用script 标签的src 属性实现跨域
2. 通过将前端方法作为参数传递到服务器端，然后由服务器端注入参数后再返回，实现服务器端向客户端通信
3. 使用script标签的src属性，因此只支持get方法

## Promise 
Promise 算是面试题只重的重中之重了，不管是谁家的面试都问过关于Promise 的题目。
## 概念
Promise 是做异步的标准用法。它接受一个函数作为参数，并且返回promise 对象。为链式调用提供基础。  

Promise 共有三种状态
1. pending: 初始状态
2. fulfilled: 意味着异步操作的结果为失败 
3. rejected: 意味着异步操作的结果为失败

## JS 的6个假值
概念：
1. false 
2. null
3. NaN
4. undefined
5. ""
6. 0 

题目： 
---
`
var test=new Boolean();
document.write(test);
document.write("<br />");

var test=new Boolean(0);
document.write(test);
document.write("<br />");

var test=new Boolean(null);
document.write(test);
document.write("<br />");

var test=new Boolean("");
document.write(test);
document.write("<br />");

var test=new Boolean(NaN);
document.write(test);
document.write("<br />");

`
上述代码的输出结果为（      ）  

false false false false false  

false true false false false  

false false true test Boolean  

--- 

## 什么是默认行为
概念： 
默认行为就是比如一个当一个form的submit button被点击时它会自动的向后端发送数据
但是其实我们不想要这个行为时，就牵扯出了另一个概念，默认行为阻止
`e.preventDefault();`
这个方法可以阻止默认行为的发生。
IE永远有一个自己的逻辑。和其他浏览器不同，它用来阻止默认行为时使用的是 `e.returnValue = false`;

其他的概念：
### 讲讲冒泡以及如何阻止冒泡
event bubbling 的概念我原来一直都理解的不是很到位。其实说白一点就是想想我们的layout, 是由一个个的元素的层层包裹完成的。
每一个元素都有其hook 的functions. 当你点击一个`<li>`的时候其实你点击了`<table>`之中的元素，也是点击了`<table>`。 所以在`<li>` hook的function 完成之后，会接着触发`<table>`的function.这就是event bubbling。  
如何阻止他呢？这也很简单。那就是使用`e.preventPropagation`的方法。propagation 在英文里是传播的意思，所以就是停止向外传播。跟bubble 差不多，感觉很形象呢。

### 案例

--- 
如何阻止IE和各大浏览器默认行为（      ）
1. window.event.cancelBubble = true;
2. window.event.returnValue = false;
3. event.stopPropagation();
4. event.preventDefault();  

Answer: BD，其他两个是关于冒泡的  

考点： 对于冒泡事件和默认行为的区分，方法认识，以及对ie broswer 和其他浏览器进行区分
--- 


## 隐式的类型转化

### 案例
--- 

以下哪些语句触发了隐式的类型转换？
parseInt(12.34, 10)
0 ? 1 : 2
2e1 * 0xaa
1 + '1'

--- 
B. 在B之中考察了三元运算符，会判断？之前的表达式为T/F。所以number 类型的0发生了隐式转换为boolean  
这里就是0被compiler 解析成了false -> if statement === TRUE: if statement === FALSE

 
## parseFloat() function 
parseFloat() function 是在Number class 下的function. 其作用为讲string -> float number  
`var floatVal = Number.parseFloat("1.95")`然后在console 之中检测数据类型`console.log(typeof floatVal)`
会得到结果`number`.


## isNaN() function 


## escape() 
这个方法已经是破碎的方法了。在MDN 上已经被注释这不要使用了。

 
## eval() function
### 概念
全局对象上的一个函数，会把传入的字符串当做js代码来执行。如果说传入的参数不是String，它会原封不动的将其返回。  
但是在各种使用规范上，包括MDN都强烈的不推荐使用eval().原因是：
1. 降低性能。
2. 安全问题。它给被求值的string 赋予了太大的权力，大家担心可能因此导致XSS攻击
3. 调试困难。
### 牵涉的其他概念以及技术
JSON 是一个轻量级的数据格式。JSON是JS的原生格式，这就意味着JS在处理JSON数据时不需要任何特殊的API或者是工具包，效率也
很高。  
Syntax: varjsonData = `'{"data1": "hello", "data2":"world"}'`;  
调用方法： jsonData.data1, jsonData.data2;  
json的解析方法  json的解析方法一般是两种，
1. eval()
2. JSON.parse()


