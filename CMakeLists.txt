cmake_minimum_required(VERSION 2.8.12)
project(NS)

option(BUILD_CLIENT "Build client library" ON)
option(BUILD_SERVER "Build server library" OFF)

set(GAMEDIR "ns" CACHE STRING "Gamedir name")
set(SERVER_INSTALL_DIR "dlls" CACHE STRING "Server library target location")
set(CLIENT_INSTALL_DIR "cl_dlls" CACHE STRING "Client library target location")
set(SERVER_LIBRARY_NAME "ns" CACHE STRING "Library name for Linux/MacOS/Windows")

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
	message(STATUS "Building for 64 Bit")
else()
	message(STATUS "Building for 32 Bit")
endif()

if(NOT MSVC)
else()
	add_definitions(-D_CRT_SILENCE_NONCONFORMING_TGMATH_H -D_CRT_SECURE_NO_WARNINGS)
endif()

# dependencies
set(ZLIB_ROOT ${PROJECT_SOURCE_DIR}/3rdparty/zlib CACHE PATH "")
add_subdirectory(3rdparty/zlib)

add_subdirectory(3rdparty/libpng)

if(BUILD_CLIENT)
#	add_subdirectory(cl_dll)
endif()

if(BUILD_SERVER)
#	add_subdirectory(dlls)
endif()

if(NOT BUILD_SERVER AND NOT BUILD_CLIENT)
	error("Nothing to build")
endif()