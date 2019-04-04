---
title: webpack
date: 2018-03-02 10:22:44
tags: JavaScript
---

------

<p style='text-decoration: line-through;'>webpack是一个模块化打包工具，所有的配置放在配置文件里面，最终可以打包到指定文件中，比如样式，图片通过webpack都可以打包到一个js文件中</p>

(2018.10.9修改)

webpack是一个模块化打包工具, 通过配置文件，将不能直接运行在浏览器上的代码，通过编译打包为可执行的JavaScript、CSS、HTML，适合浏览器运行，其主要工作内容包括

代码转换：Jsx编译成Js，SCSS编译成CSS
文件优化：压缩代码，压缩合并图片, 分包等
代码分割：提取公共代码，提取首屏不需要加载的代码
模块合并：将多个模块打包成一个文件
自动刷新：热加载
代码校验：eslint
自动发布：

### 1. 对比webpack与gulp在使用中的优缺点
> gulp优势：
> * 上手简单
> * 轻量的，需要什么功能,添加什么功能
> * 插件多，估计你想要的都可以在社区找到
> * 依赖小，各个任务之间比较独立
> gulp劣势：
> * 任务多时，维护起来比较麻烦


> webpack优势：
> * 容易做SPA
> * 以entry为入口文件，模块化加载所有引用到的文件
> * 插件丰富
> gulp劣势：
> * 配置惊人

<!--more-->
### 2. webpack 核心配置
mode 环境
entry 入口文件
output 编译后的文件
module 编译需要的loader
plugins 插件

### 3. loader

1. css loader
style loader
css loader
less-loader/sass-loader

```javascript
module.exports = {
  ...
  module: {
    rules: [
      {
        test: /\.jsx$/,
        use: {
            loader: "./loader/my-loader",
        },
        exclude: /node_modules/
      }
    ]
  }
}
```
./loader/my-loader
```javascript
/*
 * 固定格式
 * source 当前正在编译的js代码文件
*/
module.exports = function (source) {
  // 这里写具体需要做的时候
  // 下面一行代码是给静态资源加全路径和版本戳
  return source.replace(/(['"(\\])(\/static\/[^'"()\s\\]+)(['")\\])/g, `$1https://www.xx.com$2?v=${Date.now()}$3`)
}

```

### 4. 自定义plugins


### 5. devtool

source map 提供打包后文件到源文件的映射

**webpack配置文件中devtool的设置：**
>* 如果不设置，打包成一个文件 比较适合生产
>* eval 不生成sourcemap文件 生成多个模块 模块文件末尾有源文件路
>* cheap-eval-source-map 好像和eval差不多
>* cheap-module-eval-source-map 看起来像是源文件 
>* eval-source-map 和上面的有啥区别？
>* cheap-module-source-ma 和cheap-module-eval-source-map有啥区别
>* cheap-source-map eval 有啥区别？
>* inline-cheap-source-map 单个模块 
>* inline-cheap-module-source-map 源码
>* source-map  源码
>* inline-source-map 源码
>* hidden-source-map 编译出来的文件
>* nosources-source-map 看不到文件