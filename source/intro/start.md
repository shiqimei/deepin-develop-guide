# 起步

## 1.1 前言
《Deepin 开发指南》旨在帮助 Deppin 社区的开发者更快地投入进软件的开发过程中，按计划，该系列教程将会包括以下内容: 开发环境的搭建与配置、深度原生应用源码分析、Deb 与 Flatpak 打包教程以及Deepin Tool Kit API手册等。

本教程假设你已经有了一定的 C++ 基础，如果对 C++ 一无所知，建议先从学习 C++ 开始，[《C++ Primer Plus 第6版 中文版》](https://www.amazon.com/C-Primer-Plus-Sixth-Chinese/dp/7115279462/ref=sr_1_1?s=books&ie=UTF8&qid=1534737175&sr=1-1&keywords=C%2B%2B+Primer+Plus+%286th+Edition%29++Chinese)（请自行在淘宝、京东上购买）是你最好的选择。

## 1.2 部署开发环境
### 1.2.1 安装 Qt、g++、dtk 工具包、cmake
打开终端输入以下命令
```sh
sudo apt update #更新软件源
sudo apt install qtcreator-dde qttools5-dev g++ -y #安装Qt和g++
sudo apt install libdtkcore-dev libdtkwidget-dev -y #安装dtk工具包
sudo apt install libdtkcore-bin libdtksettings-dev libdtksettingsview-dev -y
sudo apt install cmake -y #安装cmake
```
### 1.2.2 安装 CLion
官方源中的 CLion 还是 2017.2 版本的，已经比较旧了，官网目前最新的是 2018.2 版本
#### 方式一 使用 apt 自动安装 CLion
打开终端输入以下命令
````
sudo apt install clion -y #安装 CLion
````
#### 方式二 官网下载压缩包手动安装 CLion
1. 打开 [CLion官网](https://www.jetbrains.com/clion/)
2. 点击 **GET FREE 30 DAY TRIAL** 按钮，Chrome 会自动下载 CLion 的压缩包
3. 在文件夹中打开该文件，解压得到 **clion-2018.2.1** 文件夹
4. 执行 **clion-2018.2.1/bin** 目录下的 **clion.sh** 脚本，安装程序会自动启动
5. 此后跟着CLion安装引导程序的提示一路往下即可安装成功
6. （可选） CLion不支持多语言，但Github上有大牛维护的 CLion 汉化包，[戳这了解更多](https://github.com/pingfangx/TranslatorX)。
> 注意：CLion 为商业软件，提供 30 天试用，授权许可是 89 美元每年，以后逐年递减，**学生或开源项目认证通过后可免费使用**，详情请关注官网。<s>如果实在资金不允许，百度上也有对应的解决方案，这里不便叙述。</s>建议有条件的开发者能够购买正版。


## 1.3 配置CLion
CLion 是一款优秀的C/C++ IDE，很遗憾的是，它并不支持直接编辑 **.ui** 文件（Qt界面文件），这里我们需要添加 Qt Designer 作为 CLion 的 External Tools，以便于直接在 CLion 中直接调用 Qt Creator 来设计界面。

在CLion中，打开菜单 **File->Settings->Tools->External Tools** , 点击 **+** 新建工具，填入如下内容:
````bash
Name: Qt Designer
Tool settings:
     Program: /usr/bin/qtcreator
     Parameters: $FilePath$
     Working directory: $ProjectFileDir$ 
````
这里需要注意的是，由于每个人的 qtcreator 的路径不一定一样，终端输入 `which qtcreator` 回车查看 qtcreator 的路径，将其填入 Program 后面的文本框中。

<img src="https://images.lolimay.cn/18-8-17/41277023.jpg">

OK->Apply 保存后打开菜单，**File->Settings->Appearance & Behavior->Project View Popup Menu**，将 External Tools 拖到最上面（方便以后编辑 **.ui** 文件，如下图所示：

![](https://images.lolimay.cn/18-8-17/38622151.jpg)

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