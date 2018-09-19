---
title: Webpack Source Map
date: 2018-09-19 11:30:41
tags: JavaScript
---

------

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