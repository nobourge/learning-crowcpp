cmake_minimum_required(VERSION 3.21)
project(Crow)

set(CMAKE_CXX_STANDARD 20)

find_package(Threads)
find_package(ZLIB)
find_package(OpenSSL)

if(OPENSSL_FOUND)
    include_directories(${OPENSSL_INCLUDE_DIR})
endif()

if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Release")
    set(CMAKE_BUILD_TYPE "Release")
endif()

include_directories(${Boost_INCLUDE_DIR})

add_executable(crow main.cpp)
