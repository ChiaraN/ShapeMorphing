cmake_minimum_required(VERSION 2.8)
set(CMAKE_BUILD_TYPE  "Release")
set(CMAKE_CXX_FLAGS   "-w -g -O3")
set(CMAKE_MACOSX_RPATH 1)
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

project(libMorphing)	
file(                  GLOB_RECURSE sources src/*)
file(                  GLOB_RECURSE headers src/*.h)
add_library(           libMorphing SHARED ${sources})
#find_library(          Commons NAMES Commons HINTS "/usr/local/lib/iscd" required)
#find_library(          Elasticity NAMES Elasticity HINTS "/usr/local/lib/iscd" required)
include_directories(   "/usr/local/include/iscd")
#target_link_libraries( libMorphing Commons)

project(morphing)
file(                  GLOB_RECURSE sources src/${dirName}/*.c)
add_executable(        morphing src/main.c)
target_link_libraries( morphing libMorphing)

install(               TARGETS libMorphing LIBRARY DESTINATION "/usr/local/lib/")
install(               FILES   ${headers} DESTINATION "/usr/local/include/morphing/")
set_property(          TARGET  libMorphing PROPERTY INSTALL_RPATH_USE_LINK_PATH TRUE)
set_property(          TARGET  libMorphing PROPERTY OUTPUT_NAME Morphing)
install(               TARGETS morphing RUNTIME  DESTINATION "/usr/local/bin/")
set_property(          TARGET  morphing PROPERTY INSTALL_RPATH_USE_LINK_PATH TRUE)
