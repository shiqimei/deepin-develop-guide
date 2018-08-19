# CMake 实战
## 1.1 构建单个源文件
尽管上文说到 CMake 适用于比较大的项目，但如果连简单项目的 CMakeLists.txt 都不会写更何况比较大的项目。下面我们从最简单的情况入门，尝试构建单个源文件。建议自己亲自动手实践下面所有的案例，这样印象会更加深刻。VS Code 是一款优秀的跨平台代码编辑器，下面的练习推荐使用 [VS Code](https://code.visualstudio.com/) 进行实践。
1. 新建项目文件夹 demo1
2. 新建 hello.cpp
````cpp demo1/hello.cpp
#include <stdio.h>

int main(int argc, char const *argv[])
{
    printf("Hello, World");
    return 0;
}
````
3. 新建 CMakeList.txt
````cpp demo1/CMakeList.txt
cmake_minimum_required(VERSION 3.8) #要求CMake的最低版本为3.8
project(demo1) #指定项目名称为demo
add_executable(demo demo1.cpp) #指定生成的可执行文件名和所需源文件 格式: add_executable(生成的可执行文件名 源文件1 源文件2 ...)
````
整个项目内容如下

![](http://images.lolimay.cn/18-8-19/66993297.jpg)
4. 打开终端 `cd` 到项目根目录
````shell lolimay@deepin: example/cmake/demo1
mkdir build && cd build #单独创建一个 build 文件夹并 cd 进去
cmake .. #用 cmake 构建项目
make -j4 #开 4 个线程去编译项目
./demo #执行可执行文件
````
运行结果：
![](http://images.lolimay.cn/18-8-19/39115902.jpg)

有人可能会有疑问，为什么要单独创建一个 build 文件夹，直接就在项目文件夹下 `cmake . && make -j4` 不是就可以吗？是不是多次一举，看看 build 文件夹的内容便知。
![](http://images.lolimay.cn/18-8-19/44200067.jpg)

将项目源文件与生成的目标文件同放在项目根目录下，会很容易产生混乱，十分不利于项目的管理。因此需要单独建立一个 build 文件夹专门放置构建生成的目标文件，防止项目的源文件被污染，以降低项目维护的成本。

## 参考链接
1. <a href="https://www.zhihu.com/question/27455963">CMake入门实战 - HaHack</a>