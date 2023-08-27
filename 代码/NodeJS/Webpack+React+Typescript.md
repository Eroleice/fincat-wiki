---
title: Webpack+React+Typescript
description: 更优雅地写代码
published: true
date: 2023-08-27T11:06:43.552Z
tags: 
editor: markdown
dateCreated: 2023-08-27T11:06:43.552Z
---

# What is ...
## Webpack
> **webpack** is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.

Webpack用于将写好地JS代码按指定规则进行打包，webpack会从一个或多个entry point开始运行，并将运行中的所有import库一并打包（或要求不打包指定库），最终你会获得一个打包了所有依赖的、充分压缩的JS文件。

## React
> **React** apps are made out of components. A component is a piece of the UI (user interface) that has its own logic and appearance. A component can be as small as a button, or as large as an entire page.

React等于将HTML的页面实现了面向对象编程。

## Typescript
> TypeScript is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.

Typescript是Javascript的超集，可以对参数赋予强类型，可以定义借口结构，可以进行编译随时发现代码运行可能的问题而不必等到出了BUG再排障。

# 软件版本
- 
- 
- Typescript 5.2

# 构建一个基于它们的网站项目

## 建立项目（NPM）
```
mkdir wrt-program
cd wrt-program
npm init -y
```


## 安装依赖库

```
npm install react react-dom
npm install -D @types/node @types/react @types/react-dom @types/copy-webpack-plugin
npm install -D typescript ts-loader webpack webpack-cli copy-webpack-plugin style-loader css-loader ts-node webpack-dev-server
```

## 搭建项目结构
- dist/
- public/
		- index.html
- src/
		- components/
    		- Header.tsx
        - Header.css
    		- Footer.tsx
        - Footer.css

