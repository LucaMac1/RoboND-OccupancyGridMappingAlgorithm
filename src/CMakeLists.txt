cmake_minimum_required(VERSION 3.17)

find_package(Python2 2.7 REQUIRED EXACT COMPONENTS Interpreter Development)
# Since we've required 2.7, these should all be valid
set(PYTHON_LIBRARY ${Python2_LIBRARIES})
set(PYTHON_NUMPY_INCLUDE_DIR ${Python2_NumPy_INCLUDE_DIRS}
    CACHE PATH "Location of NumPy include files.")
        set(PYTHON_EXECUTABLE ${Python2_EXECUTABLE})
        find_package(NumPy 1.19 REQUIRED)
message("------------After Python2--------------")

add_library(Matplotlibcpp matplotlibcpp.h)
target_include_directories(Matplotlibcpp PUBLIC ${CMAKE_CURRENT_SOURCE_DIRECTORY} ${Python2_INCLUDE_DIRS})
target_link_libraries(Matplotlibcpp PUBLIC Python2::NumPy)
