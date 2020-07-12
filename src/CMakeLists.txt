cmake_minimum_required(VERSION 3.17)

find_package(Python2 COMPONENTS Interpreter Development NumPy)
message("------------After Python2--------------")
add_library(Matplotlibcpp matplotlibcpp.h)
target_include_directories(Matplotlibcpp PRIVATE ${Python2_INCLUDE_DIRS})
target_link_libraries(Matplotlibcpp PUBLIC Python2::NumPy)
