# ggml.cpp/h

ggml框架核心逻辑与实现

## 1. ggml_contex

```c
struct ggml_context {
    size_t mem_size;//context自身大小
    void * mem_buffer;//context内存储object容器表的buffer地址
    bool   mem_buffer_owned;//buffer是否为ctx拥有
    bool   no_alloc;//是否禁止分配（用于共享内存模式）

    int    n_objects;//ctx拥有的object容器数量

    struct ggml_object * objects_begin;//容器链表头
    struct ggml_object * objects_end;//容器链表尾
};
```



## 2. ggml_tensor

```c
struct ggml_tensor {
    enum ggml_type type;//tensor的数据类型，如GGML_TYPE_F32、GGML_TYPE_Q8_K...
    struct ggml_backend_buffer * buffer;//指向能够管理、操作Tensor对应的数据区域的buffer接口

    int64_t ne[GGML_MAX_DIMS]; // number of elements：tensor的维度（最大只支持4维）
    size_t  nb[GGML_MAX_DIMS]; // stride in bytes:索引tensor不同维度时的跨步步长，计算公式如下
                            // nb[0] = ggml_type_size(type)
                            // nb[1] = nb[0]   * (ne[0] / ggml_blck_size(type)) + padding
                            // nb[i] = nb[i-1] * ne[i-1]
            //举例：例如tensor=[784,1000,1,1]
            //那么：nb = [4,3136,3136000,3136000],
            //代表访问第一维数据时，每个数据地址间隔4byte。访问第二维度数据时，间隔3136个byte（4*784）。。。以此类推
    // compute data
    enum ggml_op op;//tensor在计算时，需要执行的操作算子

    // op params - allocated as int32_t for alignment
    int32_t op_params[GGML_MAX_OP_PARAMS / sizeof(int32_t)];//op操作所需要的参数

    int32_t flags;

    struct ggml_tensor * src[GGML_MAX_SRC];//计算时所需要的源数据tensor

    // source tensor and offset for views
    struct ggml_tensor * view_src;
    size_t               view_offs;

    void * data;//tensor对应实际数据的地址

    char name[GGML_MAX_NAME];//tensor的名字

    void * extra; // extra things e.g. for ggml-cuda.cu

    char padding[8];
};
```
