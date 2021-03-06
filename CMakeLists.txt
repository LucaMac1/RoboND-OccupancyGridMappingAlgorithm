# Disable in-source builds to prevent source tree corruption.
if(" ${CMAKE_SOURCE_DIR}" STREQUAL " ${CMAKE_BINARY_DIR}")
  message(FATAL_ERROR "
   FATAL: In-source builds are not allowed.
          You should create a separate directory for build files.")
endif()

set(PROJECT_NAME "occupancy_grid_map")
set(DESCRIPTION "Occupancy Grid Map Algorithm aims to represent a map of the environment
                 as an evenly spaced field of binary random variables each representing
                 the presence of an obstacle at that location in the environment.")
set(AUTHOR "Luca Macchiusi <macchiusiluca@gmail.com>")
set(PROJECT_URL "https://github.com/LucaMac1/RoboND-OccupancyGridMappingAlgorithm")

cmake_minimum_required(VERSION 3.12...3.17)
project(${PROJECT_NAME} VERSION 1.0 LANGUAGES CXX)

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

# Release by default
# Turn on Debug with "-DCMAKE_BUILD_TYPE=Debug"
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_STANDARD 11)

add_subdirectory(include)
add_subdirectory(src)