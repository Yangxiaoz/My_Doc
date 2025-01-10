# GGML深度学习框架


to read list:

[Hugging face 基础示例教程](https://huggingface.co/blog/zh/introduction-to-ggml)

[B站视频教程](https://www.bilibili.com/video/BV1GAC9YXE5Q/?spm_id_from=333.999.0.0&vd_source=ffd358de576192fb36c26e0aa712f76f)

## Introduction

[ggml](https://github.com/ggerganov/ggml) 是一个用 C 和 C++ 编写、专注于 Transformer 架构模型推理的机器学习库。该项目完全开源，处于活跃的开发阶段，开发社区也在不断壮大。ggml 和 PyTorch、TensorFlow 等机器学习库比较相似，但由于目前处于开发的早期阶段，一些底层设计仍在不断改进中。

相比于其它库，ggml 有以下优势:

- 最小化实现: 核心库独立，仅包含 5 个文件。如果你想加入 GPU 支持，你可以自行加入相关实现，这不是必选的。

- 编译简单: 你不需要花哨的编译工具，如果不需要 GPU，单纯 GGC 或 Clang 就可以完成编译。

- 轻量化: 编译好的二进制文件还不到 1MB，和 PyTorch (需要几百 MB) 对比实在是够小了。

- 兼容性好: 支持各类硬件，包括 x86_64、ARM、Apple Silicon、CUDA 等等。

- 支持张量的量化: 张量可以被量化，以此节省内存，有些时候甚至还提升了性能。
- 内存使用高效到了极致: 存储张量和执行计算的开销是最小化的。

## 框架学习指南：

1. [Link](GGML_Guide.md)