# Deepin开发指南

# 前言
[《Deepin 开发指南》](http://deepin.lolimay.cn)旨在帮助 Deppin 社区的开发者更快地投入进软件的开发过程中，按计划，该系列教程将会包括以下内容: 开发环境的搭建与配置、深度原生应用源码分析、Deb 与 Flatpak 打包教程以及Deepin Tool Kit API手册等。

本教程假设你已经有了一定的 C++ 基础，如果对 C++ 一无所知的话，建议先从学习 C++ 开始，[《C++ Primer Plus 第6版 中文版》](https://www.baidu.com/s?wd=c%2B%2B%20prime%20plus)是你最好的选择。

# 目录

## [新手上路](http://deepin.lolimay.cn)
-  [起步](http://deepin.lolimay.cn)
    - [1.1 前言](http://deepin.lolimay.cn/#1-1-%E5%89%8D%E8%A8%80)
    - [1.2 部署开发环境](http://deepin.lolimay.cn/#1-2-%E9%83%A8%E7%BD%B2%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)
    - [1.3 配置CLion](http://deepin.lolimay.cn/index.html#1-3-%E9%85%8D%E7%BD%AECLion)
    - [1.4 用CMake构建Qt项目](http://deepin.lolimay.cn/index.html#1-4-%E7%94%A8-CMake-%E6%9E%84%E5%BB%BA-Qt-%E9%A1%B9%E7%9B%AE)
    - [参考链接](http://deepin.lolimay.cn/index.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)
- [创建Deepin示例应用](http://deepin.lolimay.cn/intro/demo.html)
    - [2.1 创建一个空项目](http://deepin.lolimay.cn/intro/demo.html#2-1-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E7%A9%BA%E9%A1%B9%E7%9B%AE)
    - [2.2 对原有项目进行改造](http://deepin.lolimay.cn/intro/demo.html#2-2-%E5%AF%B9%E5%8E%9F%E6%9C%89%E9%A1%B9%E7%9B%AE%E8%BF%9B%E8%A1%8C%E6%94%B9%E9%80%A0)
    - [2.3 重载并运行项目](http://deepin.lolimay.cn/intro/demo.html#2-3-%E9%87%8D%E8%BD%BD%E5%B9%B6%E8%BF%90%E8%A1%8C%E9%A1%B9%E7%9B%AE)
    - [其它意外情况](http://deepin.lolimay.cn/intro/demo.html#2-4-%E5%85%B6%E5%AE%83%E6%84%8F%E5%A4%96%E6%83%85%E5%86%B5)
- [CMake入门教程](http://deepin.lolimay.cn/intro/cmake/cmake.html)
    - [CMake入门](http://deepin.lolimay.cn/intro/cmake/cmake-base.html)
    - [3.1 构建工具](http://deepin.lolimay.cn/intro/cmake/cmake-base.html#3-1-%E6%9E%84%E5%BB%BA%E5%B7%A5%E5%85%B7)
    - [3.2 CMake简介](http://deepin.lolimay.cn/intro/cmake/cmake-base.html#3-2-CMake%E7%AE%80%E4%BB%8B)
    - [3.3 CMake的安装](http://deepin.lolimay.cn/intro/cmake/cmake-base.html#3-3-CMake%E7%9A%84%E5%AE%89%E8%A3%85)
    - [3.4 CMake语法](http://deepin.lolimay.cn/intro/cmake/cmake-base.html#3-4-CMake%E8%AF%AD%E6%B3%95)
    - [参考链接](http://deepin.lolimay.cn/intro/cmake/cmake-base.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)
    - [CMake实战](http://deepin.lolimay.cn/intro/cmake/cmake-practice.html)（编写中）
    - [3.5 构建单个源文件](http://deepin.lolimay.cn/intro/cmake/cmake-practice.html#3-5-%E6%9E%84%E5%BB%BA%E5%8D%95%E4%B8%AA%E6%BA%90%E6%96%87%E4%BB%B6)
    - [参考链接](http://deepin.lolimay.cn/intro/cmake/cmake-practice.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)
- [Deepin Tool Kit]()（计划）
## [API手册]()
- [Deepin Tool Kit API]()（计划）
## [附录]()
- [desktop文件入门](http://deepin.lolimay.cn/booklet/desktop.html)
    - [desktop文件模板](http://deepin.lolimay.cn/booklet/desktop.html#desktop%E6%96%87%E4%BB%B6%E6%A8%A1%E6%9D%BF)
    - [应用示例](http://deepin.lolimay.cn/booklet/desktop.html#%E5%BA%94%E7%94%A8%E7%A4%BA%E4%BE%8B)
    - [添加到启动器](http://deepin.lolimay.cn/booklet/desktop.html#%E6%B7%BB%E5%8A%A0%E5%88%B0%E5%90%AF%E5%8A%A8%E5%99%A8)
    - [Categories](http://deepin.lolimay.cn/booklet/desktop.html#Categories-%E5%8F%82%E6%95%B0)
    - [附表：Categories对照表](http://deepin.lolimay.cn/booklet/desktop.html#%E9%99%84%E8%A1%A8%EF%BC%9ACategories-%E5%AF%B9%E7%85%A7%E8%A1%A8)
    - [参考链接](http://deepin.lolimay.cn/booklet/desktop.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)
- [deepin常用路径](http://deepin.lolimay.cn/booklet/path.html#%E5%BA%94%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B7%AF%E5%BE%84)
    - [应用数据路径](http://deepin.lolimay.cn/booklet/path.html#%E5%BA%94%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B7%AF%E5%BE%84)
    - [启动器图标所在路径](http://deepin.lolimay.cn/booklet/path.html#%E5%90%AF%E5%8A%A8%E5%99%A8%E5%9B%BE%E6%A0%87%E6%89%80%E5%9C%A8%E8%B7%AF%E5%BE%84)
    - [桌面路径](http://deepin.lolimay.cn/booklet/path.html#%E6%A1%8C%E9%9D%A2%E8%B7%AF%E5%BE%84)
    - [参考链接](http://deepin.lolimay.cn/booklet/path.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)
- [以管理员身份运行你的应用](http://deepin.lolimay.cn/booklet/polkit.html)
    - [方法一 sudo命令](http://deepin.lolimay.cn/booklet/polkit.html#%E6%96%B9%E6%B3%95%E4%B8%80-sudo%E5%91%BD%E4%BB%A4)
    - [方法二 polkit](http://deepin.lolimay.cn/booklet/polkit.html#%E6%96%B9%E6%B3%95%E4%BA%8C-polkit)
    - [参考链接](http://deepin.lolimay.cn/booklet/polkit.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)

# 参与写作&校对
1. Fork 此仓库
2. 用你趁手的 Markdown 编辑器编辑 **source** 目录下的`.md`源文件
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
    ├── cmake #cmake文件夹
    ├── ...
    └── dtk.md
````
可自由在 **source/** 文件夹下创建文件夹和 Markdown 文件，添加一个新的教程页需要在 **navigation.yaml** 文件中指定它在左侧导航栏中的位置

# 贡献者
[<img alt="nujhong" src="https://avatars3.githubusercontent.com/u/32427260?s=460&v=4&s=117" width="117">](https://github.com/lolimay)[<img alt="zhangzhengyi12" src="https://avatars3.githubusercontent.com/u/18530271?s=460&v=4&s=117" width="117">](https://github.com/ziqiangxu)