# GDB优雅调试技巧

> Written  In 2024_09.28 __by yxl   
> Last Edited In 2024_12.26__by yxl

本文记录关于GDB调试的一些基本指令使用与脚本自动化GDB调试技巧

*其中，一些关于GDB的基础命令，都可以通过直接询问大语言模型得到。但仅凭这些基础的命令，想要高效地调试一个程序（尤其是大型程序）几乎举步维艰。所以本文将在介绍一些基础指令的基础上，介绍一些特殊的GDB调试指令与技巧来提高开发效率。*

## 一、常用基本指令

- 断点设置

在调试一个程序时，往往需要首先进行断点的设置

```bash
break N   
```

其中字母 N 代表当前源代码文件中的行号或者函数名称。并且break可以简写为b

如在hello.c的源程序中的第25行以及该源程序的hello_init（）函数入口进行断点设置：

```bash
b 25
b hello_ini
```

- 跨文件断点设置

而如果hello.c文件中使用了其他源文件（假设为 test.c）中的函数时，需要指明文件名称，进行跨文件断点设置：

```bash
b test.c:79
b test.c:add_io
```

以上两句指令表示在test.c源文件中的第79行和add_io()函数入口进行断点设置。

- 查看当前已经设置的断点情况：

```bash
info breakpoint           或：     info b
```
输入后会显示断点序号已经断点所在文件、位置等信息。

- 删除断点

删除断点前通常需要使用info b指令来查看当前断点的断点序号，然后根据断点序号进行删除：

```bash
delete    Num               或：   d    Num
```

这里的Num指使用info b 查询到的对于断点序号。


- 禁用/使能断点


```bash
disable/enable b Num(opt)
```

可以通过disable指令或者enable指令来禁用/使能断点。

其中，如果不指定断点序号：Num 则会禁用/使能所有断点。

同样地，Num和断点的禁用/使能状态可以通过 info b 指令来进行查看。

---

在设置好断点之后，便可以开始运行调试程序了。接下来介绍关于程序运行相关指令：

### 运行程序

！！注意，如果想要在gdb上调试运行程序，需要在编译时加上-g或-ggdb参数，否则无法正常进行gdb调试

```bash
run file_exe -parameters
```

- file_exe 是所生成的可执行文件

- -parameters 是程序运行时所需要的入口参数

在程序遇到断点停止后，可以使用指令： continue 或者 c 来使得程序继续运行

### 单步运行

单步运行分为三种类型，分别是 : n (next) ； s (step) ； si (step instruct)

顾名思义，在命令行中键入：

n(或next)：会使得程序执行下一条语句，并且在执行函数语句时，不会进入函数内部，直接执行函数内部所有代码。

s： 同样会执行下一条语句，但在执行函数语句时，会跳转至函数内部执行指令

si ： 执行下一条汇编指令，通常在调试汇编级指令代码时才会用到

### 观察状态

在调试程序的过程中，需要一些指令来观察程序运行的状态。从而更好的调试程序：

- 观察源码

在进行调试时，我们首先需要知道运行处附近的代码是什么。

```bash
list    或   l
```

可以直接使用指令“l”查看当前运行处的代码，但这里不建议使用该指令(只会在极少数情况使用)

在实践中，我们更推荐使用**layout**视图直接显示源码：

```bash
layout src      #显示源代码 
layout asm      #显示汇编代码
layout regs     #显示寄存器
layout split    #分割当前视图    
```

该功能在大部分介绍GDB的文章中（包括直接询问大语言模型GBD的用法）都没有介绍该功能，但实际上layout功能在调试过程中十分好用。


使用layout显示代码视图后，调试终端会有一片区域进行相关的内容显示，但有时程序进行源文件间的跳转时，会使得视图刷新不正常而导致乱码，这是可以使用 **“ctrl + L”** 快捷键进行视图刷新，来获得正确视图

比较奇怪的是，不知为何**大多数大语言模型似乎并不能很好的理解如何关闭layout视图**，在询问过多个大模型后，都没有给出正确的答案 。事实上，想要退出layout视图界面需要先按下 **“ctrl + x”进入编辑模式，然后按下 “A”键**，便可以退出layout视图模式。

- 观察函数栈调用： 

```
bt
```

可以使用“ bt ”指令来打印当前运行所处的函数栈帧调用情况

- 观察变量

```
p   value_name      或     p/x  value_name
```

其中直接使用 指令 P 可以观察一个变量，或者一个地址所指向的内容

使用指令： p/x 可以使得内容以十六进制数显示。

- 监控变量(很重要)

```
watch value_name
```

watch指令是在调试程序时非常重要的一个指令，它可以添加一个变量（或地址所指向的区域）到监控列表，每当监控列表中的变量发生变化时，调试器会自动停止程序，并打印变量变化前后的数值。

- 修改变量

```
set  value_name = new_value
```
可以使用set命令对目标变量的大小进行修改，当然，修改时需要谨慎。

---

 以上便是一些GDB调试的常用指令，当然GDB还有很多其他功能指令，这里不做太详细的介绍。

但如果仅仅掌握这些指令来进行程序调试时，如果遇到一个比较复杂的程序，就会发现，每次退出GBD或者不小心关闭GBD后，一切的一切都需要重新开始了。。。你需要重新恢复上一次调试的context(上下文)：重新设置断点、设置监控变量、设置启动程序的入口参数等等。

那么有没有什么方法优化这个步骤呢？因为在我们大部分的IDE中，退出调试模式
并不会丢失断点等调试信息。当然有，那就是借助python脚本来实现自动化的GDB调试。

## 二、GDB的python自动化调试脚本

GDB原生就支持将一系列基础GDB指令写在一个以“.gdb”后缀命名的文件中，然后通过运行“gdb -x file_name.gdb”来运行一系列的自动化脚本进行调试。但由于gdb原生的脚本语法过于古老，很多导致很多操作受限，例如跨文件加载符号表、函数变量运算等。

为了解决这些问题，GDB提供了python的接口，我们可以通过 import gdb 来直接在python中编写自动化调试脚本。让我们先来看一段调试脚本例程。（读者可以对该例程进行裁剪得到自己的自动化调试脚本）脚本的逐行解释，在代码下方，可以将两者结合进行理解。

```python
import gdb
import os

# define the  hook
def on_quit(event):
    gdb.execute('kill')

def on_stop(event):
    frame = gdb.selected_frame()#fetch the stack frame
    flag_value = frame.read_var("verbose")#load the value  (verbose is a value_name)
    print(flag_value)
    gdb.execute('bt')#info the call Stack

def on_d_break(event):#info the current breakpoints
    gdb.execute('info b')

#Registering hook Functions
gdb.events.exited.connect(on_quit)
gdb.events.stop.connect(on_stop)
gdb.events.breakpoint_deleted.connect(on_d_break)


# Connect to the remote target
gdb.execute('target remote localhost:1234')

# 获取当前工作目录
current_directory = os.getcwd()
debug_file = 'mdriver'
path = os.path.join(current_directory, debug_file)

# Load the debug symbols
gdb.execute(f'file {path}')


# This is the 0x7c00
gdb.Breakpoint('main')
gdb.Breakpoint('mdriver.c:258')
gdb.Breakpoint('mm.c:115')

gdb.execute('watch free_listp')

gdb.execute('layout src')

gdb.execute('run -V -f short1-bal.rep')
```

编写一个GBD的自动化测试脚本可以分为以下几个步骤，但并不是所有步骤都必须实现。可以根据实际工程需要来进行删减或者添加。

### 1. define the hook ---定义挂钩函数

GDB中有很多触发事件，具体的事件可以通过在python中键入: " gdb.events. "来查看事件的子对象方法，或者询问大语言模型。在上述例程中，给出了三个事件和对应的挂钩函数（挂钩函数名称可以任意自取）：

- exited事件----on_quit（）

在GDB调试退出时，触发该事件信号，并调用对应挂钩函数，发出“kill”信号来终止调试对象的程序。

通常应用于需要远程端口连接的工程，如果没有远程连接，而是直接在本地调试的代码可以不进行注册

- stop事件----on_stop（）

在GDB调试程序时，因为断点、单步执行等因素而停止运行程序时，触发事件信号，从而调用对应挂钩函数。

通常可以在此函数中对想要观察的变量进行读取，读取至python后，你就可以对目标变量做任意想要的操作处理，python不会限制你的任何想象。

- breakpoint_deleted事件---on_d_break（）

在人为删除断点时，触发事件。在本例程中，使用该函数打印了当前断点信息，从而实现每次删除断点后，自动打印当前断点信息，以确认断点删除是否正确。

### 2. Registering hook Functions ---注册挂钩函

此步骤为将上述定义的挂钩函数与事件进行注册关联。具体操作过程详见代码

### 3. Connect to the remote target ---进行远程端口连接

在远程调试程序时进行的端口连接，一般用于虚拟机内核远程调试等，普通程序调试不需要该步骤，可以省略。

### 4. 获取当前工作目录（加载符号表）

将需要调试的可执行文件加载到GDB的符号表中

### 5.行断点、检测变量等基础设置

你可以在gdb.execute()函数的入口以形参的方式和来执行一切gdb脚本，包括断点设置、监控变量、运行程序等。

**最后**，运行gdb -x debug.py 命令（debug.py文件就是你所实现的自动化脚本文件名称）来启动我们的GDB 程序。你当然还可以将这句脚本写进你的makfile或者Cmake中，来实现最终的一键编译与调试运行

---

以上便是一切关于GDB的调试技巧，当然还有很多细节没有介绍到。但你通过本文可以大概清楚一个自动化的GDB调试流程是怎样的，然后结合大语言模型来填充一些细枝末节，你便可以高效的调试绝大部分工程。