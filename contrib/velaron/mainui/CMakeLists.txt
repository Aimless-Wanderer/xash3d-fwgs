cmake_minimum_required(VERSION 2.8.0)
project(mainui CXX)
set(CMAKE_CXX_STANDARD 11)

set(XASH_MAINUI_SRC_DIR "${XASH_SRC_DIR}/mainui")
set(XASH_MAINUI menu)

option(MAINUI_USE_CUSTOM_FONT_RENDER "Use custom font rendering." ON)
option(MAINUI_USE_STB "Use stb_truetype.h for rendering (*nix-only)." OFF)
option(MAINUI_RENDER_PICBUTTON_TEXT "Use custom font render to render picbuttons (experimental)." OFF)
option(MAINUI_FONT_SCALE "Scale fonts by height." OFF)

file(GLOB MAINUI_SRC "${XASH_MAINUI_SRC_DIR}/*.cpp" "${XASH_MAINUI_SRC_DIR}/miniutl/*.cpp")
file(GLOB MAINUI_CONTROLS_SRC "${XASH_MAINUI_SRC_DIR}/controls/*.cpp")
file(GLOB_RECURSE MAINUI_MENUS_SRC "${XASH_MAINUI_SRC_DIR}/menus/*.cpp")
file(GLOB MAINUI_FONT_SRC "${XASH_MAINUI_SRC_DIR}/font/*.cpp")

list(APPEND MAINUI_SRC ${MAINUI_CONTROLS_SRC})
list(APPEND MAINUI_SRC ${MAINUI_MENUS_SRC})
list(APPEND MAINUI_SRC ${MAINUI_FONT_SRC})

if(MAINUI_FONT_SCALE)
	add_definitions(-DMAINUI_FONT_SCALE)
endif()

if(MAINUI_USE_CUSTOM_FONT_RENDER)
	add_definitions(-DMAINUI_USE_CUSTOM_FONT_RENDER)
	if(MAINUI_RENDER_PICBUTTON_TEXT)
		add_definitions(-DMAINUI_RENDER_PICBUTTON_TEXT)
	endif()
endif()

include_directories(
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/engine"
	"${XASH_SRC_DIR}/pm_shared"
	"${XASH_MAINUI_SRC_DIR}/"
	"${XASH_MAINUI_SRC_DIR}/controls"
	"${XASH_MAINUI_SRC_DIR}/menus"
	"${XASH_MAINUI_SRC_DIR}/miniutl"
	"${XASH_MAINUI_SRC_DIR}/font"
	"${XASH_MAINUI_SRC_DIR}/model"
)

add_library(${XASH_MAINUI} MODULE ${MAINUI_SRC})

install(
	TARGETS ${XASH_MAINUI}
	DESTINATION .
)

if(WIN32 AND MSVC)
	install(
		FILES $<TARGET_PDB_FILE:${XASH_MAINUI}>
		DESTINATION . OPTIONAL
	)
endif()
