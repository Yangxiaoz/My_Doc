# GGML Quick Start

## 一、编译工程

GGML是一个使用c、c++搭建的深度学习推理框架，该框架没有任何其他库（如opencv、math）的依赖。所以使得ggml的编译非常简单高效，无论是windows还是linux，在配置完成cmake与c++环境之后便可以一键编译。

整个项目使用了cmake编译工具进行了编译。cmake编译相关内容链接： [☁️Todo](.)


## 二、如何学习

由于该项目还在快速发展阶段，所以很多代码并没有完善的注释，加上C++、C这样低层次语言的抽象特性，导致该项目的初期学习阶段会相对较高。

所以在这种情况下最好的学习方法是寻找一个简单的demo，进行Debug逐行调试，来搞清楚整体的流程框架，要比生硬的看代码高效很多。

对于demo的选择，我们可以找到examples文件夹下的[mnist_net](https://github.com/ggerganov/ggml/tree/18703ad600cc68dbdb04d57434c876989a841d12/examples/mnist)手写数字识别项目，进行学习调试。

！注意，这里不推荐一开始学习exanple/simple的例子，因为该demo代码结构过于简单，只是为了展示一些框架的核心抽象概念，所以会导致看完后仍然无法搞清楚该框架是如何进行神经网络的训练和推理。



在开始mnist_net手写数字识别demo的学习之前，你应该阅读：[核心概念手册](GGML_Guide.md)来对ggml中的核心概念有大致的了解。

在代码阅读过程中，可以查阅：[源码注释手册](./GGML_man/README.md)

---
> Clink here to lear how the ggml works : [Next](./GGML_Guide.md) 