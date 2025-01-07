# ggml-backend-impl.h

ggml多后端兼容框架实现


## 1. ggml_backend_buffer

```c
struct ggml_backend_buffer {
    struct ggml_backend_buffer_i  iface;//后端对buffer进行操作的接口
    ggml_backend_buffer_type_t    buft;//buffer所属后端类型
    void * context;//buffer实际存储数据区域地址
    size_t size;//buffer存储数据大小
    enum ggml_backend_buffer_usage usage;//buffer用途： any/weight/compute
    };
```