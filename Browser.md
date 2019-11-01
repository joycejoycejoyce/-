# 浏览器

## 浏览器的幕后工作原理
### 包含的浏览器
Opera, Chrome, Safari, Firefox, IE 
### 浏览器的主要功能
* 浏览器解释并显示HTML 文档的方式是在HTML和CSS规范中指出的。这些规范由网络标准化组织W3C在进行维护 
* 多年来，各个浏览器都没有完全遵从这些规范。同事还在开发自己独有的extension。这给网络开发人员带来了比较严重的兼容性问题。
如今的大多数浏览器都或多或少的遵从规范。

### 浏览器的高层结构
浏览器的主要组件是：
1. 用户界面：包括地址栏，前进后退按钮，书签菜单等。除了浏览器主窗口显示的是user request的page, 其他的显示部分都属于user interface  
2. 浏览器引擎: 在user interface 和 呈现引擎之前传送指令
 `
 user interface  <--" do that"--browser engine   --" do this"  --> 呈现引擎  
 `
3. 呈现引擎:
    负责显示请求的内容。如果请求的内容是HTML,它就负责解析HTML和CSS内容，并将parse后的内容render在screen上
    `
     呈现引擎  --> parse(requstedContent)  --> render(requestedContent) 
    `
4. 网络：
    用于网络调用。比如THTTP request. 其接口与平台无关。并为所有平台提供底层实现。
5. 用户界面后端：
    用于绘制基本的窗口小部件，比如组合框和窗口。公开了和平台无关的通用接口。
6. JS解释器：
    parse & execute JS code 
7. data storage
    这是持久层。Browser需要在HW上保存各种数据，e.g. Cookie. HTML5 规范定义了“网络数据库”，这是一个完整（但是轻便）的
    浏览器内数据库。

Relationship Diagram
    `
        User Interface 
            |          |
        Browser Engine |-- Data Persistence  
            |          | 
        Render Engine  |
        |    |         |
        |    |         | 
Networking   |         |
            JS         | 
       Interpreter     |
                    UI Backend    
    
    `
Chrome 浏览器和别的浏览器不同。Chrome浏览器的每一个标签页都分别
对应一个Render Engine instance. 每一个page 都是一个独立的进程。
* 

