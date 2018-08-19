# CMake 入门教程
> CMake is great. Don't waste time on other C++ build tools, seriously.

[CMake](https://cmake.org/) 是一种高级构建工具，全称 cross-platform make，从字面意思上就可以看出，它的最大优势是跨平台。

当 Linux上著名的 [KDE](https://www.kde.org/) 项目从使用 Qt3 升级到使用 Qt4 时，整个项目将构建工具从 [Autotools](https://zh.wikipedia.org/wiki/GNU%E6%9E%84%E5%BB%BA%E7%B3%BB%E7%BB%9F) 转而使用 CMake，这使得 CMake 在 Qt 开发世界中在用户数、功能支持和质量上占有了特殊的位置。CLion 使用 cmake 作为构建工具，因此我们需要简单了解 CMake 并掌握它的一些基本用法。

<p class="button-outer"><a href="cmake-base.html"><span class="button">CMake入门 ➤</span></a></p>

<style>
    .button {
        margin-bottom: 550px;
    }
    /**
     * responsive support
     */
     @media (max-height: 800px) {
         .button {
             margin-bottom: 363px;
         }
     }
     @media (max-height: 700px) {
         .button {
             margin-bottom: 263px;
         }
     }
     @media (max-height: 600px) {
         .button {
             margin-bottom: 163px;
         }
     }
</style>