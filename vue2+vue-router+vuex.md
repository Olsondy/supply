# 使用vue搭建前后端分离的SPA应用

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
- [x] 简单表单 (选择组件、可搜索选择组件)
- [x] http api封装
- [x] server 异常拦截处理
- [x] 数据的增删改查操作例子


## 目录结构介绍 ##

	|-- build                            // webpack配置文件
	|-- config                           // 项目打包路径
	|-- src                              // 源码目录
	|   |-- assets                       // 图片资源目录
	|   |-- common                       // 组件
	|   |-- components                   // 公共组件
	|           |-- Header.vue           // 公共头部
	|           |-- Home.vue             // 公共路由入口
	|           |-- Sidebar.vue          // 公共左边栏
	|	    |-- page              // 主要路由页面
	|           |-- BaseCharts.vue       // 基础图表
	|           |-- BaseForm.vue         // 基础表单
	|           |-- BaseTable.vue        // 基础表格
	|           |-- Login.vue          	 // 登录
	|           |-- Markdown.vue         // markdown组件
	|           |-- Readme.vue           // 自述组件
	|           |-- Upload.vue           // 图片上传
	|           |-- VueEditor.vue        // 富文本编辑器
	|           |-- VueTable.vue         // vue表格组件
	|   |-- App.vue                      // 页面入口文件
	|   |-- main.js                      // 程序入口文件，加载各种公共组件
	|-- .babelrc                         // ES6语法编译配置
	|-- .editorconfig                    // 代码编写规格
	|-- .gitignore                       // 忽略的文件
	|-- index.html                       // 入口html文件
	|-- package.json                     // 项目及工具的依赖配置文件
	|-- README.md                        // 说明


## 安装步骤 ##

	git clone https://github.com/lin-xin/manage-system.git      // 把模板下载到本地
	cd manage-system    // 进入模板目录
	npm install         // 安装项目依赖，等待安装完成之后

## 本地开发 ##

	// 开启服务器，浏览器访问 http://localhost:8080
	npm run dev

## 构建生产 ##

	// 执行构建命令，生成的dist文件夹放在服务器下即可访问
	npm run build

## 组件使用说明与演示 ##