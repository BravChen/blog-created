---
title: webpack 的使用
date: 2019-08-28 23:02:51
categories:
  - 前端
tags:
  - 命令行
---

部分命令可能会有些过时，所以要多看官方文档

## 安装 node-sass

搜索：node sass github

github官网：https://github.com/sass/node-sass

命令行输入：

```
npm install node-sass -g
```

> `-g` 表示全局安装

**全局安装与局部安装的区别**

- 全局安装的命令会将插件安装在全局目录中 (包含在$PATH中)，不论在哪个目录下都可以调用

- 局部安装只能在当前路径使用该命令

### 使用

查看版本号

```
node-sass -v
```

**sass 的用法**

1. 更改CSS文件后缀为： `scss` 

   命令行中的写法：`mv style.css style.scss`

2. 使用 sass 编译：`node-sass style.scss style.css`



也可以使用 scss 语法书写代码：

```scss
div { color: red;
    > ul { font-size: 16px;
        > li { border: 1px solid #000;
            > a { font-weight: bold; }
        }
    }
}
```

再运行 `node-sass style.scss style.css` 后编译的语法：

```css
div {
  color: red; }
  div > ul {
    font-size: 16px; }
    div > ul > li {
      border: 1px solid #000; }
      div > ul > li > a {
        font-weight: bold; }
```

这样就是编译后的 CSS 了

**自动化编译**

在先前的命令后添加 ` -w 需要编译的文件名` 例如： 

```
node-sass style.scss style.css -w style.scss
```

将目录中所有scss文件自动化编译：

```
node-sass src/css/ -o dist/css -w
```

这样代码就会实时编译了，不需要每次更改都去执行先前的命令

**科普 scss 的 由来**

sass 语法 (被前端程序猿看不懂) ：

```sass
body
	p
		color: red
```

于是编译为 scss 语法 (被前端程序猿看懂的) ：

```scss
body p {
  color: red; }
```

## 安装 babel

1. 官网的安装教程：https://babeljs.io/docs/en/usage

2. 安装后点击CLI查看命令行教程：https://babeljs.io/setup#installation

> 功能：为代码兼容IE8

### 使用

```
./node_modules/.bin/babel js -d dist --watch
```

> `--watch` 表示即时编译，这样就不需要每次更改源文件后执行一次编译，它会监听源文件，变动就会自动编译

自动化编译文件夹内所有js

```
./node_modules/.bin/babel src/js/ -d dist/js/ --watch
```

**前端目录分类**

- src  ---  全称 source 表示未经翻译优化的源代码
- dist   ---   全称 distribution 表示要发布的代码
- vendors   ---   名字就是全称 表示第三方代码
- node_modules   ---   表示第三方包


## webpack 教程
官网安装教程：[Getting Started](https://webpack.js.org/guides/getting-started/)
中文版教程：[起步 | webpack 中文网](https://www.webpackjs.com/guides/getting-started/)
首先运行

```
npm init -y
```

然后安装

```
npm install webpack webpack-cli --save-dev
```

添加一个配置文件 **webpack.config.js**

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

运行

```
npx webpack
```

## 自动化提交文件

自动复制修改后的文件(主要用于不需要编译的 html 文件和 img 文件)

谷歌搜索：watch cli

安装

```
npm i -g watch-cli
```

安装后执行命令

```
watch -p "src/index.html" -c "cp src/index.html dist/index.html"
```

> 将 src 目录下的 index.html 文件自动化编译到 dist 目录下的 index.html