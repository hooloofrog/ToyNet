# demo 可执行文件，使用全局默认输出和编译选项
add_executable(demo demo.c)
target_link_libraries(demo PRIVATE common_flags)

# 如果需要特殊输出目录，可以覆盖
# set_target_properties(demo PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/special_bin)
