## React Study Notes ##
# React 简介
* React 是一个将数据渲染为HTML视图的开源 JS库
    - 由 Facebook 开发，且开源； Jordan Walke 创建，2012 应用到Ins 上，2013年开源
    - 近10年陈酿，正被很多一线大厂使用
* React 好处： 
    - 原生的JS 操作DOM 繁琐，效率低 （DOM-API 操作 UI) : document.getElementById('box'); document.querySelector('#box')
    - 使用 JS 直接操作DOM， 浏览器会进行大量的重绘重排
    - 原生JS 没有组件化编码方案，代码复用率较低
    - React 采用组件化模式，声明式编码，提高开发效率及组件复用率
    - 在 React Native 中可以使用 React 语法进行移动端开发；
    - 使用 虚拟 DOM 技术 和优秀的 Diffing 算法，尽量减少与真实 DOM 的交互
* JSX ： 
    - JSX 全称： JavascriptXML, 是react 定义到额一种类似于XML 的JS 扩展语法： JS+XML,
        -- XML 早期用于存储和传输数据，
               <student>
                       <name> Tom </name>
                       <age> 20 </age>
               </student>
        -- 后来逐步改进为JSON格式： 
           "{
            "name":"Tom",
            "age":20
           }"
    - 本质是 React.createElement(component,props,...children) 方法的语法糖
    - 作用： 用来创建虚拟DOM, 语法： var ele = <h1>helloworld</h1> 注意： 它不是字符串，也不是html/xml标签，它最终是产生一个JS对象；

    - 例子：
        <script type="text/babel">
            const VDOM = (
                <h1>Hello,React</h1>
                )
            ReactDOM.render(VDOM,document.getElementById('test')) 
        </script>
    - 虚拟DOM 的两种创建方法：
        1. JSX 方法: 如上例：   const VDOM = <h1>Hello,React</h1>
        2. JS 方法： const VDOM= react.createElement('h1',{id:'title'},'hello world')， 开发时候基本不用；
    - 浏览器不认识JSX 语法，所以要用babel去翻译，转译成JS 语言，本质就是 利用 react.createElement(标签名，标签属性，标签体)； JSX 就类似一种语法糖
    -  语法; 
        -- 1. 定义虚拟DOM时候，不要写引号
        -- 2. 标签中混入JS表达式时候，要用{} 引入
        -- 3. 样式的类名指定，要用 className, 不能用 class; 因为 class 是 ES6中保留的关键字
        -- 4. 内联样式规则 ；JSX要用 style= {{key:value}} 样式去写
            * html 下可以： style = "color:orange;width:100px" 其实是多组key value pair
            * JSX 下规则： style={{color:'white',fontSize:'10px'}} 属性名改为驼峰形式，比如 fontSize; 属性值加引号，不然会误以为是变量
        -- 5.  JSX 下的 虚拟DOM 只能有一个根标签，不可以有多个，需要用一个 div 在外面包起来；
        -- 6. 标签必须闭合；
        -- 7. 关于标签首字母， 
            * 若小写字母开头，则将该标签转换为Html中同名元素，若html中无同名元素，则报错；
            * 若大写字母开头，则react就去渲染对应的组件，若组件没有定义，则报错；

* 模块与组件
    - 模块： 
        -- 理解： 向外提供特点功能的JS程序，一般就是一个JS文件
        -- 为什么要拆成模块，随着业务逻辑增加，代码越来越多且复杂】
        -- 作用： 复用 JS，简化JS的编写，提高JS运行效率；
    - 组件
        -- 理解： 用来实现局部功能效果的代码和资源的集合
        -- 为什么一个页面更复杂
        -- 作用： 复用编码，简化项目编码，提高运行效率
    - 模块化和组件化；当应用是以JS模块和多组件方式实现的，这个应用就是模块化和组件化的项目；
* 函数式组件：
    - 例子：
          function Democomponent(){ console.log(this);return (
        <h2>我是函数式组件(适用于简单组件的定义)</h2>) }; 
        ReactDOM.render(<Democomponent/>,document.getElementById('test')) 
        // 上面的this 是 undefined, 因为 babel 编译后开启了严格模式，严格模式下自定义的函数不会让this指向window
    - ReactDOM.render(<Democomponent/>,document.getElementById('test')) 执行逻辑：
        -- React解析组件标签，找到 Democomponent组件
        -- 发现组件是函数定义的， 随后调用该函数，将返回的虚拟DOM转为真实DOM，随后呈现在页面中；
* 类相关的基本知识