cmake_minimum_required(VERSION 3.21)
project(Crow)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_THREAD_LIBS_INIT "-lpthread")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
set(CMAKE_HAVE_THREADS_LIBRARY 1)
set(CMAKE_USE_WIN32_THREADS_INIT 0)
set(CMAKE_USE_PTHREADS_INIT 1)
set(THREADS_PREFER_PTHREAD_FLAG ON)

FIND_PACKAGE( Boost 1.70 COMPONENTS REQUIRED system)
INCLUDE_DIRECTORIES( ${Boost_INCLUDE_DIR} )

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



add_executable(crowHello main.cpp)
target_include_directories(crowHello PRIVATE ${Boost_INCLUDE_DIRS})
TARGET_LINK_LIBRARIES( crowHello LINK_PUBLIC ${Boost_LIBRARIES} )

install(TARGETS crowHello RUNTIME DESTINATION bin)
#[[
The check Performing Test CMAKE_HAVE_LIBC_PTHREAD
is about whether thread support functions are compiled into libc library directly,
or one need to link additional libraries (like -lpthread).

The check Looking for pthread_create in pthreads
tries to find pthreads library and function pthread_create in it.

The check Looking for pthread_create in pthread
tries to find pthread library and function pthread_create in it.

That particular output could be interpreted as:

    The platform supports threads by providing the header pthread.h and the library pthread.

This output is common for Unix-like systems.
Despite "Failed" and "not found" words, this is perfectly good output.
]]
