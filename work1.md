## GIL
GIL（全局解释器锁）是 Python 解释器（特别是 CPython 实现）中的一个机制，它确保在任意时刻只有一个线程可以执行 Python 字节码，即使在多线程环境下也是如此。
引用计数（Reference Counting）

## JIT
JIT 编译器会分析代码运行时的行为，识别频繁执行的代码块（热点代码）,将热点代码转换为机器码，以加速后续执行

## Motivation
For scientific computing tasks, this lack of concurrency is often a bigger issue than speed of executing Python code, since most of the processor cycles are spent in optimized CPU or GPU kernels.

There are existing ways to enable parallelism in CPython today, but those techniques come with significant limitations (see [Alternatives](https://peps.python.org/pep-0703/#alternatives)).

* Neural network-based AI models
* reinforcement learning
* DeepMind: translating large parts of our Python codebase into C++
* Dose-3D: “nogil” fork
* Cellprofiler

Library: 
However, library authors frequently care a great deal about performance and will design APIs that support working around the GIL. These workaround frequently lead to APIs that are more difficult to use.

leads to a more complex and confusing user experience:
GIL如何影响Numpy和Numeric Python库的用户体验

GPU: 
在深度学习和 GPU 密集型任务中，以下场景受 GIL 影响较大：

数据预处理与训练并行：

训练神经网络时，数据预处理（如图像增强、数据转换）通常需要 CPU 并行执行。
GIL 使得 Python 多线程无法真正并行，导致数据预处理成为瓶颈。
现有解决方案是使用 multiprocessing 进行数据加载，但这会增加额外的进程间通信开销。
多个 GPU 并行训练：

现代深度学习框架通常支持 多 GPU 训练（如 PyTorch 的 DataParallel）。
但由于 GIL 限制，Python 代码在 CPU 端的 多线程计算（如梯度聚合、数据传输）不能真正并行，降低了 GPU 利用率。


Python’s global interpreter lock makes it difficult to use modern multi-core CPUs efficiently for many scientific and numeric computing applications.

