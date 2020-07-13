# Disable in-source builds to prevent source tree corruption.
if(" ${CMAKE_SOURCE_DIR}" STREQUAL " ${CMAKE_BINARY_DIR}")
  message(FATAL_ERROR "
   FATAL: In-source builds are not allowed.
          You should create a separate directory for build files.")
endif()

set(PROJECT_NAME "occupancy_grid_map")
set(TARGET_NAME "exe_occupancy_grid_map")
set(TEST_TARGET_NAME "occupancy_grid_map_tests")
set(DESCRIPTION "Occupancy Grid Map Algorithm aims to represent a map of the environment
                 as an evenly spaced field of binary random variables each representing
                 the presence of an obstacle at that location in the environment.")
set(AUTHOR "Luca Macchiusi <macchiusiluca@gmail.com>")
set(PROJECT_URL "https://github.com/LucaMac1/RoboND-OccupancyGridMappingAlgorithm")

cmake_minimum_required(VERSION 3.12...3.17)
project(${PROJECT_NAME} VERSION 1.0 LANGUAGES CXX)

if(MSVC)
  add_compile_options(/W3 /WX)
else()
  add_compile_options(-W -Wall -Werror)
endif()

set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES main.cpp)
set(HEADER_FILES)
add_subdirectory(${PROJECT_SOURCE_DIR}/include)
add_executable(${TARGET_NAME} ${SOURCE_FILES} ${HEADER_FILES})
target_link_libraries(${TARGET_NAME} Matplotlibcpp)
