cmake_minimum_required(VERSION 3.17)
project("Matplotlibcpp")

find_package(Python3 REQUIRED COMPONENTS Interpreter Development NumPy)

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(${PROJECT_NAME} INTERFACE
                            $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
                            $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
                          )
target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_11)
target_link_libraries(${PROJECT_NAME} INTERFACE Python3::Python Python3::NumPy)
