# Practice

本页为一些开源项目的集中收录与实践工程问题记录总结



## 一、项目收录

1. 面向商用化的LLM推理框架

| 名称  | 简介       | 地址    |后端|
|:---:|:----: |:--- |:---:|
| vllm | 快速且易于使用的 LLM 推理和服务库。|[Link](https://docs.vllm.ai/en/stable/)|pytorch|
| LMDeploy | LMDeploy 由 MMDeploy 和 MMRazor 团队联合开发，是涵盖了 LLM 任务的全套轻量化、部署和服务解决方案|[Link](https://github.com/InternLM/lmdeploy)|pytorch or [TurboMind](https://github.com/InternLM/lmdeploy/blob/main/docs/zh_cn/inference/turbomind.md)|
| LMDeploy-Jetson| 将LMDeploy移植到NVIDIA Jetson系列边缘计算卡的部署教程仓库|[Link](https://github.com/BestAnHongjun/LMDeploy-Jetson?tab=readme-ov-file)|同上|
| LightLLM | 纯python开发的大语言模型推理和服务框架，具有轻量级设计、易扩展以及高性能等特点 |[Link](https://github.com/ModelTC/lightllm)|python|
| TensorRT-LLM |Nvidia 官方llm推理框架 |[Link](https://github.com/NVIDIA/TensorRT-LLM)   |TensorRT |
| SGLang |针对大型语言模型和视觉语言模型的快速服务框架 |[Link](https://github.com/sgl-project/sglang)   |pytroch |


2. 面向边缘部署的LLM项目


| 名称  | 简介       | 地址    |后端|
|:---:|:----: |:--- |:---:|
| llama.cpp | Inference of Meta's LLaMA model (and others) in pure C/C++|[Link](https://github.com/ggerganov/llama.cpp)|ggml (C++)|
| llama2.c | Inference Llama 2 in one file of pure C |[Link](https://github.com/karpathy/llama2.c)| C|
| calm | CUDA/Metal accelerated language model inference |[Link](https://github.com/zeux/calm)| C|
| yalm |  LLM inference in C++/CUDA, no libraries except for I/O(专注于原理、代码可读性的科研实验项目) |[Link](https://github.com/andrewkchan/yalm)| C++|


## 二、项目部署记录

### 1. llama.cpp

| 序号 | 内容    | 地址    |状态|
|:---:|:----: |:--- |:---:|
| 00 | Build and Run|-|☁️Todo|
| 01 |Understanding how LLM inference works with llama.cpp  |[Link](https://www.omrimallis.com/posts/understanding-how-llm-inference-works-with-llama-cpp/)|Web Link|




### 2. vllm
