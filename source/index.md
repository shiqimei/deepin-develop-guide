# 起步

## DTK 简介
DTK 全称 deepin-tool-kit，是 Deepin 基于Qt5开发的一整套UI图形库，包含一些工具类和大量的常用控件，方便统一地编写深度桌面和深度系列应用<sup><a href="#link1">1</a></sup>，主要的功能有：
- 提供单实例的接口，方便直接使用，不用造轮子
- 提供窗口移动、缩放等一系列函数
- 提供一大票美观的自绘控件

DTK 已于 2017 年 7 月完成重构<sup><a href="#link2">2</a></sup>，deepin-tool-kit 已被拆分成多个模块，包括 dtkcore、dtkwidget 和 dtkwm 等，其中 dtkwidget是控件库，包括所有系统和应用的控件、dtkcore是一些非控件的工具库函数<sup><a href="#link3">3</a></sup>。

## 安装

打开终端输入以下命令以安装 DTK 开发环境:

```sh
sudo apt update #更新软件源
sudo apt install qt5-default qttools5-dev-tools qt5-qmake g++ qtcreator -y #安装Qt开发套件和g++（如果已安装则无需安装）
sudo apt install libdtkbase-dev libdtkwidget-dev libdframeworkdbus-dev -y #安装dtk工具包
sudo apt install libdtkcore-dev libdtksettings-dev libdtksettingsview-dev libdtkutil-dev libdtkwidget-dev libdtkwm-dev -y
```



```bash
$ git clone https://github.com/zalando-incubator/hexo-theme-doc-seed.git <directory>
```

Go into the resulting directory and install dependencies:

```bash
$ npm install
```

Start the preview server locally with:

```
hexo s
```

> If you open your browser at http://localhost:4000 you should see the documentation website up and running.

## 参考链接

1. <a id="link1" href="https://www.jianshu.com/p/e871723f9460">深度桌面操作系统架构设计</a>
2. <a id="link2" href="https://github.com/linuxdeepin/deepin-tool-kit/issues/8">Deepin Tool Kit 重构 #8</a>
3. <a id="link3" href="https://bbs.deepin.org/forum.php?mod=viewthread&tid=146363&page=1#pid385967">请问dtk、dtkwidget、dtkcore之间是什么关系？</a>