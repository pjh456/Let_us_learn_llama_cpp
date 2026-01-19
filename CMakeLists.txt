cmake_minimum_required(VERSION 3.18)
project(let_us_learn_llama_cpp VERSION 0.1.0)

# 1. 设置 C++ 标准 (llama.cpp 要求至少 C++11，建议使用 17 或更高)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 2. 引入 llama.cpp 目录
add_subdirectory(llama.cpp)

# 3. 添加可执行程序
add_executable(my_app src/main.cpp)

# 4. 链接库
# llama: 核心库 (llama.h 对应的实现)
# common: 官方示例中常用的工具类 (包含采样、加载模型等辅助函数)
target_link_libraries(my_app PRIVATE llama common)

# 5. 如果需要包含 llama.cpp 内部的头文件路径
target_include_directories(my_app PRIVATE
    llama.cpp/include
    llama.cpp/common
)