# IOSTAT 磁盘、CPU采样工具

## How to start

1. Install

```bash
sudo apt update
sudo apt install sysstat
```

2. Quick start

```bash
iostat -d -x -k 1
```

- -d:显示磁盘使用情况
- -x:显示更详细的信息拓展
- -k:以KB为单位显示
- 1:表示每秒刷新一次

3. 基本参数表

| 选项        | 功能描述        |
|------------|---------------|
| `-c`       | 仅显示 CPU 统计信息 |
| `-d`       | 仅显示磁盘 I/O 统计信息|
| `-k`       | 以 KB 为单位显示 I/O 数据（默认是块）|
| `-m`       | 以 MB 为单位显示 I/O 数据|
| `-t`       | 在输出中添加时间戳|
| `-x`       | 显示详细的 I/O 统计信息（包括每秒读写请求数、平均队列长度等）|
| `-p <设备>` | 显示指定设备及其分区的统计信息（如 `-p sda` 显示 sda 及所有分区）|
