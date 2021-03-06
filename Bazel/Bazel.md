### 为什么使用Bazel？
- 减少构件时间：加速构建和测试，有着很好的本地和分布式缓存，优化的依赖分析和并发分析，可以快速的增量构建
- 一个工具构建多种语言：可以构建和测试Java、C++、Android、IOS、Go和其他各种语言，Bazel可以运行在Windows，macOS和Linux上
- 可伸缩：Bazel可以帮助扩大你的组织，代码库，和持续集成系统，它能处理任意大小的代码库，也可以处理多个库，或者巨大的包含许多不同项目的单一代码库
- 通用扩展满足需求：使用bazel的扩展语言能轻松的添加对新语言和平台的支持。

### Bazel概览
Bazel是一个构建工具，它可以协调构建各个模块，并且可以运行在单元测试。它的扩展语言使它可以构建任何类型的计算机语言，并且原生支持Java，C，C++和Python已经在各个平台上进行了充分的构建和测试。
> 用简单的声明性语言构建文件

Bazel的BUILD文件描述了怎样构建你的项目，它的语法类似Python的语法，编写BUILD文件的规则来构建你的系统，或者通过扩展Bazel的规则使它能够在任何构建平台上构建任何语言。

一个Hello World程序的BUILD构建文件，它使用两个规则:cc_library和cc_binary.
```
cc_library(
    name = "hello-time",
    srcs = ["hello-time.cc"],
    hdrs = ["hello-time.h"]
)

cc_binary(
    name = "hello-world",
    srcs = ["hello-world.cc"],
    deps = [
        ":hello-time",
        "//lib:hello-greet"
    ]
)
```
> 描述整个系统的依赖图

BUILD文件中声明了构建依赖的资源, Bazel可以通过它精确地画出所有源代码的依赖图. 只不过这张图由Bazel维护在内存中. 由于这张精确的依赖图存在, 它使得增量构建和平行执行成为了可能。

> 快速构建和测试，修改和复现

互不干扰的规则和沙箱环境让Bazel构建出正确的，可重复使用的构建和测试结果，缓存可以使构建出的构件和测试结果重复使用。
Baze的构建速度特别快，增量构建使得Bazel在进行重复构建时可以做最少的工作，Bazel的准确性和重复性使得Bazel可以重复使用未经修改且已缓存的构件，也就是说当你修改你的代码时，Bazel不会重新构建所有的源代码，而只是重新构建你修改的代码。
 你可以完全信任Bazel的构建结果的正确性，也就是说你不用运行bazel clean命令来清除bazel的构建结果，如果你需要运行bazel clean命令，那只能说明bazel存在bug。

 