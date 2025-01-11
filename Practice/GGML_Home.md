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

## 二、 学习目录：

| 序号 | 内容    | 地址    |状态|
|:---:|:----: |:--- |:---:|
| 00 | 快速开始与学习方法介绍|[Link](./GGML_quickStart.md)|🔬Researching|
| 01 | GGML核心概念解析|[Link](./GGML_Guide.md)|🔬Researching|
| 02 | 源码注释目录  |[Link](./GGML_man/README.md)|🔬Updating|




