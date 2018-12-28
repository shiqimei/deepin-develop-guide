# 创建Deepin示例应用

## 2.1 创建一个空项目
打开 CLion，新建一个项目

![](https://images.lolimay.cn/18-8-18/65089447.jpg)

修改项目名为 Demo，修改 C++ 标准为 C++17，点击 Create

![](https://images.lolimay.cn/18-8-18/89538457.jpg)

双击项目文件夹，此时项目的目录结构应该如下所示

![](https://images.lolimay.cn/18-8-18/32475353.jpg)

CLion 会自动在每个项目的根目录下创建 **cmake-build-debug** 文件夹，这个文件夹的内容是自动生成的，我们无需关心。

## 2.2 对原有项目进行改造
下面我们按照 <a href="start.html#1-4-%E7%94%A8-CMake-%E6%9E%84%E5%BB%BA-Qt-%E9%A1%B9%E7%9B%AE" target="_blank">起步 - 1.4 用 CMake 构建 Qt</a> 中提供的项目模板对原来的项目进行改造，改造后的结果如下

![](https://images.lolimay.cn/18-8-18/90831166.jpg)

## 2.3 重载并运行项目
现在我们右击项目，点击 **Reload CMake Project** 重载项目

![](https://images.lolimay.cn/18-8-21/25274282.jpg)

若 CLion 的 Debug输出如下显示，则说明项目配置没有问题

![](https://images.lolimay.cn/18-8-18/2004859.jpg)

最后，我们点击屏幕右上角的 <img src="https://images.lolimay.cn/18-8-18/7636848.jpg" /> 绿色三角形按钮（红框标注），运行此示例项目

![](https://images.lolimay.cn/18-8-18/6100766.jpg)

运行结果如上图所示，恭喜你已跨入 Deepin 应用开发的大门！

#### [点击查看本示例源码](https://github.com/loliMay/deepin-develop-guide/tree/master/example/Demo)

## 2.4 其它意外情况
1. 重载项目时 CLion 的 Debug 输出报错

![](https://images.lolimay.cn/18-8-18/34186974.jpg)

**原因**： 缺少 DTK 组件 (点击这里[了解 DTK](/intro/dtk.html))，应该是在 <a href="start.html#1-2-%E9%83%A8%E7%BD%B2%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83" target="_blank">起步 - 步骤 1.2.1</a> 中没有正确地安装完整的 dtk 工具包
**解决方法**： 打开终端，输入以下命令
````bash lolimay@lolimay-PC:
sudo apt install libdtkbase-dev libdtkwidget-dev libdframeworkdbus-dev -y #安装dtk工具包
sudo apt install libdtkcore-dev libdtksettings-dev libdtksettingsview-dev libdtkutil-dev libdtkwidget-dev libdtkwm-dev -y
````

<p class="button-outer"><a href="cmake/cmake.html"><span class="button">CMake入门教程 ➤</span></a></p>