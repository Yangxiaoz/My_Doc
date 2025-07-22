# Flame Graphs 火焰图

1. 使用 perf record 记录数据

perf record 会对你的程序进行采样，记录下在 CPU 上执行的是哪个函数。

```bash
perf record -g --call-graph dwarf -F 99 -- ./my_io_demo
```

-g: 记录调用栈信息。

--call-graph dwarf: 使用 DWARF 调试信息来生成更精确的调用栈。需要你的程序用 -g 编译。

-F 99: 设置采样频率为每秒 99 次。这是一个常用的频率，可以避免与某些系统时钟产生共振。

-- ./my_io_demo: 运行你的程序。

这个命令会生成一个 perf.data 文件。

2. 安装和使用火焰图工具

火焰图的原始作者是 Brendan Gregg。你需要从他的 GitHub 仓库克隆工具集。

```bash
git clone https://github.com/brendangregg/FlameGraph.git
cd FlameGraph
```

3. 生成火焰图

现在，我们将 perf.data 转换成可视化的火焰图。

```bash
# 1. 将 perf.data 转换为可读格式
perf script > out.perf

# 2. 使用 FlameGraph 工具折叠调用栈
./stackcollapse-perf.pl ../out.perf > ../out.folded

# 3. 生成 SVG 格式的火焰图
./flamegraph.pl ../out.folded > ../io_uring_profile.svg
```

注意：上面的 ../ 假设你是在 FlameGraph 目录下执行这些命令，而 out.perf 和 out.folded 文件生成在了上一级目录。你可以根据自己的目录结构调整路径。