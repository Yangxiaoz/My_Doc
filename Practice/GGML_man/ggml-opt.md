# ggml-opt.cpp/h

此文件包含使用 GGML 训练模型的功能。与普通 GGML 相比，它不是严格需要的，但它为数据集等常见需求提供了更高级的接口。

## 1.ggml_opt_dataset

code：

```cpp
struct ggml_opt_dataset {
    struct ggml_context   * ctx    = nullptr;//外部变量，详情见下方表格连接
    ggml_backend_buffer_t   buf    = nullptr;
    struct ggml_tensor    * data   = nullptr;
    struct ggml_tensor    * labels = nullptr;
    //以图片检测举例
    int64_t ndata       = -1;// Number of data:训练/推理使用的数据批次的数量，例如一次读取1000张图片，ndata=1000
    int64_t ndata_shard = -1;//将ndata切片后的数量，例如将1000个批次照片切两份，那么ndata_shard = 500
    size_t  nbs_data    = -1;// Number byte of ndata_shard = ndata_shard * 一个图片大小 * 数据字节数量
    size_t  nbs_labels  = -1;// Number byte of labels_shard = ndata_shard * label数量 *  数据字节数量
    std::vector<int64_t> permutation; //排序，暂时未知作用
};
```

| 类型  | 名称    |  详解  | Link |
|:---:|:---:|:---:|:---:|
| struct ggml_context *| ctx|上下文管理结构体，负责管理tensor、buffer等数据| - |
| ggml_backend_buffer_t | buf | ggml管理内存分配和存储的核心结构体|...|
| struct ggml_tensor *| data | 训练/推理所需的数据的索引，处于ctx内部|...|
| struct ggml_tensor *| labels | 训练/推理所需的标签索引，处于ctx内部|-|
