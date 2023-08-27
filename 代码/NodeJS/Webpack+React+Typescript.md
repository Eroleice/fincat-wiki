---
title: Webpack+React+Typescript
description: 更优雅地写代码
published: true
date: 2023-08-27T11:35:57.944Z
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
```
dist/
public/
		index.html
src/
		components/
    		Footer.tsx
        Footer.scss
		entrypoint.tsx
    App.tsx
```
上述结构中，`dist/`是最终的程序输出目录，包含网站本身的index.html、js文件和css文件。`public/`包含了所有不需要编译而直接复制到`dist/`的内容，例如我们上方的`index.html`最终就会**原封不动**地放入`dist/`目录下。而`src/`目录便是我们代码的存储位置了，里面的`entrypoint.tsx`将会是webpack打包时运行的文件。

> 由于`public/index.html`是**原封不动**地被复制到`public/`目录下，里面有关调用js文件和css文件（包括webpack生成地js文件和css文件！）都需要手动写入！
{.is-warning}

## 创建index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="bundle.css" />
    <title>Document</title>
</head>
<body>
    <div id="root"></div>
    <script src="bundle.js"></script>
</body>
</html>
```

> 如果是在使用`Visual Studio Code`，可以新建`index.html`后，在编辑器中按`shift+1`，即可自动获得一份基础的html模板，你仍然需要手动添加上面代码中的第7、11、12行。
{.is-info}

## 创建Footer.tsx
```ts
import "./Footer.scss";

export default function Footer() {
  return (
    <footer>
      <a href="#">A Footer Link</a>
    </footer>
  );
}
```

## 创建App.tsx
```ts
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

const rootElement = document.getElementById("root");

// New as of React v18.x
const root = createRoot(rootElement!);

root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

## 创建entrypoint.tsx
```ts
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

const rootElement = document.getElementById("root");

// New as of React v18.x
const root = createRoot(rootElement!);

root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```