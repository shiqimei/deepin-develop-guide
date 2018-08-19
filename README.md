# Deepin开发指南

# 前言
[《Deepin 开发指南》](http://deepin.lolimay.cn)旨在帮助 Deppin 社区的开发者更快地投入进软件的开发过程中，按计划，该系列教程将会包括以下内容: 开发环境的搭建与配置、深度原生应用源码分析、Deepin Tool Kit API手册等。

# 目录
本文档包括以下内容：
## [新手上路](http://deepin.lolimay.cn)
-  [起步](http://deepin.lolimay.cn)
    - [1.1 前言](http://deepin.lolimay.cn/#%E5%89%8D%E8%A8%80)
    - [1.2 部署开发环境](http://deepin.lolimay.cn/#%E9%83%A8%E7%BD%B2%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)
    - [1.3 配置CLion]()
    - [1.4 用CMake构建Qt项目]()
    - [参考链接]()
- [创建Deepin示例应用]()
    - [2.1 创建一个空项目]()
    - [2.2 对原有项目进行改造]()
    - [2.3 重载并运行项目]()
    - [其它意外情况]()
- [CMake入门教程]()
    - [CMake入门]()
        - [3.1 构建工具]()
        - [3.2 CMake简介]()
        - [3.3 CMake的安装]()
        - [3.4 CMake语法]()
        - [参考链接]()
    - [CMake实战]()
        - [3.5 构建单个源文件]()
- [Deepin Tool Kit]() (计划)
## [API手册]()
- [Deepin Tool Kit API]() (计划)

# 参与写作&校对
1. Fork 此仓库
2. 用你趁手的Markdown编辑器编辑 **source** 下的`.md`源文件
3. Pull Request 到这个仓库

仓库下的 **public/** 文件夹是 [《Deepin 开发指南》](http://deepin.lolimay.cn) 的源码，是 [Hexo](http://www.hexo.io) 根据 **source/** 文件夹的内容动态生成的，不要修改此目录下的文件，会被覆盖掉。

## **source/** 文件夹的目录结构
````
.
├── _data
│   └── navigation.yaml #左侧导航栏配置文件
├── images
│   ├── favicon.ico #站点favicon文件
│   └── logo.png #站点logo文件（废弃）
├── index.md #站点主页
└── intro
    ├── cmake.md
    └── dtk.md
````
可自由在 **source/** 文件夹下创建文件夹和 Markdown 文件，添加一个新的教程页需要在 **navigation.yaml** 文件中指定它在左侧导航栏中的位置