cmake_minimum_required(VERSION 3.8)
project(MyProject)

# 查找 CUDA
find_package(CUDA REQUIRED)

# 添加你的 CUDA 源文件和 C++ 源文件
set(CUDA_SOURCE_FILES test_gpt2.cu train_gpt2.cu)
set(CPP_SOURCE_FILES test_gpt2.c train_gpt2.c)

# 设置 CUDA 源文件使用 NVCC 编译器
set_source_files_properties(${CUDA_SOURCE_FILES} PROPERTIES LANGUAGE CUDA)

# 设置 C++ 源文件使用 GCC 编译器
set_property(SOURCE ${CPP_SOURCE_FILES} PROPERTY LANGUAGE C)

add_executable(test_gpt2_c test_gpt2.c)
target_compile_options(test_gpt2_c -Ofast -Wno-unused-result -Wno-ignored-pragmas -Wno-unknown-attributes)
#add_executable(test_gpt2_cu test_gpt2.cu)
# 设置 NVCC 编译器选项
#target_compile_options(MyProject PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:-gencode arch=compute_50,code=sm_50>)