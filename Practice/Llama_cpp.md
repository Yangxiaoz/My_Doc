# Llama.cpp 项目简介

项目github地址连接： [Link](https://github.com/ggerganov/llama.cpp/)

## 什么是llama.cpp?

llama.cpp是由Georgi Gerganov 个人创办的一个使用C++/C 进行llm推理的软件框架(同比类似vllm、TensorRL-LLM等)。但不要被其名字误导，该框架并不是只支持llama模型，其是一个支持多种llm模型，多种硬件后端的优秀框架。

## 为什么选择llama.cpp?

llama.cpp是一个专注于在边缘设备、个人PC上进行llm部署的推理框架。其相比于vllm等主流llm推理框架来说，有以下明显的优点：

- 纯 C++/C 实现，在windows、mac、linux等多种系统下编译都非常简单。
- 丰富的后端支持：支持x86、arm、Nidia_GPU、AMD_GPU、Vulkan甚至华为昇腾NPU_CANN
- 支持CPU AVX指令集进行矢量计算加速、CPU+GPU混合计算
- 支持低精度量化：1.5bit、2 bit、3 bit、4 bit、5 bit、6 bit和 8 bit整数量化，可加快推理速度并减少内存使用
- 在apple silicon苹果芯片上的优化是业内SOTA的

项目背景与核心思想： [Inference at the edge](https://github.com/ggerganov/llama.cpp/discussions/205)

## 相关术语解释

- GGML： ggml是一个类似于pytroch、tensorflow的，但使用C++/C 语言实现的机器学习tensor库。项目llama.cpp就是基于ggml进行开发的。
- GGUF： gguf是一种在ggml框架在推理/训练时使用权重的文件格式。同时其也是模型参数量化的一种格式。所以对于模型的4/8 bit等量化来说，gguf有其规定的量化方式。
- Backend： 后端，这里的后端指的是在推理时使用的硬件（如CPU、GPU、NPU），ggml框架通过设计统一的后端backend接口，使得可以让同一个模型同时运行在不同后端上

## How to Start

- 只想体验本地llm部署

首先，llama.cpp并不是一个面向消费者的成熟产品，尽管其因为任何依赖，编译简单。但对于c++语言不熟悉的同学来说，可能部署仍然有困难。这里推荐MIT团队的ollama开源项目：[Link](https://github.com/ollama/ollama)

ollama开源框架是一个使用llama.cpp作为底层进行封装的面向用户的项目，故其使用教程充分考虑到很多未接触c++、甚至不懂编成的用户。使得你可以使用仅仅几个步骤，利用docker完成llm的本地部署。

- 想要对llama.cpp底层原理一探究竟？

llama.cpp是一个非常好的ai高性能部署优化学习项目。在llama.cpp中你可以学习到关于各种ai算子的优化手段、cpu并行计算、CUDA算子加速、异构混合计算、ai模型量化、内存高效管理等等。

并且该项目使用C++/C，与其他大部分python/pytroch的项目相比，你可以直接看到很多方法技巧的底层实现。比如在学习那些以python等语言实现的项目时，可能你会发现阅读源码时非常轻松，看什么都能看的懂，但是一旦你想了解很多方法的底层细节时，你会发现其被各种规范层层封装，难以修改。总之，如果你对边缘AI高性能计算感兴趣，llama.cpp无疑是一个非常好的学习项目。

## 如何学习llama.cpp

对于很多人（包括我自己），可能对完整的llm推理流程不熟悉，甚至对于完整的AI网络推理过程（如tensor管理、网络的有向无环图遍历推理）没有太清晰的概念。这样就会使得一开始在阅读llama.cpp源码时无比痛苦，这也是C++这样相对低级语言的一个缺点：虽然你能直接看到很多方法的底层实现，但这也意味着很多代码相对比较晦涩、抽象。

那么，该如何进行llama.cpp的学习呢？

### 磨刀不误砍柴工：从GGML开始

ggml项目源码连接： [Link](https://github.com/ggerganov/ggml)

前面说到，ggml相当于c++版的pytroch。所以如果想要搞懂llama.cpp项目中的很多实现方法之前，你需要对ggml框架进行基础的一些概念学习。了解在这个框架里，tensor是如何保存、使用的？ggml_context又是什么东西？ggml框架如何管理多个异构的后端设备、内存的？等等。

当你从一些简单的例子开始，了解了一些ggml框架的基础概念、网络推理流程等后。再去阅读llama.cpp的源码就会轻松快速很多。

---

而本系列后续会记录如何学习ggml的过程、一些关键的概念与源码解析，最终到llama.cpp项目的完整源码学习与概念解读

> Next part: ggml框架学习：[LInk](./GGML_Home.md)