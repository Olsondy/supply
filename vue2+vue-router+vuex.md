# leo-face 学习脚手架 (基于vue.js的SPA应用)

> 前言

### SPA应用？

- SPA应用的概念
> - SPA (Signle Page Application) 整个webapp就一个html文件，里面的各个功能页面是javascript通过hash,或者history api来进行路由，并通过ajax拉取数据来实现响应功能。因为整个webapp就一个html，所以叫单页面！

- 优势
> - 前后端职责分离，架构清晰：前端进行交互逻辑，后端负责数据处理。
  - 前后端单独开发、单独测试。
  - 良好的交互体验，前端进行的是局部渲染。避免了不必要的跳转和重复渲染

## 功能 ##
- [x] Element UI & iView UI
- [x] 布局(菜单、头部、内容)
- [x] 登录
- [x] 分页表格
- [x] 表单 (选择组件、可搜索选择组件)
- [x] http api封装
- [x] server 异常拦截处理
- [x] 数据的增删改查操作例子


## 目录结构介绍 ##

	|-- build                            // webpack配置文件
	|-- config                           // 项目打包运行环境配置
	|-- src                              // 源码目录
	|   |-- assets                       // 图片资源目录
	|   |-- common                       // 公共模块目录
	|           |-- api                  // http请求方法
	|           |-- components           // 公共通用组件
	|           |-- config               // 路由加载配置
	|           |-- font                 // 全局自定义字体
	|           |-- main                 // 首页布局模板
	|           |-- plugins              // 插件目录
	|           |-- router               // 路由配置
	|           |-- styles               // 通用css样式
	|           |-- utils                // filter 工具函数类
	|   |-- components                   // 当前项目单独组件
	|   |-- mock                         // 模拟请求
	|   |-- stores                       // vuex数据存储
	|   |-- styles                       // 当前项目css样式 
	|   |-- views                        // 当前项目页面模块  
	|   |-- App.vue                      // 页面入口文件
	|   |-- main.js                      // 程序入口文件，加载各种公共组件
	|    
	|    ....
	|   
	|-- .babelrc                         // ES6语法编译配置
	|-- .editorconfig                    // 代码编写规格
	|-- .eslintignore                    // 需要忽略js语法及代码风格的配置
	|-- .eslintrc.js                     // 检查js语法错误及代码风格
	|-- .gitignore                       // git提交忽略的文件
	|-- .npmrc                           // npm install 工具包配置
	|-- index.html                       // 入口html文件
	|-- package.json                     // 项目及工具的依赖配置文件
	|-- README.md                        // 说明





## 安装步骤 ##

	git clone http://code.hoau.net/itiaoling-sc/leo-face.git     // 下载到本地
	cd leo-face      // 进入工程目录
	npm i           // 安装项目依赖，等待安装完成之后
	or      
	npm i --registry=https://registry.npm.taobao.org

## 本地开发 ##

	// 开启服务器，浏览器访问 http://localhost:8089
	npm run dev

## 构建生产 ##

	// 执行构建命令，生成的dist文件夹放在服务器下即可访问
	npm run build

## 组件使用说明与演示 ##
### Element & iView ###
vue.js封装的网站快速成型工具 <a href="https://npmjs.org/package/element-ui"><img src="http://img.shields.io/npm/dm/element-ui.svg" alt="Downloads"></a>
- 源码地址：[Element](https://github.com/ElemeFE/element)
  