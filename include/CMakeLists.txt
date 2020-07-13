cmake_minimum_required(VERSION 3.17)

find_package(Python2 2.7 REQUIRED COMPONENTS Interpreter Development)

#add_library(Matplotlibcpp matplotlibcpp.h)
#target_include_directories(Matplotlibcpp PRIVATE ${Python2_INCLUDE_DIRS} ${Python2_NumPy_INCLUDE_DIRS})
#target_link_libraries(Matplotlibcpp Python2::Python Python2::NumPy)

add_library(Matplotlibcpp INTERFACE)
target_sources(Matplotlibcpp INTERFACE matplotlibcpp.h)
target_include_directories(Matplotlibcpp INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/Matplotlibcpp")
target_link_libraries(Matplotlibcpp INTERFACE Python2::NumPy)
