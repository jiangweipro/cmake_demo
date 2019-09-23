aux_source_directory(. M2_DIR_SRCS)

# 编译为动态库
add_library(module2 SHARED ${M2_DIR_SRCS})

