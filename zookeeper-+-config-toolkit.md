# 配置集中管理搭建
分布式应用配置工具包config-toolkit 用于集群配置向 zookeeper的迁移

[TOC]

## introduction
>* Zookeeper
>* Config Toolkit

## zookeeper
zookeeper是为分布式应用设计的一个高性能协调服务，提供了如下的通用服务，如命名、配置管理、通过锁和分组服务，封装成简单易用的接口而无需开发人员从头编写代码。可以拿来即用，应用的领域有取得共识、分组管理、领导者选举和协议呈现。还可以按需自定义功能 [官网介绍](http://zookeeper.apache.org)

### Quick Start

## Config Toolkit
Config Toolkit 是大型集群和分布式应用配置工具包。Config Toolkit 用于简化从本地配置文件到 Zookeeper 的迁移。在大型集群和分布式应用中，配置不宜分散到集群结点中，应该集中管理。

### Module
>* Config Toolkit ： 封装应用属性配置的获取及更新
>* ConfigWeb： 提供web界面维护属性配置，提供配置导入导出功能

### Features
>* 集中管理集群配置
>* 实现配置热更新
>* 多配置源支持，内置支持zookeeper、本地文件、http协议
>* Spring集成
>* 本地配置覆盖
>* 配置管理web界面
>* 版本控制，支持灰度发布
>* 支持为配置项添加注释

### Quick Start
* 下载安装config-toolkit工具包
```java
    git clone https://github.com/dangdangdotcom/config-toolkit.git
    cd config-toolkit/config-zk-web
    mvn package
```
* 将编译好的config-web.war部署到tomcat即可
* applicationContext.xml 结合spring SPEL方式注入配置
```xml
    <config:profile connect-str="localhost:2181" root-node="/projectx/modulex" version="1.0.0"/>
    <config:group id="groupProp" node="group"/>
    
    <!-- Your business bean -->
    <bean class="your.BusinessBean">
    <property name="strProp" value="#{groupProp['config.str']}" />
    <property name="intProp" value="#{groupProp['config.int']}" />
    </bean>
```


