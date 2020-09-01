cmake_minimum_required(VERSION 2.8.0)
project(engine C)

set(XASH_ENGINE_SRC_DIR "${XASH_SRC_DIR}/engine")
set(XASH_ENGINE xash)

file(GLOB_RECURSE XASH_ENGINE_SRC "${XASH_ENGINE_SRC_DIR}/common/*.c" "${XASH_ENGINE_SRC_DIR}/server/*.c")
file(GLOB_RECURSE XASH_ANDROID_SRC
	"${XASH_ENGINE_SRC_DIR}/platform/posix/*.c"
	"${XASH_ENGINE_SRC_DIR}/platform/linux/*.c"
	"${XASH_ENGINE_SRC_DIR}/platform/android/*.c"
	"${XASH_ENGINE_SRC_DIR}/platform/android/*.cpp"
	)
file(GLOB_RECURSE XASH_WIN32_SRC "${XASH_ENGINE_SRC_DIR}/platform/win32/*.c")
file(GLOB_RECURSE XASH_SDL_SRC "${XASH_ENGINE_SRC_DIR}/platform/sdl/*.c")
file(GLOB_RECURSE XASH_CLIENT_SRC "${XASH_ENGINE_SRC_DIR}/client/*.c")

include_directories(
	"${XASH_SRC_DIR}/"
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/pm_shared"
	"${XASH_SRC_DIR}/public"
	"${XASH_ENGINE_SRC_DIR}/"
	"${XASH_ENGINE_SRC_DIR}/common"
	"${XASH_ENGINE_SRC_DIR}/common/imagelib"
	"${XASH_ENGINE_SRC_DIR}/common/soundlib"
	"${XASH_ENGINE_SRC_DIR}/client"
	"${XASH_ENGINE_SRC_DIR}/client/vgui"
	"${XASH_ENGINE_SRC_DIR}/server"
)

if(WIN32)
	list(APPEND XASH_ENGINE_SRC ${XASH_WIN32_SRC})
endif()

if(ANDROID)
	list(APPEND XASH_ENGINE_SRC ${XASH_ANDROID_SRC})
endif()

if(XASH_SDL AND NOT ANDROID)
	list(APPEND XASH_ENGINE_SRC ${XASH_SDL_SRC})
endif()

if(NOT XASH_DEDICATED)
	list(APPEND XASH_ENGINE_SRC ${XASH_CLIENT_SRC})
else()
	add_definitions(-DXASH_DEDICATED)
endif()

if(XASH_SINGLE_BINARY)
	add_definitions(-DSINGLE_BINARY)
	set(XASH_ENGINE xash3d)

	if(WIN32)
		add_executable(${XASH_ENGINE} WIN32 ${XASH_ENGINE_SRC})
	else()
		add_executable(${XASH_ENGINE} ${XASH_ENGINE_SRC})
	endif()
else()
	add_library(${XASH_ENGINE} MODULE ${XASH_ENGINE_SRC})
endif()

if(WIN32)
	add_definitions(-DDBGHELP -DPSAPI_VERSION=1)
	target_link_libraries(${XASH_ENGINE} dbghelp psapi ws2_32)
endif()

if(XASH_SDL AND NOT ANDROID)
	add_definitions(-DXASH_SDL=2)
	set(SDL2_BUILDING_LIBRARY ${XASH_SINGLE_BINARY})
	find_package(SDL2)
	include_directories(${SDL2_INCLUDE_DIR})
	target_link_libraries(${XASH_ENGINE} ${SDL2_LIBRARY})
endif()

if(ANDROID)
	target_link_libraries(${XASH_ENGINE} public log)
else()
	target_link_libraries(${XASH_ENGINE} public)

	install(
		TARGETS ${XASH_ENGINE}
		DESTINATION .
	)
endif()

if(WIN32 AND MSVC)
	install(
		FILES $<TARGET_PDB_FILE:${XASH_ENGINE}>
		DESTINATION . OPTIONAL
	)
endif()
