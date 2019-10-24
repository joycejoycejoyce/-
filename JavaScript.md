# JavaScript 的练习题看这里

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
window.event.cancelBubble = true;
window.event.returnValue = false;
event.stopPropagation();
event.preventDefault();

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

 


 



