# 顶层cmake项目文件

# cmake 的最低版本要求
cmake_minimum_required (VERSION 3.8)

# 工程名
project ("project1")

# 添加版本号
set (project1_version_major 1)
set (project1_version_minor 0)


include_directories(.)

# 子目录
add_subdirectory ("src")


