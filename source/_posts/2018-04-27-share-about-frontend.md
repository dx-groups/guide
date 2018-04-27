title: L0 - 前端技术概览
layout: post
---

根据主题循序渐进如下

## 1. 做一个项目需要用到哪些技术？

附上脑暴图

```bash
react/rax/mirror - 框架 - angular、vue、extjs/avalon/knockjs/riot
redux - 组件状态共享 - mobx/immer  === sub/pub, Object.defineProperty(get,set)
ant.design - material design  <=  atomic design
bootstrap

history - 跳转
- 栈 (replace/push)
- pc, 任意性

less - 样式 - sass、css
- css-modular

rxjs - 流式的数据处理框架

nodejs - 语言 - V8

git - 版本控制，分支

es678 - js promise +
babel - pollfill - shim

axios - http 请求 - ajax - xmlhttprequest - fetch

typescript
coffeescript
elm
haskell

jslint
eslint - 统一，语法
stylelint
htmllint
editorconfig

proxy - 本地代理，middleware
xiaoyaoji - 接口定义、mock

设计 => ui => 开发
产品思想
测试，质量
性能

沟通
约定


npm - 包管理工具 vs yarn - 镜像，源，依赖关系
- 版本
- 缓存
- ui
- 串行 / 并行

module.exports = 
require()

import 
export

分治  <= 代码可控

组件化
模块管理工具 - commonjs/ES6 module/amd/cmd/umd/ - seajs/requirejs/
- 业务代码
- 框架代码
- 懒加载


webpack - gulp 流、grunt 配置、rollup、parcel 开箱即用、browserify
- treeshaking
- source-map
- 打包 - js/css/图片/html
- 优化 - 压缩
        * 懒加载
        * vendor
        * hash
        * cdn 替换
        * ...

```

## 2. 前端的方方面面

> 工程化 + 技术栈 => 架构（脚手架）

### 工程化

![engineer](/guide/docs/static/engineer.png)

### 技术

![technology](/guide/docs/static/technology.png)

## 3. 渐进式前端框架

> f(state) => ui

框架的取舍，`arthur` 的演进之路

## 4. 函数式编程

[Monad](www.ruanyifeng.com/blog/2015/07/monad.html)

## 5. 方向？

![choice](/guide/docs/static/choice.png)
