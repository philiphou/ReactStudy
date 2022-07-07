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
* 类相关的基本知识及类式组件
    - 类的基本知识--例子
        <script type="text/javascript">
          //  定义一个Person的类 ; 定义类用关键字 class
        class Person {
            // 构造器函数 constructor， 里面参数就是实例对象的属性
            constructor(name, age) {
                    //  构造器中的this是类的实例对象，new 的是谁 this 就是谁
                    this.name = name;
                    this.age = age
                }
                //     person带有的行为或者方法（一般方法）： 
            speak() {
                // speak()放在了哪里？ 放在了 Person类的原型对象上， 是供给实例对象用的；
                //  通过Person实例调用 speak()时， this 就是该实例； p1.speak.call({a:1,b:2}) call 方法就是临时改变this 指向，就是把call 里的参数做this,调用 speak 方法；
                // apply 和 bind 也都可以更改 this的指向
                console.log(`my name is ${this.name}, my age is ${this.age}`)
            }
        }
        //  创建一个 student 类， 继承于Person类
        class Student extends Person {
            //     构造器不是一个必须要写的东西，此处 Student 可以继承 Person的构造器函数，一样可以接收 name age 参数属性，也会继承 speak()方法； 
            //  对于这个 Student类，因为我们需要额外的属性，比如 studentID, 此时对于新属性，我们还是需要利用构造器函数去添加： 
            constructor(name, age, gender) {
                    //  对于继承的 name 和 age 属性，我们可以直接用关键字 super()去实现复制继承，对于新的属性，我们手动添加给student；
                    // 如果在子类中需要添加构造器函数，那么必须调用 super(), 并把共有属性传入到super(共有属性1，共有属性2.。。。)中
                    super(name, age) // 注意要把子类与父类共有的属性，作为参数传入到super() 中，这样super() 就可以调用父类里的构造器，实现属性配置
                    this.gender = gender // gender 是子类中新添加的属性，在构造器中手动加入
                }
                //  为了让 speak()方法更全面，我们给 Student 类重写 speak(), 我们叫重写从父类继承来的方法；
            speak() {
                    console.log(`my name is ${this.name}, my age is ${this.age} and my gender is ${this.gender}`)
                }
                //  学生独有的方法 study()
            study() {
                //  study ()放在了哪里？ Student 类的原型对象上， 供实例对象使用或调用
                //  通过Student实例，调用 study（）时， this 就是该实例对象
                console.log("我学习很努力")
            }
        }
        // 创建一个 Person的实例对象
        const p1 = new Person('tom', 18)
        const p2 = new Person('jack', 28)
        console.log(p1, p2)
        p1.speak()
        p2.speak()
        p2.speak.call({
                name: 'liyi',
                age: 18
            }) // 输出：my name is liyi, my age is 18
            // 创建一个 Student的实例对象
        const s1 = new Student("david", 22, 'male')
        console.log(s1)
        s1.speak()
        s1.study()
            /*
            总结：
            1. 类中的构造器不是必须要写的， 要对实例进行一些初始化操作时候，如添加指定属性时候，才写构造器函数
            2. 如果A类继承了B类，且A类中写了构造器，那么A类构造器中， super()是必须要调用的，调用时候还要传入A,B共有的属性；
            3. 类中所定义的方法，都是放在了类的原型对象上，供实例去使用；
            */
    </script>
    - 类式组件： 
              class Mycomponent extends React.Component{
                  render(){
                   return (<h2> 我是类式组件哟（适用于复杂组件的创建）</h2>) 
                          } 
                 }; 
               ReactDOM.render(<Mycomponent/>,document.getElementById('test'))
                <!-- 
                类式组件里的 render()方法是放在哪里的？ 放在组件的原型对象上，供实例使用， render()中的this 是Mycomponent类（组件）的实例对象
                ReactDOM.render(<Mycomponent/>,document.getElementById('test')) 执行逻辑： 
                1. React 解析组件标签，找到了Mycomponent组件
                2. 发现组件是类式组件，随后new 出一个该类的实例， 并通过实例去调用原型上的render()方法， 得到返回的虚拟DOM
                3. 将render()返回的虚拟DOM转换为真实DOM， 呈现在页面上 */
                -->
    - 复杂组件（类式组件实例的三大属性之state)： 
        -- 有状态 state 的组件就是复杂组件；比如 人这个组件 就是有状态的；状态就会影响或者驱动行为； 组件的状态驱动页面；
        -- 组件的状态里存储着数据，数据的改变就会更新页面；
        -- 状态state是组件实例对象身上的属性；值是对象（可以包含多个键值对）
        -- 组件被称为“状态机”， 通过更新组件的state来更新对应页面的显示（重新渲染组件）
        -- 注意：
            1. 组件中的render方法中的this为组件实例对象
            2. 组件自定义方法中的this 为 undefined,如何解决？
                a. 强制绑定this: 通过含税对象的 bind()
                b. 箭头函数
            3. 状态数据： 不能直接修改或者更新！
* 组件三大属性之一： state
    - state 是组件对象最重要的属性，值是对象，可以包含多个键值对
    - 组件被称为状态机，通过更新组件的state来更新对应的页面显示（重新渲染组件）
    -强烈注意：
        -- 组件中render 方法中的this 为组件实例对象
        --  组件自定义的方法中的this 为undefined, 因为组件内部默认开启严格模式，自定义的函数禁止this指向全局window, 为了让自定义函数的this指向实例对象可以：
            a. 强制绑定this; 通过函数对象的 bind()
            b.箭头函数； 利用把箭头函数赋值给属性实例对象
        -- 状态数据： 不能直接修改或者更新
* 组件三大属性之 props
* 组件三大属性之 refs 与事件处理， refs 类似于原生html 中的 id 等属性标识符; refs是一个对象，里面是键值对，键就是ref 的名字，值就是该节点
* 组件生命周期： 生命周期回调函数 或者钩子；
    - 组件从创建到死亡会经理一些特定的阶段
    - React组件中包含一系列钩子函数（生命周期回调函数）会在特定的时刻调用
    - 我们在定义组件时候，会在特定的生命周期回调函数中做特定的工作
* 生命周期阶段 (旧)
    - 初始化阶段：由ReactDOM.render()触发，初次渲染
        -- constructor()
        -- componentWillMount()
        -- render()
        -- componentDidMount() ---->这个钩子比较常用，一般在这个钩子中做一些初始化的操作， 例如开启定时器，发送网络请求，订阅消息等。
    - 更新阶段： 由组件内部 this.setState() 或者父组件重新render 触发
        -- shouldComponentUpdate()
        -- componentWillUpdate()
        -- render() ----> 基本一直在用。
        -- componentDidUpdate()
    - 卸载组件： 由 ReactDOM.unmountComponetAtNode()触发
        -- componentWillUnmount() ----> 这个钩子比较常用，一般做一些收尾的事： 关闭定时器， 取消订阅消息；
* 生命周期阶段 (新)
    - 新版本中，除了 componentWillUnMount() 之外所有的Will钩子都需要在前面加 UNSAFE_: 
    - 包括： ComponentWillMount; ComponentWillUpdate; ComponentWillReceiveProps
    - React 正在设计异步渲染， 过时的生命周期会给React未来版本推出异步渲染后带来不安全的编码实践， 就是上面这三个 UNSAFE 的钩子；预计在未来的异步渲染中，这些钩子可能被误用，所以尽量避免使用；
    - 新生命周期阶段
        -- 初始化阶段： 由 ReactDOM.render()触发，初次渲染
            1. constructor()
            2. componentWillMount()
            3. render()
            4. componentDidMount() ===> 常用
                一般这个钩子中做一些初始化的事，如：开启定时器，发送网络请求，
        -- 更新阶段： 由组件内部 this.setState() 或者父组件重新render触发
            1. getDerivedStateFromProps
            2. shouldComponentUpdate()
            3. render()
            4. getSnapshotBeforeUpdate
            5. componentDidUpdate()
        -- 卸载组件： 由 ReactDOM.UnmountComponentAtNode()触发
            1. componentWillUnmount() 
        -- 总结：重要的钩子
            1. render
            2. componentDidMount
            3. componentWillUnmount
        -- 即将废弃的钩子：
            1. componentWillMount
            2. componentWillUpdate
            3. componentWillReceiveProps
* React Diffing 算法：最小力度是节点（也就是对比的最小单位， 是所有节点）
    - 经典面试题
        1. react中的key 有什么作用？（key的内部原理是什么）
            -- 简单的说，key 就是虚拟DOM中对象的标识，在更新显示时候，key 起着及其重要的作用
            -- 详细的说： 当状态中数据发生变化时候，react会根据新数据生成新的虚拟DOM， 随后React进行虚拟DOM 与旧虚拟DOM的diff比较，比较规则如下：
                1. 旧虚拟DOM中找到了与新虚拟DOM相同的key
                   - 若虚拟DOM中内容没变，直接使用之前的真实DOM
                   - 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM
                2. 旧虚拟DOM中未找到与新虚拟DOM相同的key
                    - 根据数据创建新的真实的DOM，随后渲染到页面
        2. 为什么遍历列表时候，key最好不要用index?
            -- 若对数据进行：逆序添加，逆序删除等破坏顺序的操作： 
                会产生没有必要的真实DOM的更新---> 页面效果没问题，但是效率低
            --  如果结构中还包含输入类的DOM， 则会产生错误的DOM 更新---》界面有问题
            -- 注意，如果不存在对数据的逆序添加，逆序删除等破坏顺序的操作，仅用于渲染列表用于展示，则使用index 是没有问题的。
        3. 开发中如何使用选择key?
            -- 最好使用每条数据的唯一标识，比如 id, 手机号，身份证号，学号等唯一值；
            -- 如果确定只是单一的展示数据，用index也是可以的。
* React 脚手架
    - 使用create-react-app 创建 react 应用
        1. xxx 脚手架是用来帮助程序员快速创建一个基于 xxx库的模板项目
            - 包含了所有需要的配置 （语法检查，jsx 编译， devServer）
            - 下载好了所有相关的依赖
            - 可以直接运行一个简单效果
        2. react 提供了一个用于创建react项目的脚手架： create-react-app
        3. 项目的整体技术架构为： react + webpack +es6 +eslint
        4. 使用脚手架开发的项目特点： 模块化，组件化，工程化
    - 创建项目并启动： 
        1. 全局安装：  npm install -g create-react-app
        2. 切换到想床项目的目录 使用命令： create-react-app my-app
        3. 进入项目文件夹： cd my-app
        4. 启动项目： npm start

        

