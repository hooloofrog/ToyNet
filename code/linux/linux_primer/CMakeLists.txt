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
# Debug / Release 编译选项（现代风格）
# -----------------------------
# 直接设置 CMAKE_C_FLAGS_DEBUG / RELEASE，而不是自己造字符串
# 这最稳定，不会被引号坑，也不需要 INTERFACE target
set(CMAKE_C_FLAGS_DEBUG "-O0 -Wall -fPIC -ggdb")
set(CMAKE_C_FLAGS_RELEASE "-O3 -Wall -fPIC")

# 如果是 Clang 你想区分，可以这样加（可选）
if (CMAKE_C_COMPILER_ID STREQUAL "Clang")
    set(CMAKE_C_FLAGS_DEBUG "-O0 -Wall -fPIC -g")
endif()

# -----------------------------
# 全局默认输出目录
# -----------------------------
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

# -----------------------------
# 添加子目录
# -----------------------------
add_subdirectory(demo)
