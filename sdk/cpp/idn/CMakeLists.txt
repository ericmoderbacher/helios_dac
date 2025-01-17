# Specify the minimum CMake version
cmake_minimum_required(VERSION 3.15)

# Set the project name
project(IDN_LIB VERSION 1.0 LANGUAGES CXX)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set_source_files_properties(
        ${CMAKE_CURRENT_SOURCE_DIR}/plt-posix.c
        PROPERTIES LANGUAGE CXX
)
add_library(plt STATIC
        ${CMAKE_CURRENT_SOURCE_DIR}/plt-posix.c
)
target_include_directories(
        plt
        PUBLIC ${PROJECT_SOURCE_DIR}/include
)

# Create a static library (change to SHARED if you prefer it to be shared)
add_library(idn STATIC
        ${PROJECT_SOURCE_DIR}/idn.cpp
        ${PROJECT_SOURCE_DIR}/idnServerList.cpp
        ${PROJECT_SOURCE_DIR}/plt-posix.c
)

# Add the include directory (headers)
include_directories(${PROJECT_SOURCE_DIR})

target_include_directories(
        idn
        PUBLIC ${PROJECT_SOURCE_DIR}/include
)

# Gather all source files in the 'src' directory
set(IDN_SOURCES
        ${PROJECT_SOURCE_DIR}/idn.cpp
        ${PROJECT_SOURCE_DIR}/idnServerList.cpp
        ${PROJECT_SOURCE_DIR}/plt-posix.c
)

target_link_libraries(idn PUBLIC plt)

message(STATUS "IDN Sources: ${IDN_SOURCES}")