# desktop文件入门

Desktop Entry 文件是 Linux 桌面系统中用于描述程序启动配置信息的文件，它以 `.desktop` 为后缀名，相当于 Windows 系统下的桌面快捷方式。通常一个二进制可执行程序是一个没有后缀没有图标的文件，不可以随意移动。如果没有 desktop 文件，用户每次都需要打开一层层文件夹最后找到这个可执行文件，然后启动应用。这样打开应用的方式没有问题，但特别繁琐，而且可执行文件分布散乱，不易于管理。
因此很多 Linux 发行版（包括 Deepin ) 都提供了启动器，便于集中管理应用程序。启动器本质是一个位于 `/usr/share/applications/` 路径下的目录。启动器目录中存放着很多 `.desktop` 文件，每个 `.desktop` 文件都是一个应用程序的入口，并且 `.desktop` 文件可以显示图标，对用户更加友好。

## desktop文件模板
一个 desktop 文件主要由两部分组成，头部 `[Desktop Entry]` 声明（用于指定这是一个desktop文件）和一系列的参数/值对组成。一个 desktop 文件至少要指定 3 个参数的值（Name、Type 和 Exec)
````desktop demo1.desktop
[Desktop Entry]
Name=<应用程序名>
Type=Application
Exec=<应用程序完整路径>
````
- Name: desktop 文件最终显示的名称（一定要注意和 desktop 文件名的区别）
- Type: 用于指定 desktop 文件的类型（包括 3 种类型：Application、Link、Directory)。我们这里主要讨论 Application（应用） 类型，若对其它两种类型的用法感兴趣请看[官方文档](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html)。
- Exec: 用于指定二进制可执行程序的完整路径

大多数情况下，我们还需要指定 Icon 的值（一个 desktop 文件没有图标那也太卑微了吧 :< ）
- Icon: 指定应用程序图标的完整路径(可以省略后缀名)
图标支持 `png` 格式、`svg` 格式等，图标的推荐尺寸为 `128x128`。

因此一个基本的 desktop 文件模板应该像下面这样：
````desktop demo2.desktop
[Desktop Entry]
Name=<应用程序名>
Type=Application
Exec=<应用程序完整路径>
Icon=<应用程序图标的完整路径>
````
## 应用示例
小明同学在 [CLion官网](https://www.jetbrains.com/clion/) 下载 CLion 解压后，把整个应用目录放置在 `~/Apps` 路径下（Apps 目录是他自己创建的），小明发现 CLion 的可执行文件和它的图标就在 `bin` 目录下：

![](https://images.lolimay.cn/18-9-9/95940192.jpg)

因此小明编写了在桌面新建了个 `clion.desktop` 文件，内容如下

````desktop clion.desktop
[Desktop Entry]
Name=CLion
Type=Application
Exec=/home/xiaoming/Apps/clion-2018.2.3/bin/clion.sh
Icon=/home/xiaoming/Apps/clion-2018.2.3/bin/clion
````
效果如下

![](https://images.lolimay.cn/18-9-9/31077250.jpg)

**这里要提个很多人可能会忽视的细节。小明创建的 clion.desktop 文件名是 clion，Name的值为 CLion，虽然图标最终显示的是 Clion，但是这个 desktop 的文件全名仍然是 clion.desktop 而不是 CLion.desktop。**

双击桌面的图标也可以正常启动 CLion，大功告成！

![](https://images.lolimay.cn/18-9-9/87550172.jpg)

## 添加到启动器

仅仅将 desktop 文件添加到桌面其实还不够，作为一名开发者我们要考虑最坏的情况（万一哪位用户一不小心就把桌面的 desktop 文件给删除了），因此把你的应用程序发送到启动器才是较为推荐的方法（用户可以自行把启动器中的应用发送到桌面）。
启动器本质是一个位于 `/usr/share/applications/` 路径下的目录，目录中存放着很多 `.desktop` 文件，我们只需将我们的应用图标复制一份到 `/usr/share/applications/`即可。

假设你的桌面有个 clion.desktop 文件
````bash
sudo cp ~/Desktop/clion.desktop /usr/share/applications # 把 clion.desktop 复制一份到启动器目录下
````
这时我们再打开启动器，会发现启动器中已经多了一个 CLion 的图标：

![](https://images.lolimay.cn/18-9-9/20506021.jpg)

## Categories 参数
desktop 支持的参数远远不止上诉4个，在 deepin 系统还有一个比较常用的参数就是 Categories。
- Categories: 用于指定应用的分类（如果缺省则分类到 `其他应用` ）

我们打开启动器并切换到分类视图，可以看到刚刚添加到 CLion 被分类到`其他应用`了，这显然不是我们想看到的。

![](https://images.lolimay.cn/18-9-9/40615066.jpg)

deepin 启动器将所有应用分为10类，分别是网络应用、社交沟通、音乐欣赏、视频播放、图形图像、办公学习、阅读翻译、编程开发、系统管理和其他应用。

![](https://images.lolimay.cn/18-9-9/73357158.jpg)

下面我们修改 `clion.desktop` 文件，使 deepin 启动器能够正确地将 CLion 分类为 `编程开发`。

````bash
sudo gedit /usr/share/applications/clion.desktop
````
在最后一行添加 `Categories=Development`并保存

![](https://images.lolimay.cn/18-9-9/97514158.jpg)

再打开启动器，可以发现 CLion 已经被正确地分类为`编程开发`分类下

![](https://images.lolimay.cn/18-9-9/4807365.jpg)

## 附表：Categories 对照表

| Categories | 分类 |
| - | - |
| network | 网络应用 |
| Chat | 社交沟通 |
| Audio | 音乐欣赏 |
| Video | 视频播放 |
| Graphics | 图形图像 |
| Office | 办公学习 |
| Translation | 阅读翻译 |
| Development | 编程开发 |
| Utility | 系统管理 |

## 参考链接
1. [Linux桌面快捷方式 Desktop Entry 详解](http://blog.chinaunix.net/uid-20332519-id-3015914.html)
2. [Desktop Entry Specification](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html)