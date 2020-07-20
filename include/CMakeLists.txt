cmake_minimum_required(VERSION 3.12...3.17)
project("matplotlibcpplib")


# add_library(${PROJECT_NAME} INTERFACE)

#target_include_directories(${PROJECT_NAME} INTERFACE
#                            $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
#                            $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
#                          )
#target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_11)
#target_link_libraries(${PROJECT_NAME} INTERFACE Python3::Python Python3::NumPy)


set(HEADER_FILES ${CMAKE_CURRENT_SOURCE_DIR}/matplotlibcpp.h)

add_library(${PROJECT_NAME} STATIC ${HEADER_FILES})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE CXX CXX_STANDARD 11 CXX_STANDARD_REQUIRED ON CXX_EXTENSIONS ON)

find_package(Python REQUIRED COMPONENTS Interpreter Development)
if (${Python_FOUND})
  target_include_directories(${PROJECT_NAME} PRIVATE ${Python_INCLUDE_DIRS})
  target_link_libraries(${PROJECT_NAME} PUBLIC Python::Python)
else()
  message(FATAL_ERROR "Python not found, please install it.")
endif()

find_package(Python REQUIRED COMPONENTS NumPy)
if (${Python_NumPy_FOUND})
  target_include_directories(${PROJECT_NAME} PRIVATE ${Python_NumPy_INCLUDE_DIRS})
  target_link_libraries(${PROJECT_NAME} PUBLIC Python::NumPy)
else()
  message(WARNING "Python NumPy not found, proceeding with -DWITHOUT_NUMPY."
  " Some functions might not work.")
  add_definitions(-DWITHOUT_NUMPY)
endif()
