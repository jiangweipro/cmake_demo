# 顶层cmake项目文件

# cmake 的最低版本要求
cmake_minimum_required (VERSION 3.8)

# 工程名
project ("project1")

# 添加版本号
set (project1_version_major 1)
set (project1_version_minor 0)


include_directories(.)

# 添加需要构建的子目录
add_subdirectory ("src")

if(1)

message("+++++++++++++++++++++++++++++++++++")
# 定义变量
set(var_name "var" "name")
# 打印 STATUS WARNING FATAL_ERROR(输出错误，会退出)
message(STATUS ${var_name})
# 判断变量是否存在
if(var_name)
    message(STATUS "after set check var_name")
endif()
# 删除变量
unset(var_name)
if(var_name)
    message(STATUS "after unset check var_name")
endif()

# 设置环境变量
set(ENV{PATH} $ENV{PATH}:/home/jiang)
message(STATUS "PATH: $ENV{PATH}")

# 判断环境变量
set(ENV{TEST_ENV} "HI")
if(NOT DEFINED ENV{TEST_ENV})
    message(STATUS "check not defined.")
endif() 
if(DEFINED ENV{TEST_ENV})
    message(STATUS "check defined.")
endif() 

# 判断文件是否存在
if(EXISTS test_exist.txt)
    message(STATUS "file test_exist.txt exist")
else()
    message(STATUS "file test_exist.txt not exist")
endif()

# 设置默认值
# 在命令行中没有 -D 定义变量时使用
# 命令行定义了，使用命令行的
option(flag "xxx" ON)

# 字符串比较
if("${flag}" STREQUAL "ON")
    message(STATUS "flag equal ON")
endif()

# 复制文件到其他地方并修改内容
#configure_file(
#    "${source_dir}/Config.h.in"
#    "${binary_dir}/Config.h"
#)

# file操作
# 创建文件并写入，如果文件存在就覆盖
file(WRITE tmp.txt "test file write.")
# 追加内容
file(APPEND tmp.txt "test file append.")
# 读取内容 读取长度1024 从offset 0开始 HEX指定十六进制 
file(READ tmp.txt file_content_string 1024 0 HEX)
message(STATUS ${file_content_string})  
# 创建目录，父目录不存在会创建
file(MAKE_DIRECTORY tmpdir)
# 重命名 mv
file(RENAME tmp.txt tmp1.txt)
# 删除 rm
file(REMOVE del.txt)
# 递归删除 rm -r 
file(REMOVE_RECURSE tmpdir)
# 路径转换 TO_CMAKE_PATH TO_NATIVE_PATH 

# 查找文件的完整路径 会在指定的和cmake path中找 可以使用NO_DEFAULT_PATH屏蔽
find_file(build_sh build.sh .)
message(STATUS "build.sh path: ${build_sh}")

# 查找库文件
find_library(pthread_so pthread /lib)
message(STATUS "pthread lib path: ${pthread_so}")

# 查找文件所在绝对路径
find_path(build_path build.sh .)
message(STATUS "build sh path: ${build_path}")

# 循环
foreach(i 1 2 3 4 5 6)
    message(${i})
endforeach()


# 判断 NOT AND OR
# TARGET名字是一个已存在的构建目标或导入目标
# EXISTS 是否存在
# IS_NEWER_THEN 文件更新，或者其中一个不存在
# IS_DIRECTORY 是否是一个路径（使用完整路径）
# IS_SYMLINK 是否是符号链接
# string MATCHES regex 匹配正则
# LESS GREATER EQUAL STRLESS(按字典序比较) VERSION_LESS(版本号比较)

# 包含 .h路径
include_directories(.)

# install指定安装是的路径 如果使用相对路径会加上 CMAKE_INSTALL_PREFIX
# install(FILE filename DESTINATION dir)  文件安装
# install(PROGRAMS file DESTINATION dir) 比FILE多OWNER_EXECUTE WORLD_EXECUTE
# install(DIRECTORY dir... DESTINATION dir) 目录安装


# 函数
function(my_print)
    message(STATUS "${ARGC} ${ARGV0} ${ARGV1}")
endfunction()
my_print("a" "b")

# 截取文件名部分 PATH(路径)  EXT(扩展名)  
# NAME_WE(去除扩展名) ABSOLUTE(完整路径) REALPATH(链接会解析为真实路劲)
get_filename_component(file_ext /home/ab.c.tar.gz EXT)
message(STATUS "Get file ex: ${file_ext}")


message(${CMAKE_INSTALL_PREFIX})

message("------------------------------------")
endif()


