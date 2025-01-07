# Model Quantize 

### 1. Introduction to Weight Quantization

[参考文章1](https://towardsdatascience.com/introduction-to-weight-quantization-2494701b9c0c)、[参考文章2](https://python.plainenglish.io/quantization-demystified-gguf-gptq-awq-94796bd0ae27)



量化一共分两个大类：

- Post-Training Quantization (PTQ)   
一种简单的量化技术，其中已训练模型的权重被转换为较低的精度，而无需任何重新训练。虽然易于实现，但 PTQ 可能会导致性能下降。
- Quantization-Aware Training (QAT)   
在预训练或微调阶段加入权重转换过程，从而提高模型性能。然而，QAT 计算成本高昂，并且需要有代表性的训练数据。

### 具体量化方法

本节主要讨论Post-Training Quantization (PTQ)相关量化方法

| 方法名称  | 简介       | 原文（论文）地址  |  相关介绍  |
|:---:|:---:|:---:|:---:|
| llm.int8()量化 | 混合精度量化| [Link](https://arxiv.org/abs/2208.07339)|[Link](https://towardsdatascience.com/introduction-to-weight-quantization-2494701b9c0c)|
| GPTQ | 4bit量化技术| [Link](https://arxiv.org/abs/2210.17323)|[Link1](https://towardsdatascience.com/4-bit-quantization-with-gptq-36b0f4f02c34)&[Link2](https://huggingface.co/docs/transformers/quantization/gptq)|
| GGUF | Llama.cpp使用的量化结构，支持CPU、GPU混合运算| [Link](https://github.com/ggerganov/ggml/blob/master/docs/gguf.md)|[Link](https://towardsdatascience.com/quantize-llama-models-with-ggml-and-llama-cpp-3612dfbcc172)|
| ... | ... | ...|...|



### 其他参考：

1. Achieving FP32 Accuracy for INT8 Inference Using Quantization Aware Training with NVIDIA TensorRT:[Nvidia_Doc](https://developer.nvidia.com/blog/achieving-fp32-accuracy-for-int8-inference-using-quantization-aware-training-with-tensorrt/)





