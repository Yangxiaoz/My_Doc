# GGML深度学习框架



## 一、 Introduction

[ggml](https://github.com/ggerganov/ggml) 是一个用 C 和 C++ 编写、专注于 Transformer 架构模型推理的机器学习库。该项目完全开源，处于活跃的开发阶段，开发社区也在不断壮大。ggml 和 PyTorch、TensorFlow 等机器学习库比较相似，但由于目前处于开发的早期阶段，一些底层设计仍在不断改进中。

相比于其它库，ggml 有以下优势:

- 最小化实现: 核心库独立，仅包含 5 个文件。如果你想加入 GPU 支持，你可以自行加入相关实现，这不是必选的。

- 编译简单: 你不需要花哨的编译工具，如果不需要 GPU，单纯 GGC 或 Clang 就可以完成编译。

- 轻量化: 编译好的二进制文件还不到 1MB，和 PyTorch (需要几百 MB) 对比实在是够小了。

- 兼容性好: 支持各类硬件，包括 x86_64、ARM、Apple Silicon、CUDA 等等。

- 支持张量的量化: 张量可以被量化，以此节省内存，有些时候甚至还提升了性能。
- 内存使用高效到了极致: 存储张量和执行计算的开销是最小化的。



## 二、How to start

由于该项目还在快速发展阶段，所以很多代码并没有完善的注释，加上C++、C这样低层次语言的抽象特性，导致该项目的初期学习阶段会相对较高。

所以在这种情况下最好的学习方法是寻找一个简单的demo，进行Debug逐行调试，来搞清楚整体的流程框架，要比生硬的看代码高效很多。

对于demo的选择，我们可以找到examples文件夹下的 [mnist_net](https://github.com/ggerganov/ggml/tree/master/examples/mnist) 手写数字识别项目，进行学习调试。

*！注意，这里不推荐一开始学习exanple/simple的例子，因为该demo代码结构过于简单，只是为了展示一些框架的核心抽象概念，所以会导致看完后仍然无法搞清楚该框架是如何进行神经网络的训练和推理。*

| 序号 | 内容    | 地址    |状态|
|:---:|:----: |:--- |:---:|
| 01 | GGML核心概念解析|[Link](./GGML_Guide.md)|🔬Researching|
| 02 | 源码注释目录  |[Link](./GGML_man/README.md)|🔬Updating|




