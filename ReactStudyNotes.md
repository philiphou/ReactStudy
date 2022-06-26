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