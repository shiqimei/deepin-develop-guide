# 起步

## 前言
《Deepin 开发指南》旨在帮助 Deppin 社区的开发者更快地投入进软件的开发过程中，按计划，该系列教程将会包括以下内容: 开发环境的搭建与配置、深度原生应用源码分析、Deepin Tool Kit API手册等。

## 部署开发环境
### 1. 安装 Qt、g++、dtk 工具集、cmake
打开终端输入以下命令
```sh
sudo apt update #更新软件源
sudo apt install qtcreator-dde g++ -y #安装Qt和g++
sudo apt install libdtkbase-dev libdtkwidget-dev libdframeworkdbus-dev -y #安装dtk工具集
sudo apt install libdtkcore-dev libdtksettings-dev libdtksettingsview-dev libdtkutil-dev libdtkwidget-dev libdtkwm-dev -y
sudo apt install cmake #安装cmake
```
### 2. 安装 CLion
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
> 注意：CLion 为商业软件，提供 30 天试用，授权许可是 89 美元每年，以后逐年递减，**学生或开源项目认证通过后可免费使用**，详情请关注官网。<s>如果实在资金不允许，百度上也有对应的解决方案，这里不便叙述。</s>建议有条件的开发者能够购买正版。