cmake_minimum_required(VERSION 3.16)

project(finterp LANGUAGES Fortran)

file(GLOB SRC
  "${CMAKE_CURRENT_SOURCE_DIR}/src/*.F90"
)

add_library(finterp ${SRC})

set_target_properties(finterp PROPERTIES
  Fortran_MODULE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/mod"
)

target_include_directories(finterp PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/mod>
)

option(BUILD_TESTS "Build tests for finterp" ON)

if(PROJECT_IS_TOP_LEVEL AND BUILD_TESTS AND BUILD_TESTING)
  include(CTest)
  enable_testing()
  add_subdirectory(test)
endif()
