cmake_minimum_required(VERSION 2.8.11)

if (NOT DEFINED CMAKE_BUILD_TYPE)
  set (CMAKE_BUILD_TYPE Release CACHE STRING "Build type")
endif ()

project (dlfcn-win32 C)

list(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake/modules")
include(Macros)

option(BUILD_SHARED_LIBS "shared/static libs" ON) 
option(BUILD_TESTS "tests?" OFF)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

if (MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall)
endif()

if(WIN32)
    add_subdirectory(src)
endif()

if (BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()
