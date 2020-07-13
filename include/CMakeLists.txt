cmake_minimum_required(VERSION 3.17)

find_package(Python3 REQUIRED COMPONENTS Interpreter Development NumPy)

#add_library(Matplotlibcpp matplotlibcpp.h)
#target_include_directories(Matplotlibcpp PRIVATE ${Python3_INCLUDE_DIRS} ${Python3_NumPy_INCLUDE_DIRS})
#target_link_libraries(Matplotlibcpp Python2::Python)

add_library(Matplotlibcpp INTERFACE)
target_sources(Matplotlibcpp INTERFACE matplotlibcpp.h)
target_include_directories(Matplotlibcpp INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(Matplotlibcpp INTERFACE Python3::NumPy)
