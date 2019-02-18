# CMake 实战
## 3.5 单个源文件
CMake 适用于比较大的项目，但如果连简单项目的 CMakeLists.txt 都不会写更何况比较大的项目。下面我们从最简单的情况入门，尝试构建单个源文件。建议自己亲自动手实践下面所有的案例，这样印象会更加深刻。VS Code 是一款优秀的跨平台代码编辑器，下面的练习推荐使用 [VS Code](https://code.visualstudio.com/) 进行实践。
1. 新建项目文件夹 demo1
2. 新建 demo1.cpp
````cpp demo1/demo1.cpp
#include <stdio.h>

int main(int argc, char const *argv[])
{
    printf("Hello, World");
    return 0;
}
````
3. 新建 CMakeLists.txt
````cpp demo1/CMakeLists.txt
cmake_minimum_required(VERSION 3.8) #要求CMake的最低版本为3.8,这行命令是可选的，我们可以不写这句话，但在有些情况下，如果CMakeLists.txt文件中使用了一些高版本Cmake特有的一些命令的时候，就需要加上这样一行，提醒用户升级到该版本之后再执行Cmake
project(demo1) #指定项目名称为demo1
add_executable(demo demo1.cpp) #指定生成的可执行文件名和所需源文件 格式: add_executable(生成的可执行文件名 源文件1 源文件2 ...)
````
整个项目内容如下

![](https://images.lolimay.cn/18-8-19/66993297.jpg)
4. 打开终端 `cd` 到项目根目录
````shell lolimay@lolimay-PC: example/cmake/demo1
mkdir build && cd build #单独创建一个 build 文件夹并 cd 进去
cmake .. #用 cmake 构建项目
make -j4 #开 4 个线程去编译项目
./demo #执行可执行文件
````

运行结果
![](https://images.lolimay.cn/18-8-19/39115902.jpg)

#### [点击查看本示例源码](https://github.com/loliMay/deepin-develop-guide/tree/master/example/cmake/demo1)

可能有人会有疑惑，为什么要单独创建一个 build 文件夹，直接就在项目文件夹下 `cmake . && make -j4` 不是更方便吗？是不是多次一举，让我们看看 build 文件夹下的内容

![](https://images.lolimay.cn/18-8-19/44200067.jpg)

### Out-Of Source 构建原则
将项目源文件与构建生成的目标文件同放在项目根目录下，会很容易产生混乱，十分不利于项目的管理。因此单独建立一个 build 文件夹专门放置构建生成的目标文件，能够防止项目的源文件被污染，以降低项目维护的成本，这体现了 CMake 的 Out-Of Source 构建原则。

## 3.6 同一目录多个源文件
接下来让我们尝试用 CMake 构建同一目录下含有多个源文件的项目。在这个示例中，我们把 [3.5](#3-5-%E5%8D%95%E4%B8%AA%E6%BA%90%E6%96%87%E4%BB%B6) 中的 `printf("Hello, World");` 封装成一个函数 `hello()` 并单独放置在 `hello.cpp` 源文件中，具体步骤如下：
1. 新建项目文件夹 demo2
2. 新建源文件 hello.cpp
````cpp demo2/hello.cpp
#include <stdio.h>

void hello() {
    printf("Hello, World");
}
````
3. 新建头文件 hello.h
````cpp demo2/hello.h
extern void hello();
````
4. 新建源文件 main.cpp
````cpp demo2/main.cpp #程序入口
#include "hello.h"

int main(int argc, char const *argv[])
{
    hello(); //调用hello函数
    return 0;
}
````
5. 新建 CMakeLists.txt
<figure class="highlight cmake"><figcaption><span>demo2/CMakeLists.txt</span></figcaption><table><tbody><tr><td class="gutter"><pre><span class="line">1</span><br><span class="line">2</span><br><span class="line">3</span><br></pre></td><td class="code"><s style="color:#9b9b9b;"><pre><span class="line"><span class="keyword">cmake_minimum_required</span>(VERSION <span class="number">3.8</span>) <span class="comment">#要求CMake的最低版本为3.8</span></span><br><span class="line"><span class="keyword">project</span>(demo2) <span class="comment">#指定项目名称为demo2</span></span><br><span class="line"><span class="keyword">add_executable</span>(demo main.cpp hello.cpp) <span class="comment">#指定生成的可执行文件名和所需源文件</span></span><br></pre></s></td></tr></tbody></table></figure>
    与 [3.5](#3-5-%E5%8D%95%E4%B8%AA%E6%BA%90%E6%96%87%E4%BB%B6) 中的 CMakeLists.txt 唯一不同的是在 `add_executable` 命令中增加了一个 hello.cpp 文件。这些写虽然没有什么问题，但如果源文件很多，把源文件的名字都添加进去将是一件烦人的工作。更省事的方法是使用 `aux_source_directory` 命令，该命令会查找指定目录下的所有源文件，然后将结果存入指定的变量名中。其语法如下：
    ````cmake
    aux_source_directory(<dir> <variable>)
    ````
    因此，可以修改 CMakeLists.txt 如下：
    ````cmake demo2/CMakeLists.txt
    cmake_minimum_required(VERSION 3.8)
    project(demo2)
    aux_source_directory(. DIR_SRCS) #将当前目录下所有源文件存至 DIR_SRCS 变量中
    add_executable(demo ${DIR_SRCS}) #引用 DIR_SRCS 变量的格式是 ${DIR_SRCS}
    ````

整个项目内容如下

![](https://images.lolimay.cn/18-8-20/6696068.jpg)

6. 打开终端 `cd` 到项目根目录
````shell lolimay@lolimay-PC: example/cmake/demo2
mkdir build && cd build #单独创建一个 build 文件夹并 cd 进去
cmake .. #用 cmake 构建项目
make -j4 #开 4 个线程去编译项目
./demo #执行可执行文件
````

运行结果
![](https://images.lolimay.cn/18-9-5/32502741.jpg)

#### [点击查看本示例源码](https://github.com/loliMay/deepin-develop-guide/tree/master/example/cmake/demo2)

## 参考链接
1. <a href="http://www.hahack.com/codes/cmake/">CMake入门实战 - HaHack</a>
