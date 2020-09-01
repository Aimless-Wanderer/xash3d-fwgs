cmake_minimum_required(VERSION 2.8.0)
project(xash3d-fwgs)

include(CheckIncludeFile)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake/")
set(XASH_VERSION 0.20)
set(XASH_SRC_DIR "${CMAKE_CURRENT_LIST_DIR}/../.." CACHE INTERNAL "Xash3D sources directory.")

option(XASH_DEDICATED "Enable dedicated build. Servers must choose this." OFF)
set(SDL2_PATH "${XASH_SRC_DIR}/SDL2" CACHE PATH "Custom SDL2 library path.")

if(CMAKE_SIZEOF_VOID_P MATCHES "8")
	option(XASH_64BIT "Enable experimental 64-bit build. Note that you must also provide 64-bit game binaries." ON)
else()
	option(XASH_64BIT "Enable experimental 64-bit build. Note that you must also provide 64-bit game binaries." OFF)
endif()

if(XASH_DEDICATED) 
	option(XASH_SDL "Enable SDL." OFF)
	option(XASH_SINGLE_BINARY "Don't build game launcher and build engine as executable." ON)
else()
	option(XASH_SDL "Enable SDL." ON)
	option(XASH_SINGLE_BINARY "Don't build game launcher and build engine as executable." OFF)
endif()

check_include_file("stdint.h" STDINT_H_EXISTS)
if(STDINT_H_EXISTS)
    add_definitions(-DSTDINT_H="stdint.h")
else()
	add_definitions(-DSTDINT_H="pstdint.h")
endif()

if(NOT XASH_SINGLE_BINARY)
	add_subdirectory(game_launch)
endif()

if(NOT XASH_DEDICATED)
	add_subdirectory(mainui)
	add_subdirectory(ref_gl)
	add_subdirectory(ref_soft)
	if(NOT ANDROID)
		add_subdirectory(vgui_support)
	endif()
endif()

if(ANDROID)
	add_subdirectory(hlsdk-xash3d)
endif()

add_subdirectory(public)
add_subdirectory(engine)
