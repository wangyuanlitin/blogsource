---
title: 基于Antd Pro搭建的后台管理平台
date: 2019-04-03 13:47:14
tags: JavaScript
---

------

纯后台页面及操作，主要面向公司内部人员及部分B端用户，界面要求不高，但是要简单、整洁

### 一、 前端框架选择考虑
1. 开发时间大概在一个月左右
2. 不希望后期因为框架基础问题有比较大的调整
3. 只有两个前端冲刺，两个人分别有Vue、React经验，交叉较少
4. 不要求UI，但是不能太丑
5. 可能还要有多余时间来做些别的技术调研

选定React后，拿什么来搭建呢？又面临几个问题
  <!--more-->
1. 自己写webpack配置文件
2. create-react-app
3. 选择使用Antd Pro

自己写？不想写，写过一次就不想再写第二次了，不想每次都上来造轮子，会写就行了
create-react-app？不想用，用过一次就行了，不想每次都用，
Antd Pro？从github直接安装脚手架代码，我*，太多了，不想看，我们业务还算简单，要弄这么大个东西吗？时间这么紧，不想学啊

心理活动这么多，也花了三天左右来学习Antd Pro，中间一度要放弃，选择更加简单的create-react-app，但是又回来了，因为create-react-app在我看来就是帮我写了webpack的编译文件，其他东西其实也用不到，还要自己再加样式库，太麻烦，后续可能还要自己加状态容器，有点儿麻烦

最终选择Antd Pro，虽然前期学习多，但是通过几天的调研，至少在用上没什么问题

进入正题：
### 二、 Antd Pro有什么
1. umi 各个环境的编译、打包，目录约定，约定式路由，Link跳转
2. dva
3. Antd | Antd Pro
4. mock api
5. 测试

满足开发所有要求，但是从github获取的脚手架改动起来也是真心的累，如果刨去所有的逻辑，只是一个空项目还是很不错的

至于大家都是大，还需要我再看看大在什么地方，后续再更新

### 三、配置
1. 从github仓库直接安装最新的脚手架代码，安装依赖、启动服务、编译参照官方文档
2. 简化后的目录结构
<img src='/assets/images/mulu.png' style="width: 500px" />
简化后的，主要保留了config、mock、e2e、models部分以及一些代码格式化工具
去掉了图表、ts、还有些用不到的配置信息
3. 各个配置文件
config/router.config.js 路由配置信息
mock/ 注意拆分文件，一个model一个mock文件，mock数据
src/components 基本通用组件，非通用组件不建议放在这里
src/e2e 页面测试，看起来觉得没必要，前端页面测试略微复杂，页面总是变动，测试dom有没有，url跳转正不正确，没什么必要
src/models 数据请求、reducer state存储，其中effects用来请求数据，异步操作，reducers更新state
src/pages 对应router下的页面
src/services 封装api接口
src/utils 工具方法

### 四、各个部分怎么使用？