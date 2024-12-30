# LLM-Inference 
Summary of theoretical knowledge on LLM Inference



本页主要大语言模型LLM推理优化相关知识



## 文档目录

### 1.LLM高效推理综述

- [A survey on efficient inference for large language models](https://arxiv.org/abs/2404.14294)  from arXiv

### 2.推理优化部分

|  序号 |   名称     | 简介    |地址|
|:---:|:----: |:---: |:---:|
| 1 | KV Cache|LLM推理基石，通过缓存加速decode过程|☁️Todo|
| 2 | GQA:Group-Query Attention|缓解KV Cache带来的内存IO开销的优化手段|[paper](https://arxiv.org/pdf/2305.13245)&[原理解释](https://mp.weixin.qq.com/s/_4OxoRLxhOcjGf0Q4Tvp2Q)|
| 3 | Flash Attention|通过GPU_IO aware优化内存IO开销实现的算子加速|[站外博客](https://readpaper.feishu.cn/docx/AC7JdtLrhoKpgxxSRM8cfUounsh)|
| 4 | Page Attention|以操作系统虚拟内存思想启发的KV cache内存管理优化|[站外博客](https://readpaper.feishu.cn/docx/EcZxdsf4uozCoixdU3NcW03snwV)|
| 5 | Offload|GPU+CPU混合计算内存卸载技术|☁️Todo|
| 6 | Quantization|LLM参数量化|[Link](./Quantize_Home.md)|
| 7 | sample TopK 采样|LLM参数量化|☁️Todo|
| ... | -     |-      | ... |





