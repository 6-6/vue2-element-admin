# vue2-element-admin
基于 ElementUI + Vue2 后台管理系统，将之前开发常用的前端基建整合出教程，以便于以后可以快速入手。

## 一、前期准备
前期需要准备：node环境配置 > yarn包管理 > UI框架 > webpack配置 > Jest单元测试 > Mock模拟数据 > Git版本管理配置 等等。 

### 1.1 Yarn or Npm
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
## 初始化项目，生成package.json文件（使用了Vue-Cli脚手架安装，这一步可省略）
yarn init
```

### 1.2 创建Vue项目
通过官网的[Vue CLI 安装](https://cli.vuejs.org/zh/guide/installation.html)教程，按照步骤即可。

```shell
# 全局安装
yarn global add @vue/cli
```

```shell
# 查看Vue CLI脚手架的版本
# 当前使用版本 @vue/cli 4.5.15
vue --version
```

```shell
# 通过脚手架创建项目
vue create vue2-element-admin
```

```shell
# 基本上都要用到，所以我这里选择了第一个
? Please pick a preset: (Use arrow keys)
> vue2.0 ([Vue 2] dart-sass, babel, router, vuex, eslint)
  Default ([Vue 2] babel, eslint)
  Default (Vue 3) ([Vue 3] babel, eslint)
  Manually select features
```

### 1.3 项目结构
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
**(1) 介绍：**
browserslist 是在不同的前端工具之间共用目标浏览器和 node 版本的配置工具。主要被以下工具使用：
* Autoprefixer
* Babel
* postcss-preset-env
* eslint-plugin-compat
* stylelint-unsupported-browser-features
* postcss-normalize

举例来说，项目创建的时候，需要通过这个文件确认兼容的浏览器版本。

为何需要确认版本呢？跟以上的工具相关。

我们知道Bebal的作用是是将ES6的语法转换为ES5，兼容低版本浏览器。那么就需要提供项目所兼容浏览器版本的范围，以便于Babel确认哪些ES6不需要转换，哪些需要转换ES5。

**(2) 原理：**
关于前端打包体积与垫片关系，我们有以下几点共识:

1. 由于低浏览器版本的存在，垫片是必不可少的
1. 垫片越少，则打包体积越小
1. 浏览器版本越新，则垫片越少

babel，在 @babel/preset-env 中使用 core-js 作为垫片（可以理解为兼容性的核心代码）

browserslist 的原理： browserslist 根据正则解析查询语句，对浏览器版本数据库 caniuse-lite 进行查询，返回所得的浏览器版本列表。

**(2) 配置：**
```javascript
> 1%
last 2 versions
not dead
```

**参考文章：**
* [前端工程基础知识点--Browserslist (基于官方文档翻译）](https://juejin.cn/post/6844903669524086797)
* [你了解 Browserslist 吗](https://juejin.cn/post/7033765500228206622)

#### .editorconfig
**(1) 介绍：**
editorconfig 跨IDE保持编码风格一致的配置文件。

**(2) 安装：**
webstorm 自带支持 editorconfig ，而 vscode 需要下载插件 EditorConfig for VS Code 。修改下配置文件 ````indent_size = 2````，可以看到编辑器立即生效了，Tab缩进变为了2个空格。

**(3) 配置：**
```javascript
# 顶层editorconfig文件标识
root = true

# 针对所有文件适用
[*]

indent_style = space # 缩进符使用的风格 （tab ｜ space）
indent_size = 4 # 缩进大小
end_of_line = lf # 控制换行类型(lf | cr | crlf)
charset = utf-8 # 编码格式
trim_trailing_whitespace = true #行开始是不是清除空格
insert_final_newline = true #文件最后添加空行

[*.md]
trim_trailing_whitespace = false
```

**参考文章：**
* [editorconfig + prettier + Eslint 规范化](https://juejin.cn/post/6944320742687408141)

#### .eslintrc.js
**(1) 介绍：**
````.eslintrc.js```` 是 ````ESlint```` 的配置，所以必须从 ````ESlint````开始了解。

JavaScript 是一个动态的弱类型语言，在开发中比较容易出错。因为没有编译程序，通常需要在执行过程中不断调试。

````ESLint```` 是一个集代码审查和修复的工具。内置了一些规则，也可以自定义规则，来限制代码的合法性和风格。


**(2) 配置：**
ESLint 有两种配置方式：

1. ````ESLint```` 采用逐级向上查找的方式查找 ````.eslintrc```` 文件，当找到带有 ````"root": true```` 配置项的 ````.eslintrc```` 文件时，将会停止向上查找。
2. 在 ````package.json```` 文件里的 ````eslintConfig```` 字段进行配置。

VSCode ESLint插件配置：

1. 安装 ````VSCode```` 的 ````ESLint```` 和 ````vetur```` 插件
2. 为项目安装 ````ESLint```` 包，````Vue-CLI```` 创建项目时，我们已经选择了所以无需安装。
3. 在项目的根目录下检查有无 ````.eslintrc.js```` 配置文件，无就自己创建
4. ````VSCode```` 更改 ````ESLint````插件的配置， 首选项 > 设置 > ````settings.json````（不同版本配置项有可能会不一样）：

```json
// 每次保存的时候将代码按eslint格式进行修复
"editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
},
// 用eslint的规则检测以下格式文件
"eslint.validate": [
    "javascript",
    "javascriptreact",
    "vue",
    "html"
],
```

修改项目文件试一下，````CTRL+S```` 保存之后确实会自动格式化代码，那么就说明成功了。

**(3) 一键修复项目格式：**
项目的文件比较多的情况下，单独去保存比较麻烦，所以需要命令一键处理项目中的问题。

把校验命令加到 package.json

```json
{
    "scripts": {
        "lint": "npx eslint --ext .js,.jsx,.vue src",
        "lint:fix": "npx eslint --fix --ext .js,.jsx,.vue src",
    }
}
```

```shell
# 将error显示在终端中
yarn lint
# 修复这些错误
yarn lint:fix
```

**(4) 过滤一些不需要校验的文件：**
例如像是JQuery.min.js这种第三方插件，我们不需要对其进行校验，所以我们需要 ````.eslintignore```` 文件来配置，告诉 ESLint 校验的时候忽略它们：

**参考文章：**
* [十分钟了解 ESLint 配置 && 编写自定义 ESLint 规则](https://juejin.cn/post/6844903903964692494)
* [ESLint 开始，说透我如何在团队项目中基于 Vue 做代码校验](https://juejin.cn/post/6974223481181306888)

#### babel.config.js
Babel配置 

#### LICENSE
LICENSE 开源软件协议

#### package.json

#### README

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
