# CMake入门

## 1.1 构建工具
由源文件生成最终的可执行程序这一过程称为[构建](https://stackoverflow.com/questions/15198725/build-or-compile)，完成这一过程的工具称为构建工具，最常用的构建工具是 make<sup><a href="#link1">1</a></sup>、qmake 以及我们即将介绍的 CMake。
当你的程序只有一个源文件时，直接就可以使用 `gcc` 命令编译它。但是，当项目中包含了多个源文件，用 `gcc` 命令去逐个编译就很容易产生混乱而且工作量巨大。于是，出现了 make。make 是最常用的构建工具，Makefile 是 make 的配置文件，make 可根据 Makefile 文件自动完成编译和链接最后生成可执行文件。Makefile 在一些简单的项目中可以人工手写，但是当项目非常大的时候，手写 Makefile 文件并不现实。

## 1.2 CMake简介
CMake作为更高级的构建工具，它并不直接构建出可执行文件，而是生成 make 工具所需要的 Makefile 文件。它允许开发者通过更简单的配置来定制整个编译流程，CMake的配置文件是 CMakeLists.txt。
使用 CMake 构建整个项目并生成可执行文件的完整流程是：
1. 编写 CMake 配置文件 CMakeLists.txt
2. 执行命令 `cmake path` 生成 make 工具所需要的 Makefile 文件。其中 `path` 是 CMakeLists.txt 所在的目录。
3. 使用 `make` 命令进行编译生成可执行文件

## 1.3 CMake的安装
在 Deepin 下安装 cmake 非常简单，只需打开终端
````shell
sudo apt install cmake -y #安装cmake
````
细心的同学可能会发现，在教程的 [起步 - 1.2.1 安装 Qt、g++、dtk 工具包、cmake](http://deepin.lolimay.cn/#1-2-%E9%83%A8%E7%BD%B2%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83) 一节中其实已经引导大家安装了 cmake，cmake 是使用 C++ 开发项目的首选构建工具。
## 1.4 CMake语法
CMake 的语法比较简单，由命令、注释（注释符是 #）和空格组成，CMake对大小写不敏感（建议命令全部小写以增加可读性），命令由命令名称、小括号和参数组成，参数之间使用空格进行分隔。CMake 的配置文件 CMakeLists.txt 一般在项目根目录下，下面是最简单的 CMakeLists.txt 示例：
````cmake
cmake_minimum_required(VERSION 3.8) #要求CMake的最低版本为3.8
project(demo) #指定项目名称为demo
add_executable(demo main.c) #指定生成的可执行文件名和所需源文件 格式: add_executable(生成的可执行文件名 源文件1 源文件2 源文件3 ...)
````

<p class="button-outer"><a href="cmake-practice.html"><span class="button">CMake实战 ➤</span></a></p>

## 参考链接
1. <a id="link1" href="http://www.ruanyifeng.com/blog/2015/02/make.html">Make 命令教程 - 阮一峰</a>
2. <a href="https://www.zhihu.com/question/27455963">make makefile cmake qmake都是什么，有什么区别？ - 知乎问答</a>