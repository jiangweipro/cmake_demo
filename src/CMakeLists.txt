# 自动查找当前目录下所有源文件到变量
aux_source_directory (. DIR_SRCS) 

# 编译界面打印信息
message (STATUS "${DIR_SRCS}")

add_subdirectory("module1")
add_subdirectory("module2")

# 编译为可执行文件
add_executable (project1 ${DIR_SRCS})

# 链接库
target_link_libraries(project1 module1 module2)
