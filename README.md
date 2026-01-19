# 深入浅出 Llama.cpp：从底层 API 到高性能推理后端

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![C++](https://img.shields.io/badge/Language-C++11/14/17-blue.svg)](https://en.wikipedia.org/wiki/C%2B%2B)
[![llama.cpp](https://img.shields.io/badge/Backend-llama.cpp-green.svg)](https://github.com/ggerganov/llama.cpp)

本仓库记录了我基于 `llama.cpp` 进行二次开发、将其作为推理后端集成到 C++ 项目中的完整过程。包含详细的 **博文系列**、**源码解析注释** 以及 **工程化封装示例**。

## 🚀 为什么发起这个项目？

`llama.cpp` 提供了极致的推理性能，但其核心接口采用的是 C 风格（`llama.h`），对习惯现代 C++ 开发的项目来说有一定的集成门槛。

本项目旨在：

1. **解构源码**：理清 `llama.cpp` 的推理生命周期。
2. **二次开发封装**：将原始 C API 包装成易用的现代 C++ 类。
3. **工程化实践**：探索 KV Cache 管理、多线程优化及流式接口实现。

---

## 📚 深度博文系列 (Blog)

我将学习过程总结为了一系列博客，存放在本仓库的 [`/docs`](./docs) 目录下：

- **[Part 1] 为什么选择 llama.cpp 及其源码导读**：介绍核心架构与学习路径。
- **[Part 2] 500 行代码跑通第一个推理示例**：拆解 `examples/simple` 的核心逻辑。
- **[Part 3] 封装你的第一个 C++ LlamaEngine**：利用 RAII 管理内存与生命周期。
- **[Part 4] 深入 KV Cache 管理**：如何实现多轮对话与并发推理优化。
- *(持续更新中...)*

---

## 📂 仓库结构

```text
Let_us_learn_llama_cpp
├── docs/               # 博文/文档目录
├── examples/           # 基于 llama.cpp 开发的各个阶段 Demo
│   ├── 01_simple/      # 最小推理示例
│   └── 02_wrapper/     # 初步封装的 C++ 类示例
├── src/                # 最终集成的推理后端核心代码
├── third_party/        # 第三方库（通过 Git Submodule 引入 llama.cpp）
└── CMakeLists.txt      # 统一的构建脚本
```

---

## 🛠️ 快速开始

### 1. 克隆仓库（包含子模块）

```bash
git clone --recursive https://github.com/pjh456/Let_us_learn_llama_cpp.git
cd Let_us_learn_llama_cpp
```

### 2. 编译项目

```bash
mkdir build
cd build
cmake ..
cmake --build . --config Release
```

### 3. 运行示例

你需要先准备一个 GGUF 格式的模型文件（如 `Qwen2-0.5B-Instruct-GGUF`）：

```bash
./bin/simple_inference -m ../models/your_model.gguf -p "Hello, how are you?"
```

---

## 🛠️ 开发环境

- **OS**: macOS / Linux / Windows (WSL2)
- **Compiler**: 支持 C++11 以上的编译器
- **Build System**: CMake 3.10+
- **Hardware Accelerator**: 支持 Metal (Apple Silicon) / CUDA (NVIDIA) / AVX2 (CPU)

---

## 🤝 贡献与交流

如果你在阅读源码或二次开发过程中有任何疑问，欢迎提交 **Issue** 或 **Pull Request**。

如果你觉得这些内容对你有帮助，欢迎点个 ⭐️ **Star**，这是对我最大的支持！

---

## 📜 鸣谢

感谢 [ggerganov/llama.cpp](https://github.com/ggerganov/llama.cpp) 项目及其贡献者，为开源社区提供了如此优秀的推理框架。