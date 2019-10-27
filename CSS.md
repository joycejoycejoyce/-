# CSS 的面试题

## overflow 属性的value 
overflow 是一个加在父元素上的属性，用来定义父元素如何处理溢出的子元素。  
它的四个值为：
1. visible (default): 子元素溢出时可见
2. auto：当子元素溢出时出现滚动条 
3. scroll： 无论子元素是否溢出都添加滚动条
4. hidden： 隐藏子元素的溢出部分

### 案例
--- 
css属性overflow属性定义溢出元素内容区的内容会如何处理。如果值为 scroll，不论是否需要，用户代理都会提供一种滚动机制。
True
False

A: True
---

### Codepen 代码
`<p class="codepen" data-height="300" data-theme-id="37857" data-default-tab="js,result" data-user="joycho123" data-slug-hash="KKKmKrG" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="css overflow attribute">
  <span>See the Pen <a href="https://codepen.io/joycho123/pen/KKKmKrG">
  css overflow attribute</a> by Joy (<a href="https://codepen.io/joycho123">@joycho123</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>`



