cmake_minimum_required(VERSION 2.8)
project(dhtest)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_VERBOSE_MAKEFILE ON)
endif()

set(GENERAL_WARNING_FLAGS           "-Wall -Wextra -pedantic -Wundef -Wshadow -Wno-cast-align -Wno-unused-parameter -Wno-unused-variable -Wcast-align -Wwrite-strings -Wswitch-default -Wswitch-enum -Wconversion -Wfloat-equal -Wno-aggregate-return")
set(GENERAL_DEBUG_FLAGS             "-ggdb -O0 -fno-omit-frame-pointer")
set(GENERAL_PROFILE_FLAGS           "-fprofile-arcs -ftest-coverage -fsanitize=address")
set(GENERAL_RELEASE_FLAGS           "-DNDEBUG -O3 -fomit-frame-pointer -funswitch-loops")
set(GENERAL_COMPILER_FLAGS          "-pipe")
set(STATIC_COMPILER_FLAGS           "-fPIC")

set(CMAKE_CXX_FLAGS_DEFAULT         "-std=c++14 -Weffc++ -Wctor-dtor-privacy -Wold-style-cast -Woverloaded-virtual -fnon-call-exceptions")
set(CMAKE_C_FLAGS_DEFAULT           "-std=c99 -D_POSIX_SOURCE")
set(CMAKE_EXE_LINKER_FLAGS_DEFAULT  "")
set(CMAKE_EXE_LINKER_FLAGS_DEBUG    "-rdynamic")
set(CMAKE_EXE_LINKER_FLAGS_PROFILE  "-fprofile-arcs -ftest-coverage -fsanitize=address")
set(CMAKE_EXE_LINKER_FLAGS_RELEASE  "-s")

set(CMAKE_CXX_FLAGS                 "${CMAKE_CXX_FLAGS_DEFAULT} ${GENERAL_COMPILER_FLAGS} ${GENERAL_WARNING_FLAGS}")
set(CMAKE_CXX_FLAGS_DEBUG           "${CMAKE_CXX_FLAGS_DEBUG_DEFAULT} ${GENERAL_DEBUG_FLAGS}")
set(CMAKE_CXX_FLAGS_RELEASE         "${CMAKE_CXX_FLAGS_RELEASE_DEFAULT} ${GENERAL_RELEASE_FLAGS}")
set(CMAKE_C_FLAGS                   "${CMAKE_C_FLAGS_DEFAULT} ${GENERAL_WARNING_FLAGS} ${GENERAL_COMPILER_FLAGS}")
set(CMAKE_C_FLAGS_DEBUG             "${CMAKE_C_FLAGS_DEBUG_DEFAULT} ${GENERAL_DEBUG_FLAGS}")
set(CMAKE_C_FLAGS_RELEASE           "${CMAKE_C_FLAGS_RELEASE_DEFAULT} ${GENERAL_RELEASE_FLAGS}")

set(DHTEST_SOURCE_DIR              "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(DHTEST_INCLUDE_DIR             "${CMAKE_CURRENT_SOURCE_DIR}/include")
include_directories(AFTER           "${DHTEST_INCLUDE_DIR}")

file(GLOB_RECURSE DHTEST_FILES_C "${DHTEST_SOURCE_DIR}/*.c")
file(GLOB_RECURSE DHTEST_FILES_H "${DHTEST_SOURCE_DIR}/*.h")

add_executable(dhtest ${DHTEST_FILES_C} ${DHTEST_FILES_H})
