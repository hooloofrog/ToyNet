# ===== CMakeLists.txt (顶层) =====
cmake_minimum_required(VERSION 3.16)

project(linux_primer VERSION 0.1.0 LANGUAGES C)

# -----------------------------
# 强制 C11
# -----------------------------
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_VERBOSE_MAKEFILE ON)

# -----------------------------
# Debug/Release 编译选项
# -----------------------------
if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
    set(DEBUG_FLAGS "-O0 -Wall -fPIC -ggdb")
elseif (CMAKE_C_COMPILER_ID STREQUAL "Clang")
    set(DEBUG_FLAGS "-O0 -Wall -fPIC -g")
else()
    set(DEBUG_FLAGS "-O0 -Wall -fPIC -g")
endif()

set(RELEASE_FLAGS "-O2 -Wall -fPIC")

# -----------------------------
# INTERFACE target 管理编译选项
# -----------------------------
add_library(common_flags INTERFACE)
target_compile_options(common_flags INTERFACE
    $<$<CONFIG:Debug>:${DEBUG_FLAGS}>
    $<$<CONFIG:Release>:${RELEASE_FLAGS}>
)

# -----------------------------
# 全局默认输出目录
# -----------------------------
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)   # 可执行文件
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)   # 静态库
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)   # 动态库

# -----------------------------
# 添加子目录
# -----------------------------
add_subdirectory(demo)
#add_subdirectory(utils)
#add_subdirectory(other)
