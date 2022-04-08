# vue2-element-admin
基于 ElementUI + Vue2 后台管理系统，将之前开发常用的前端基建整合优化。

## 一、前期准备
前期需要准备：node环境配置 > yarn包管理 > UI框架 > webpack配置 > Jest单元测试 > Mock模拟数据 > Git版本管理配置 等等。 

### 1.1 项目结构
首先要了解项目结构，可以使用treer生成项目目录结构。

```shell
# 安装
yarn add treer 

使用方式: treer [options]

# 帮助
treer --help

 -V, --version          output the version number # 版本号
 -d, --directory [dir]  Please specify a directory to generate structure tree (default: "/Users/wangping/self/node-exer") # 导出树的目录
 -i, --ignore [ig]      You can ignore specific directory name  # 忽略的目录
 -e, --export [epath]   export into file  # 导出的目录 <导出路径/文件名>
 -h, --help             output usage information

# 使用方法： treer -i "排除的目录，支持正则" -e "导出文件名.md"
treer -i "/node_modules|dist_electron|devtools|nouse|.git|.vscode/" -e "tree.md"
```

项目目录：

```shell
D:\XPROJECT\PROGRAM\vue2-element-admin
├─.browserslistrc # 配置兼容浏览器
├─.editorconfig # 编辑器的配置
├─.eslintrc.js # ESlint编程规范
├─babel.config.js # Babel配置 
├─LICENSE # LICENSE 开源软件协议
├─package.json # 配置项目所需的依赖和启动命令
├─README.md # 必读markdown文件
├─yarn.lock # yarn依赖包lockfile
├─src
|  ├─App.vue # 根组件
|  ├─main.js # 入口文件
|  ├─views # 视图代码归类
|  |   ├─About.vue
|  |   └Home.vue
|  ├─store # 全局状态管理归类
|  |   └index.js
|  ├─router # 路由归类
|  |   └index.js
|  ├─components # 组件归类
|  |     └HelloWorld.vue
|  ├─assets # 资源（图片、字体等）归类
|  |   └logo.png
├─public # 静态文件归类
|   ├─favicon.ico
|   └index.html # 主页，项目入口
```

#### .browserslistrc
**作用：**
browserslist 是在不同的前端工具之间共用目标浏览器和 node 版本的配置工具。主要被以下工具使用：
* Autoprefixer
* Babel
* post-preset-env
* eslint-plugin-compat
* stylelint-unsupported-browser-features
* postcss-normalize

举例来说，项目创建的时候，我们需要通过确认兼容哪些版本的浏览器。因为超过我们设定范围的浏览器版本，

参考文章：[前端工程基础知识点--Browserslist (基于官方文档翻译）](https://juejin.cn/post/6844903669524086797)

#### .editorconfig
编辑器的配置

#### .eslintrc.js
ESlint编程规范

#### babel.config.js
Babel配置 

#### LICENSE
LICENSE 开源软件协议

#### package.json

#### README

### 1.2 Yarn or Npm
首先安装node环境，node自带的npm包管理工具，不需单独安装。

虽然npm有nrm这样的切换镜像源，npm安装依赖包的速度快多了，但是npm有诸多的问题。比如：之前开发遇到package-lock.json冲突问题、奇怪的版本号... 听说新版的npm5.0修复很多问题，不过这次还是选用yarn。


```shell
## 全局安装yarn
npm install -g yarn
```

```shell
## 安装成功后，查看版本号：
yarn --version
```

```shell
## 初始化项目，生成package.json文件
yarn init
```

### 1.3 ElementUI搭建

#### 安装 Element
```shell
# Yarn 安装 Element-UI
yarn add element-ui
```

接着根据[Element官网-快速上手](https://element.eleme.cn/#/zh-CN/component/quickstart)教程，在项目中引入ElementUI。

#### 引入 Element
我们这里采用“按需引入”的方式，尽量的节约项目的体积。

首先，安装 babel-plugin-component：
```shell
yarn add babel-plugin-component -D
```


### 安装axios
```shell
yarn add axios
```

### 安装vue-router
```shell
yarn add vue-router
```

### 安装mock
```shell
yarn add mockjs
```

```shell
yarn add vite-plugin-mock -D
```
