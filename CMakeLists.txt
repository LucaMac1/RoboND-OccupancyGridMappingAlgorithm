set(PROJECT_NAME "occupancy_grid_map")
set(TARGET_NAME "exe_occupancy_grid_map")
set(TEST_TARGET_NAME "occupancy_grid_map_tests")
set(DESCRIPTION "Occupancy Grid Map Algorithm aims to represent a map of the environment
                 as an evenly spaced field of binary random variables each representing
                 the presence of an obstacle at that location in the environment.")
set(AUTHOR "Luca Macchiusi <macchiusiluca@gmail.com>")
set(PROJECT_URL "https://github.com/LucaMac1/RoboND-OccupancyGridMappingAlgorithm")

cmake_minimum_required(VERSION 3.17)
project(${PROJECT_NAME} VERSION 1.0 LANGUAGES CXX)

if(MSVC)
  add_compile_options(/W3 /WX)
else()
  add_compile_options(-W -Wall -Werror)
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(HEADER_FILES src/matplotlibcpp.h)

#find_package(Python COMPONENTS Interpreter Development NumPy)
find_package(Python2 COMPONENTS NumPy)
add_executable(${TARGET_NAME} ${HEADER_FILES})
target_include_directories(${TARGET_NAME} PRIVATE ${Python2_INCLUDE_DIRS})
target_link_libraries(${TARGET_NAME} PUBLIC Python2::NumPy)
