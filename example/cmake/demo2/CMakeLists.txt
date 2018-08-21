cmake_minimum_required(VERSION 3.8)
project(demo2)
aux_source_directory(. DIR_SRCS)
add_executable(demo ${DIR_SRCS}) #引用 DIR_SRCS 变量的格式是 ${DIR_SRCS}