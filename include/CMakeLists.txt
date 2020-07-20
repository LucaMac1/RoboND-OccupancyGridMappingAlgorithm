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

# Set compiler specific settings (FixMe: Should not cmake do this for us automatically?)
IF("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
   SET(CMAKE_CXX_FLAGS_DEBUG  "-O0 -g")
   SET(CMAKE_CXX_FLAGS_RELEASE "-O3")
   #SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -Wextra  -Wno-deprecated-register -Qunused-arguments -fcolor-diagnostics")
ELSEIF("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
   SET(CMAKE_CXX_FLAGS_DEBUG  "-O0 -g")
   SET(CMAKE_CXX_FLAGS_RELEASE "-O3")
   SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -Wextra -std=c++11 -Wno-deprecated-declarations -ftemplate-backtrace-limit=0")
   SET(CMAKE_CXX_FLAGS_COVERAGE "${CMAKE_CXX_FLAGS_DEBUG} --coverage -fno-inline -fno-inline-small-functions -fno-default-inline")
   SET(CMAKE_EXE_LINKER_FLAGS_COVERAGE "${CMAKE_EXE_LINKER_FLAGS_DEBUG} --coverage")
   SET(CMAKE_SHARED_LINKER_FLAGS_COVERAGE "${CMAKE_SHARED_LINKER_FLAGS_DEBUG} --coverage")
ELSEIF(CMAKE_CXX_COMPILER_ID MATCHES "^MSVC$")
   ADD_DEFINITIONS("-D _USE_MATH_DEFINES /bigobj /wd4305 /wd4244 /MP")
ENDIF()

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
  option(WITHOUT_NUMPY "WITHOUT_NUMPY switches to ON if NumPy is not found." OFF)
  add_definitions(-DWITHOUT_NUMPY)
else()
  message(WARNING "Python NumPy not found, proceeding with -DWITHOUT_NUMPY."
  " Some functions might not work.")
  add_definitions(-DWITHOUT_NUMPY)
endif()
