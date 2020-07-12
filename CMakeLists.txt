set(PROJECT_NAME "occupancy_grid_map")
set(TEST_TARGET_NAME "occupancy_grid_map_tests")
set(DESCRIPTION "Occupancy Grid Map Algorithm aims to represent a map of the environment 
                 as an evenly spaced field of binary random variables each representing 
                 the presence of an obstacle at that location in the environment.")
set(AUTHOR "Luca Macchiusi <macchiusiluca@gmail.com>")
set(PROJECT_URL "https://github.com/LucaMac1/RoboND-OccupancyGridMappingAlgorithm")

cmake_minimum_required(VERSION 3.3...3.17)
project(${PROJECT_NAME} VERSION 1.0 LANGUAGES CXX)

if(MSVC)
  add_compile_options(/W3 /WX)
else()
  add_compile_options()-W -Wall -Werror)
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

# Configure built shared libraries in top-level lib directory
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../../lib)

find_package(Python2 COMPONENTS Interpreter NumPy)

# Build the shared libraries
add_library(frvt_11_null_001 SHARED nullimplfrvt11.cpp)
target_include_directories (frvt_11_null_001 PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/../include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../common/src/include
)
target_link_libraries(frvt_11_null_001 PUBLIC Python2::NumPy)
