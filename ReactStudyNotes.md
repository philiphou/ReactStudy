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

        -- 例子：
                    <script type="text/babel">
                        const myId= 'philip'; const myData='hello philip 666'; const VDOM = (
                        <h2 id={myId}>
                            <span>{myData}</span>
                        </h2>
                        ); ReactDOM.render(VDOM,document.getElementById('test'))
                    </script>

    