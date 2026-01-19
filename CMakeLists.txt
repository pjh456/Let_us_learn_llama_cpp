cmake_minimum_required(VERSION 3.18)
project(let_us_learn_llama_cpp VERSION 0.1.0)

# 1. 设置 C++ 标准 (llama.cpp 要求至少 C++11，建议使用 17 或更高)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 2. 引入 llama.cpp 目录
add_subdirectory(llama.cpp)

# 3. 添加可执行程序
file(GLOB SRC_SUBDIRS
    RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
    src/*
)

function(add_llama_example TARGET SRC)
    add_executable(${TARGET} ${SRC})
    target_link_libraries(${TARGET} PRIVATE llama)
    target_include_directories(${TARGET} PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/llama.cpp/include
    )
endfunction()

foreach(dir ${SRC_SUBDIRS})
    # 只处理目录
    if(IS_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/${dir})
        # 只匹配纯数字目录名
        if(dir MATCHES "^src/[0-9]+$")
            # 提取数字 N
            string(REGEX REPLACE "^src/([0-9]+)$" "\\1" N ${dir})

            set(TARGET_NAME main${N})
            set(MAIN_SRC ${CMAKE_CURRENT_SOURCE_DIR}/${dir}/main.cpp)

            if(EXISTS ${MAIN_SRC})
                add_llama_example(${TARGET_NAME} ${MAIN_SRC})
            else()
                message(WARNING "Skip ${dir}: main.cpp not found")
            endif()
        endif()
    endif()
endforeach()
