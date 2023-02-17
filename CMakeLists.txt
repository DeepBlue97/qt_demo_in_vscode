cmake_minimum_required(VERSION 3.5)
project(Demo1 LANGUAGE CXX)
set(CMAKE_INCLUDE_CURRENT_DIR ON) # cmake 包含当前目录
set(CMAKE_PREFIX_PATH "/home/peter/Qt") # Qt kit dir
set(CMAKE_AUTOUIC ON)  # 自动生成UI相关的东西
set(CMAKE_AUTOMOC ON)  # 自动生成信号槽的东西
set(CMAKE_AUTORCC ON)  # 自动生成资源文件的东西
set(CMAKE_CXX_STANDARD 11) # C++标准设置
set(CMAKE_CXX_STANDARD_REQUIRED ON)  # C++标准库
find_package(Qt5 COMPONENTS Widgets REQUIRED)  # Qt COMPONENTS 要加啥组件，加在这
aux_source_directory(./src srcs)

# Specify MSVC UTF-8 encoding  # 强制让MSVC用UTF-8来编译代码
add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

add_executable(${PROJECT_NAME}
    WIN32  # If you need a terminal for debug, please comment this statement (没有的话会附带一个黑框框)
    ${srcs}
)

# 链接库，差不多和 find_package 相呼应
target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Widgets)  # Qt5 Shared Library
