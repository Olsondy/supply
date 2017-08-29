# leo-face 学习脚手架 (基于vue渐进式框架的SPA应用)
<!-- TOC -->

- [leo-face 学习脚手架 (基于vue渐进式框架的SPA应用)](#leo-face-学习脚手架-基于vue渐进式框架的spa应用)
    - [SPA应用？](#spa应用)
    - [项目简介](#项目简介)
    - [兼容性](#兼容性)
    - [功能](#功能)
    - [目录结构介绍](#目录结构介绍)
    - [安装及启动](#安装及启动)
        - [安装](#安装)
        - [本地开发](#本地开发)
        - [测试环境](#测试环境)
        - [生产环境](#生产环境)
        - [构建生产分析](#构建生产分析)
    - [相关组件说明与简单例子演示](#相关组件说明与简单例子演示)
        - [Element & iView](#element--iview)
        - [mock.js 框架的使用](#mockjs-框架的使用)
        - [http请求 axios框架使用](#http请求-axios框架使用)
        - [vuex 状态管理](#vuex-状态管理)
        - [vue-router 路由](#vue-router-路由)
        - [布局](#布局)
        - [内容页](#内容页)
        - [Selector 下拉组件](#selector-下拉组件)
        - [简单的分页表格](#简单的分页表格)
        - [其他](#其他)

<!-- /TOC -->
## SPA应用？ ##
- SPA应用的概念
> - SPA (Signle Page Application) 整个webapp就一个html文件，里面的各个功能页面是javascript通过hash,或者history api来进行路由，并通过ajax拉取数据来实现响应功能。因为整个webapp就一个html，所以叫单页面！

- 优势
> - 前后端职责分离，架构清晰：前端进行交互逻辑，后端负责数据处理。
  - 前后端单独开发、单独测试。
  - 良好的交互体验，前端进行的是局部渲染。避免了不必要的跳转和重复渲染

## 项目简介 ##
Authority Management System (权限管理系统)

[![node](https://img.shields.io/node/v/webpack.svg)](https://github.com/nodejs/node)
[![npm](https://img.shields.io/badge/npm-3.8.9-blue.svg)](https://github.com/npm/npm)
[![webpack](https://img.shields.io/badge/webpack-2.6.1-blue.svg)](https://github.com/webpack/webpack)
[![vue](https://img.shields.io/badge/vue-2.4.2-brightgreen.svg)](https://github.com/vuejs/vue)
[![vuex](https://img.shields.io/badge/vuex-2.3.1-brightgreen.svg)](https://github.com/vuejs/vuex)
[![vue-router](https://img.shields.io/badge/vue--router-2.5.3-brightgreen.svg)](https://github.com/vuejs/vue-router)
[![Travis](https://img.shields.io/travis/rust-lang/rust.svg)]()

- 本项目使用的是vue-cli 脚手架生成的基于webpace的单页应用.[vue-cli 脚手架](https://cn.vuejs.org/v2/guide/installation.html)
- 开发工具
	- 规定使用`webstorm 2017.2 + eslint + babel`
- 基本规范
 - 使用 ES6/ES2015 来编写代码。
 - 统一使用QA工具(eslint)规范进行编码,后续会有代码审查(详细使用在`.eslintrc`)
 - 项目中的错误日志统一使用`console.error`输出
 - 待补充....  :sweat:



## 兼容性 ##
 基于Chrome内核的现代浏览器和Internet Explorer 10+

## 功能 ##
- [x] 布局(菜单、头部、导航、内容)
- [x] 登录
- [x] 路由导航,动态侧边栏（支持多级路由）
- [x] 分页表格
- [x] 表单 (选择组件、可搜索选择组件)
- [x] http请求封装(get post put delete)
- [x] store 状态数据存储
- [x] mock数据
- [x] http请求的国际化
- [x] 与后台交互增删改查的例子
- [x] 多环境发布
- [ ] 权限设计
- [ ] 界面语言、换肤切换


## 目录结构介绍 ##
	|-- build                            // webpack配置文件
	|-- config                           // 项目打包运行环境配置
	|-- src                              // 源码目录
	|   |-- assets                       // 图片资源目录
	|   |-- common                       // 公共模块目录
	|       |-- api                      // http请求方法
	|       |-- components               // 公共通用组件
	|       |-- config                   // 路由加载配置
	|       |-- font                     // 全局自定义字体
	|       |-- main                     // 首页布局模板
	|       |-- plugins                  // 插件目录
	|       |-- router                   // 路由配置
	|       |-- styles                   // 通用css样式
	|       |-- stores                   // 状态管理数据存储
	|       |-- utils                    // 工具函数
	|   |-- components                   // 当前项目单独组件
	|   |-- mock                         // 模拟请求
	|   |-- styles                       // 当前项目css样式
	|   |-- views                        // 当前项目页面模块  
	|   |-- App.vue                      // 页面入口文件
	|   |-- main.js                      // 程序入口文件，加载各种公共组件
	|   |-- permissionMenu.js            // 动态路由权限树菜单的生成
	|    
	|    ....
	|   
	|-- .babelrc                         // babel-loader语法编译配置
	|-- .editorconfig                    // 代码编写规格
	|-- .eslintignore                    // 需要忽略js语法及代码风格的配置
	|-- .eslintrc.js                     // 检查js语法错误及代码风格
	|-- .gitignore                       // git提交忽略的文件
	├── leo-face.ico                      // favicon图标
	|-- .npmrc                           // npm install 工具包配置
	|-- index.html                       // 入口html文件
	|-- package.json                     // 项目及工具的依赖配置文件
	|-- README.md                        // 说明


> 注意:开发时请按照上面目录结构描述进行开发.

## 安装及启动
### 安装 ###

	git clone http://code.hoau.net/itiaoling-sc/leo-face.git     // 下载到本地
	cd cancer-face     // 进入工程目录
	// 安装项目依赖，等待安装完成之后
	npm i  或者 npm i --registry=https://registry.npm.taobao.org   

### 本地开发 ###

	// 开启服务器，浏览器访问 http://localhost:8089
	npm run dev

### 测试环境 ###

	// 执行构建命令，生成的dist文件夹放在服务器下即可访问
	// 生成webpack-bundle-analyzer的code split图
	npm run build:test

### 生产环境 ###

	// 执行构建命令，生成的dist文件夹放在服务器下即可访问
	npm run build:prod
### 构建生产分析 ####

	// 执行 单元测试
	npm run unit
	// 端到端测试
	npm run e2e
	// 所有测试
	npm test

## 相关组件说明与简单例子演示 ##
### Element & iView ###
基于vue2.x封装的网站快速成型工具包

>项目已经在`main.js`中引入了相关依赖,在组件中直接按照官方例子使用即可,如需在js中单独使用,请使用`import`按需引入

**相关地址**
- [Element](https://github.com/ElemeFE/element) ,[官方教程](http://element.eleme.io/#/zh-CN)<p></p>
[![version](https://img.shields.io/badge/element--ui-1.4.2-brightgreen.svg)](https://github.com/ElemeFE/element)
[![downloads](http://img.shields.io/npm/dm/element-ui.svg)](https://github.com/ElemeFE/element)

- [iView](https://github.com/iview/iview/),[官方教程](https://www.iviewui.com)<p></p>
[![version](https://img.shields.io/badge/iview-2.1-brightgreen.svg)](https://github.com/iview/iview/)
[![downloads](http://img.shields.io/npm/dm/iview.svg)](https://github.com/iview/iview/)

>注意
- leo-face 脚手架使用了俩个ui组件库的组件.组件内部使用互不影响,但可能某些情况下会出现css样式冲突


### mock.js 框架的使用 ###
拦截并模拟 ajax 请求

>项目使用了mock.js模拟，在无后台环境前可使用展示界面,需使用后端api，可在main.js移除
>
>	  import 'common/mock/index.js'; // 模拟http数据请求  (注释则可以调用本地配置的开发环境)

**相关地址**
- [官方wiki](https://github.com/nuysoft/Mock/wiki/Getting-Started)
- [简易教程](http://cnodejs.org/topic/53f718218f44dfa3511af923)

**使用**
- 文件位置`common/mock/index.js`

```javascript
/**
 * 测试接口覆盖
 */
import Mock from 'mockjs';
import mockAPI from './response';

// 声明需要拦截的地址请求,
// 参数说明
// restful接口
// http method
// 执行请求方法
// 前俩个参数需与拦截的请求一致方可拦截成功
Mock.mock(/\/users\/v1\/actions\/login/,'post',mockAPI.login);
```

### http请求 axios框架使用 ###
**基于http客户端的promise，面向浏览器和nodejs**

[![axios](https://img.shields.io/badge/axios-0.16.2-brightgreen.svg)](https://github.com/mzabriskie/axios)
> vue更新到2.0之后，就宣告不再对vue-resource更新，而是推荐的axios

**相关地址**
- [源码地址](https://github.com/mzabriskie/axios)
- [中文翻译文档](https://segmentfault.com/a/1190000008470355)

**使用**
- 文件位置`common/api/http.js`
  ```javascript
	//get请求
	http.get(getUrl, params).then(data =>{

	}).catch(error=>{

	})

	//post or put请求  请求url、请求json对象、请求方法
	http.mergePostAndPut(reqUrl, params,reqMethod).then(data =>{

	}).catch(error=>{

	})
			//delete 请求
	http.delete(delUrl).then(data =>{  

	}).catch(error=>{

	})
  ```

- 使用例子
```javascript
     //获取用户信息
     http.get('/users/v1/current').then(data => {
          if (data){
            const user = data.result;
            if (user){
              commit('SET_NAME', user.userChineseName);  
              commit('SET_CODE', user.userCode);
            } else {
              return Message({
                message: '获取用户信息失败',
                type: 'error',
                showClose: true,
                duration: 5 * 1000
              });
            }
          }
    }).catch(error => {
       //异常需要处理的流程
    });
```

> 提示: 在目录`common/utils/fetch.js`中封装了axios的httpRequest和httpResponse相关promise hook

### vuex 状态管理 ###
应用的数据与状态存储

>- `main.js`已经全局导入声明了vuex
>- 项目中只有user和app配置相关状态使用vuex存在全局，其它数据都由每个业务页面自己管理。


**相关地址**
- [vuex](https://vuex.vuejs.org/zh-cn/)
- [Actions](https://vuex.vuejs.org/zh-cn/actions.html)

**实例介绍**
- 目录结构`src/common`

		|-- stores                               //stores目录
		|   |-- module                           //模块    
		|       |-- app.js                       //当前应用使用的数据存储对象及操作
		|       |-- permission.js                //整个系统路由的数据存储对象及操作
		|   		|-- user.js                      // 左侧菜单路由渲染组件
		|   |-- getters.js                       // vuex对象属性全局获取的对象
		|   |-- index.js                         // vuex对象声明创建
- 组件中使用
```javascript
//在vue的computed属性中使用Es6数组扩展运算符加载getters对象
computed: {
	...mapGetters([
	'permission_routers',
	'sidebar'
	]),
}
//组件中使用
this.$store.dispatch('toggleSideBar')  //vue当前组件对象中使用
this.$store.commit('SET_LANG',e);  //提交数据存储到vuex对象
//js中使用
store.dipatch('login')   
```

### vue-router 路由
使用vue-router实现的动态路由导航

>项目中根据权限的数据生成的vue-router对象,达到动态路由的目的渲染菜单和页面

**相关地址**
- [router导航](https://router.vuejs.org/zh-cn/advanced/navigation-guards.html)
- [router导航信息配置](https://router.vuejs.org/zh-cn/api/route-object.html)

**实例介绍**
```javascript
//main.js
import router from 'common/router';

//router/index.js
//设置当前系统的默认路由导航
export const constantRouterMap = [{
	path: '/login',component:_import('login/LoginPage'), hidden:true
},
{
	path: '/',
	name: '首页',
	component: LeoLayout,
	redirect: '/main',
	hidden: true,
	children: [
		{ path: '/main', component: homepage }
	]
}];
//创建路由
export default new Router({
	mode:'history',  //此模式适用服务端
	routes: constantRouterMap
});

//permissionMenu.js
//导航拦截,用来完成跳转
router.beforeEach((to, from, next) => {});
//完成导航
router.afterEach(() => {});
```

### 布局 ###
项目的主体框架布局

**介绍**
- 目录结构`src/common`

		|  -- main                              // 首页目录
		|    |-- Layout.vue                    // 主组件
		|    |-- siderbar.vue                  // 左侧菜单面板组件
		|    |-- siderbarItem.vue              // 左侧菜单路由渲染组件
		|    |-- Navbar.vue                    // 头部组件
		|    |-- Levelbar.vue                  // 面包屑组件
		|    |-- TabsView.vue                  // 基于tags的标签页组件(后续修改为tabs)
		|    |-- AppMain.vue                   // 右侧内容布局组件

>布局虽统一,但可扩展功能,不同情况下可添加组件和样式修改

### 内容页 ###
- 表单,表格的一致性风格
```html
<template>
  <div class="app-container">
    <div class="filter-container">
	<Form :label-width="80">
        <el-row>
          <el-col :span="5">
            <Form-item label="系统编码">
              <static-selector :params="codeSelector" ref="staticSelector"></static-selector>
            </Form-item>
          </el-col>

          <el-col :span="5">
            <Form-item label="系统名称">
              <dynamic-selector :params="nameSelector" ref="dynamicSelector"></dynamic-selector>
            </Form-item>
          </el-col>

          <el-col :span="5">
            <Form-item label="系统编码">
              <Input  placeholder="输入系统名称"/>
            </Form-item>
          </el-col>
          <el-col :span="5">
            <Form-item>
              <Button size="small" type='primary' icon="search" @click="clickSearch">查 询</Button>
              <Button size="small" type='primary' icon="refresh" @click="clickReset">重 置</Button>
            </Form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <Form-item label="系统名称">
              <Input placeholder="输入系统名称"/>
            </Form-item>
          </el-col>
          <el-col :span="6">
            <Form-item label="创建日期">
              <date-time-multiple :emptyText="dateEmptyText" ref="dateMultiple"></date-time-multiple>
            </Form-item>
          </el-col>
        </el-row>
      </Form>
    </div>
    <div class="panel-container">
		   这里是表格内容...
    </div>
  </div>
</template>
```

### Selector 下拉组件 ###
**以`ChildSystemSetting.vue`组件使用为例**

- 可选择selector `StaticSelector.vue`
	- 在父组件中使用
		- `template`
			```html
			<el-col :span="4">
			 <Form-item label="系统编码">
				 <static-selector :params="codeSelector" ref="staticSelector"></static-selector>
			 </Form-item>
			</el-col>
			```

  		- `script`
			```javascript
			data () {
			return {
			codeSelector: {
				selectAt: 'all',     //设置默认值
				emptyText: '选择系统编码',  //设置默认文本提示,默认值是:'请选择'
				remoteUrl: '/sub-systems/v1/display' //获取数据的url
			}
				}
			}
			```

- 动态搜索selector `DynamicSelector.vue`
	- 在父组件中使用
		- `template`
			```html
			<el-col :span="4">
				<Form-item label="系统名称">
			 		<dynamic-selector :params="nameSelector" ref="dynamicSelector"></dynamic-selector>
				</Form-item>
			</el-col>
			```

		- `script`
			```javascript
			data () {
				return {
					nameSelector: {
						emptyText: '选择系统编码',  //设置默认文本提示,默认值是:'请选择'
						remoteUrl: '/sub-systems/v1/systemName' //获取数据的url
					}
				}
			}
			```

> 说明:
>- `:params`自定义属性,该属性封装了父组件传递给子组件的信息
>- `ref`属性用于获取子组件信息进行通信,在当前vue对象中使用`this.$refs.XXX`获取子组件
>- `@selectChange`自定义选择事件,当前组件选择option后触发
>- `StaticSelector.vue`中的方法,
>	- `resetValue`,重置下拉选择
>	- `loadData`,执行获取服务器请求方法
>- `DynamicSelector.vue`中的方法,
>	- `setSelectorValue`,重置或设置默认值
>	- `remoteMethod`,对输入的值进行搜索返回渲染的方法

### 简单的分页表格 ###

- `template`
```html
<el-row class="filter-btn">
  <el-col align="right">
    <Button size="small" icon="plus" @click="clickAdd">新 增</Button>
    <Button size="small" icon="edit" @click="clickUpdate" :disabled="updateDisabled">修 改</Button>
    <Button size="small" icon="trash-b" @click="clickDelete" :disabled="delDisabled">删 除</Button>
    <Button size="small" icon="ios-download" @click="exportData">导 出</Button>
  </el-col>
</el-row>
<el-table
   ref="systemTable"
   :data="list"
   v-loading.body="listLoading"
   border fit highlight-current-row
   tooltip-effect="dark"
   @selection-change="handleSelectionChange"
   style="width: 100%">

   <el-table-column type="selection"              @selection-change="handleSelectionChange">
   </el-table-column>

   <el-table-column align="center" v-if="false" prop="id" label="id">
   </el-table-column>

   <el-table-column
   show-overflow-tooltip
   v-for="column in columns"
   :prop="column.prop"
   :label="column.label"
   :width="column.width"
   :min-width="column.minWidth"
   :align="column.align"
   :key="column.prop">
   </el-table-column>

   <el-table-column show-overflow-tooltip align="center" prop="createTime" label="创建时间" :formatter="dateFormatter">
   </el-table-column>

   <el-table-column show-overflow-tooltip align="center" prop="modifyTime" label="修改时间" :formatter="dateFormatter">
   </el-table-column>
   </el-table>

   <div v-show="!listLoading" class="grid-pagination" align="right">
     <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page.sync="listQuery.page"
                 :page-sizes="tablePaginationSize" :page-size="listQuery.limit" layout="total, sizes, prev, pager, next, jumper" :total="total">
  </el-pagination>
</div>
```
- 主要相关的`script`
  ```javascript
  //data对象
  //表格的模板列
  columns: [
    { prop: 'systemCode', label: '系统编码',align:'center' },
    { prop: 'systemName', label: '系统名称',align:'center' },
    { prop: 'entryUrl', label: 'URL地址', minWidth: '150',align:'center' },
    { prop: 'createUserCode', label: '创建人工号',align:'center' }
  ]
  //computed
  computed : {
    ...mapGetters([
      'tablePaginationSize'
    ])
  },

  //methods
  paginationList(){  
     //fetch data
  },
  handleSelectionChange(val){  //表格选择处理
    this.multipleSelection = val;
  },
  handleSizeChange(val) { //分页
    this.listQuery.limit = val;
    this.paginationList();
  },
  handleCurrentChange(val) {
    this.listQuery.page = val;
    this.paginationList();
  },
  dateFormatter(row, column){
    let date = row[column.property];
    if (date) {
      return utils.parseTime(date,'{y}-{m}-{d} {h}:{i}:{s}');
    }
    return '';
  },
  ```

>说明
- 表格使用的是`elementUI`最基本的表格,需要扩展请自行开发
- 表格的首列是`checkbox`可选择列,单独定义一列,设置`type`属性为`selection`,并且绑定选择事件`@selection-change="handleSelectionChange"`
- 模板列,使用`v-for`指令遍历定义的列模板数据
- 数据渲染,`:formatter`属性,指定方法进行返回值渲染

### 其他 ###
**font**

>项目中的有4个字体组件,ElementUI 和 iview自带的以及自定义的,以下俩个是自定义字体组件的使用

- [vue-awesome](https://github.com/justineo/vue-awesome)
	- 组件中使用
	```html
	<template>
	   <icon-vueSvg name="you icon name"></icon-vueSvg>
	</template>
	```
	- js注册图标
	```javascript
      //index.js
      //引入自定义注册库的js
      import './font-basic';

      //font-basic.js
      //引入图标组件进行图标注册
      import Icon from './Icon';

      Icon.register({
         'information': {
         'width': 1024,
         'height': 1024,
         'paths': [
             {
					//svg数据
             }
           ]
         }
      });
	```

>给图标设置样式（大小可以通过 transform: scale() 来设置）
>新建图标文件出口文件，这个在使用的图标很多的时候比较方便

- [iconfont](http://iconfont.cn/)
	- 使用图标库步骤:
		- 在当前自己的图标库中生成`symbol`引用地址
		- 定义一个自定义的`icon.vue`组件
		- 组件中使用
		```html
  		<template>
  		   <icon-fontSvg icon-class="you icon name"></icon-fontSvg>
  		</template>
		```

>项目统一使用一个项目图标库,只生成一个统一的图标库地址,不需要开发者单独去生成引用,可以使用即可

**vue-devtools**
- 基于chrome的vuejs开发调试工具
- [下载及使用](http://www.cnplugins.com/devtool/vuejs-devtools/)
