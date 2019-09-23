aux_source_directory(. M1_DIR_SRCS)

# 编译为静态库
add_library(module1 ${M1_DIR_SRCS})

