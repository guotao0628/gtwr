# gtwr_portal

## 项目概述

这个项目的预期是希望能够搭建一个门户原型实现GTWR计算，包括如下几个功能：

* 支持登录，用户可选择匿名登录或实名注册

* 支持用户自定义GTWR计算的源数据类型，包括图片？Excel/csv表格？json/geojson数据？

* 支持数据预览以及计算前对源数据的简单统计及可视化

* 支持用户自定义计算参数

* 支持用户对计算结果的预览、简单统计以及可视化

## 项目工具

项目门户搭建过程中计划使用如下的工具或框架：

* Vue.js渐进式前端开发框架

使用Vue.js搭建前端框架，Vue教程[戳这里](https://cn.vuejs.org/)

* Github & Git配合的版本管理

GitHub是项目的远程仓库，存放用于共享的项目文件；Git用于提交更新文件，方便多人合作进行版本更新。

已经在GitHub搭建了仓库，[gtwr_vue仓库地址](https://github.com/GTWR/gtwr_vue)，Git和GitHub的关系理解教程，[戳这里](http://blog.jobbole.com/111187/)。

* Express发布数据查询服务

用Express在后端发布数据查询服务，Express教程[戳这里](http://www.expressjs.com.cn/)，后期的GTWR计算会涉及到其他的接口设计，先不做考虑。

* SASS扩展语言

基于SASS定义CSS样式，当然还是可以用原始的CSS文件定义样式，自由选择，SASS的教程[戳这里](https://www.sass.hk/)

* Echarts

## 项目配置

### 下载安装node

* node安装教程，[戳这里](http://www.runoob.com/nodejs/nodejs-install-setup.html)，建议安装最新版本。
* 下面会用到npm进行node相关工具的安装，npm随node一起下载，无需单独安装，npm的教程和功能理解，[戳这里](http://www.runoob.com/nodejs/nodejs-npm.html)

### 安装cnpm

* 国内运行npm较慢，且容易出现各种各样的问题，因此一般使用npm的淘宝镜像进行安装，即cnpm
```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### 下载安装git

* git下载地址，[戳这里](https://gitforwindows.org/)
* git安装教程，[戳这里](https://jingyan.baidu.com/article/020278117cbe921bcc9ce51c.html)

### 克隆项目文件

* 在你喜欢的路径下，单机右键选择Git Bash Here
* 在命令面板下输入命令，将存储在远程仓库的项目文件拷贝在本地
```
git clone https://github.com/GTWR/gtwr_vue.git
```
* 你就可以看到在你喜欢的路径下出现了gtwr_vue这个文件

### 运行项目

* 安装项目依赖包：在cmd中选择项目所在路径

```
cnpm install

npm run dev
```

* 浏览器自动打开端口为8080的页面

### 提交版本更新

* 在项目地址下，打开Git Bash Here

```
$ git checkout -b dev //切换本地分支
$ git commit -m "update revise" //提交更新到暂存区
$ git push origin dev //提交分支暂存到远程仓库
```

* 如果提交过程存在冲突，自行百度Git相关命令解决，建议首次使用git提交前进行文件备份！！！

## 项目更新日志

### 2018.3.25

负责人： 李晨悦

工作内容：

* 登录页面底图调用高德地图API实现缩放功能

* 应用案例滚动展示窗，实现应用案例图片的轮播，采用父子组件实现，子组件在Carousel.vue中实现，然后在login.vue中调用。应用案例图片采用echart的简单地图截图。

负责人：张敏

工作内容：

* 设计实现主体页面布局，及其样式定义，页面中包含参数自定义面板、数据选择面板、地图展示面板、数据表格面板

* 实现了各面板中简单的组件，例如数据选择列表实现，参数自定义面板输入框实现，以及基础底图加载

----------------------------------------------

### 2018.4.8

负责人：张敏

工作内容：

* 新增Vuex组件，用于管理项目中共享的数据状态

* 新增数据预览、数据说明两个功能按钮，分别用于预览数据内容\数据在地图上的分布、元数据内容的具体说明

* 数据预览部分，能够实现数据在地图上的显示、对应的数据列表的更新

* 参数定义模块可以进行计算，计算结果设置图表展示、计算日志、精度评价、其他四个模块，其中计算日志和其他仍未空白；图表展示中包含2D和3D两种类型的图表，可供选择


负责人：李晨悦

工作内容：

* 元数据信息

* 其他具体信息具体

----------------------------------------------

### 2018.4.8

负责人：张敏

工作内容：

* 修改优化平台首页内容，在首页中添加动态的正态分布效果
* 实现数据勾选，弹出参数选择框，同步更新参数选择到选择面板和参数设置面板

### 2018.4.22

负责人：李晨悦

工作内容：
* 修改数据选择与参数设置内容，添加勾选框与计算进度条，并添加了隐藏显示数据选择列表的功能；

* 但是还有一些小bug，以及数据选择与参数联动效果没有做出来

### 2018.4.22

负责人：@我最胖！

工作内容：

* 实现了数据预览模块中表头固定，表体滚动的功能

----------------------------------------------

## 项目任务安排

具体分工安排：

* 张敏：
    * 实现图表展示模块中地图与数据图表之间的联动
    * 实现登录首页轮播组件与三维动态可视化组件的分离
* 李晨悦：
    * 实现数据预览模块中地图与数据表格之间的联动，即点击地图中的图块，数据表格滚动到对应数据行<br/>
    ===>参考mapbox example中类似的实现
* @我最胖！：
    * 实现计算日志模块，代码打印结束之后页面切换到图表展示模块<br/>
    ===>熟悉vue-router，以及JS代码
    * 安装git，实现自己的本地修改实时上传，不懂的即时问
    * 如果可以，尽量实现参数设置模块滚动条和开始计算按钮的合并，也就是说点击开始计算，按钮宽度变大，利用CSS的animation动画效果在按钮上显示进度<br/>
    ===>熟悉CSS3的animation transition等内容
代码书写要求
* 要有注释，注释内容包括JS代码中函数的主要功能，甚至函数中不同的部分的主要功能，如果HTML中DOM较多（div等标签较多）可以在HTML的DOM中注释每个模块的功能
* 代码格式要整齐，div的排列要有换行，按照树形结构去整理；js代码函数之间空格换行也要尽量整齐，规范



