set(PROJECT_NAME "occ_grid_map")
set(TARGET_NAME "exe_occ_grid_map")
set(TEST_TARGET_NAME "occ_grid_map_tests")

cmake_minimum_required(VERSION 3.12...3.17)
project(${PROJECT_NAME} VERSION 1.0 LANGUAGES CXX)

# set C++ standard to C++11
set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES solution.cpp)
set(HEADER_FILES)
  
set(MATPLOTLIBCPPLIB matplotlibcpplib)

# add the exectuable and link it to the matplotlibcpp lib
add_executable(${TARGET_NAME} ${SOURCE_FILES} ${HEADER_FILES})
target_link_libraries(${TARGET_NAME} PRIVATE ${MATPLOTLIBCPPLIB})

