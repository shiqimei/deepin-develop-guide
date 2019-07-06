# 起步

## 1.1 前言
《Deepin 开发指南》旨在帮助 Deppin 社区的开发者更快地投入进软件的开发过程中。看完本教程你将掌握以下内容:
1. 基于 VS Code + CMake 的 C++/Qt 开发环境的搭建与配置
2. 使用 VS Code 调试 C++/Qt 程序
3. 将二进制源代码打包成 deb

> 本教程假设你已经有了一定的 C++ 基础。如果你缺少 C++ 基础，啃一本 C++ 入门书籍(如《C++ Primer Plus》)是一个不错的选择。

## 1.2 部署开发环境
### 1.2.1 安装 Qt、g++、clang、dtk 和 CMake
在正式开始之前，我们需要安装一些必要的开发工具（如编译器、构建工具等），请打开终端输入下面的命令安装它们:
```sh
sudo apt update
sudo apt install qtcreator-dde qttools5-dev -y
sudo apt install g++ clang -y
sudo apt install libdtkcore-dev libdtkwidget-dev -y
sudo apt install libdtkcore-bin libdtksettings-dev libdtksettingsview-dev -y
sudo apt install cmake -y
```
### 1.2.2 安装 VS Code
本系列教程使用 VS Code 作为代码编辑器，你可以通过下面几种方式获取 VS Code:

1. 直接从官网下载安装
  打开 [https://code.visualstudio.com](https://code.visualstudio.com/) 下载最新版本的 deb 包后双击调用软件包管理器完成安装。
2. 使用 apt 安装
  打开终端输入以下命令
  ````bash
  sudo apt install vscode -y # 不推荐(源中版本过旧)
  ````


## 1.3 配置 VS Code
VS Code 是一款强大的可拓展的代码编辑器，借助它丰富的插件，我们可以配置个性化的 C++/Qt 程序的开发环境，这里是一些 `必须/建议` 安装的插件，请在正式开发之前安装好它们:

- <img src="https://ms-vscode.gallerycdn.vsassets.io/extensions/ms-vscode/cpptools/0.21.0/1548280626223/Microsoft.VisualStudio.Services.Icons.Default" height="25"> C/C++ <span style="color:white;background:#E1424D;margin-left:10px;padding: 2px 5px;border-radius:5px;">必须安装</span>
- 


## 1.4 用 CMake 构建 Qt 项目
在学习本节内容前，如果你不清楚什么是 CMake，请先看我们为你提供的 [CMake入门教程](cmake/cmake.html)。

CLion 使用 CMake 作为构建工具，使用 CLion 创建 Qt 项目一个较好的项目模板<sup><a href="#link1">1</a></sup>如下，建议新手创建 Qt 项目均按此模板创建。
### 项目目录结构
````bash
ProjectName               #项目目录
├── CMakeLists.txt      #项目根目录CMakeLists.txt配置文件
└── src                 #源码目录
    ├── CMakeLists.txt  #源码目录CMakeLists.txt配置文件
    └── main.cpp        #程序入口
````
### 模板内容
````cmake ProjectName/CMakeList.txt
cmake_minimum_required(VERSION 3.7)
project(Demo)
add_subdirectory(src)
````
````cmake ProjectName/src/CMakeLists.txt
cmake_minimum_required(VERSION 3.7)
set(TARGET_NAME Demo)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
file(GLOB_RECURSE SOURCES "*.cpp")
file(GLOB_RECURSE HEADERS "*.h")
file(GLOB_RECURSE FORMS "*.ui")
file(GLOB_RECURSE RESOURCES "*.qrc")
find_package(PkgConfig REQUIRED)
set(QT Core Gui Widgets Network DBus Sql)
find_package(Qt5 REQUIRED ${QT})
pkg_check_modules(3rd_lib REQUIRED
        dtkwidget dframeworkdbus
        )
add_executable(${TARGET_NAME} ${SOURCES} ${HEADERS} ${FORMS} ${RESOURCES})
target_include_directories(${TARGET_NAME} PUBLIC ${3rd_lib_INCLUDE_DIRS} )
target_link_libraries(${TARGET_NAME} ${3rd_lib_LIBRARIES} )
qt5_use_modules(${TARGET_NAME} ${QT})
set(CMAKE_INSTALL_PREFIX /usr)
install(TARGETS ${TARGET_NAME} DESTINATION bin)
````
````cpp ProjectName/src/main.cpp
/**
 * Deepin Tool Kit 模板代码
 */
#include <DApplication>
#include <DUtil>
#include <DMainWindow>
#include <DWidgetUtil>
#include <DLog>
#include <zconf.h>

DWIDGET_USE_NAMESPACE
        DCORE_USE_NAMESPACE
int main(int argc, char *argv[]) {
    DLogManager::registerConsoleAppender();
    DLogManager::registerFileAppender();
    DApplication::loadDXcbPlugin();
    DApplication app(argc, argv);
    app.setAttribute(Qt::AA_UseHighDpiPixmaps);
    const QString socket_path(QString("Demo_%1").arg(getuid()));
    if (app.setSingleInstance(socket_path)) {
        app.setTheme("light");
        app.loadTranslator();
        const QString descriptionText = QApplication::tr("A simple Qt Demo by CLion 2018.2 and CMake");
        const QString acknowledgementLink = "https://deepin.lolimay.cn";
        app.setOrganizationName("lolimay");
        app.setApplicationName("Demo");
        app.setApplicationDisplayName(QObject::tr("Demo"));
        app.setApplicationVersion("1.0.0");
        app.setProductName(QApplication::tr("Demo"));
        app.setApplicationDescription(descriptionText);
        app.setApplicationAcknowledgementPage(acknowledgementLink);

        DMainWindow window;
        window.setFixedWidth(600);
        Dtk::Widget::moveToCenter(&window);
        window.show();
        return app.exec();
    }
    qDebug() << "app has started";
    return 0;
}
````

<p class="button-outer"><a href="demo.html"><span class="button">创建Deepin示例应用 ➤</span></a></p>

## 参考链接
1. <a id="link1" href="https://blog.csdn.net/qq_32768743/article/details/80056316">【配置分享】CMake构建Qt</a>