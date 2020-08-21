cmake_minimum_required(VERSION 2.8.0)
project(vgui_support CXX)

set(XASH_VGUI_SUPPORT_SRC_DIR "${XASH_SRC_DIR}/vgui_support")
set(XASH_VGUI_SUPPORT vgui_support)

file(GLOB XASH_VGUI_SUPPORT_SRC "${XASH_VGUI_SUPPORT_SRC_DIR}/*.cpp")

include_directories(
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/engine"
	"${XASH_SRC_DIR}/vgui-dev/include"
	"${XASH_VGUI_SUPPORT_SRC_DIR}/"
)

find_library(
	VGUI_LIBRARY vgui
	HINTS "${XASH_SRC_DIR}/vgui-dev"
	PATH_SUFFIXES lib lib/win32_vc6
)

add_library(${XASH_VGUI_SUPPORT} MODULE ${XASH_VGUI_SUPPORT_SRC})
target_link_libraries(${XASH_VGUI_SUPPORT} ${VGUI_LIBRARY})

install(
	TARGETS ${XASH_VGUI_SUPPORT}
	DESTINATION .
)

if(WIN32 AND MSVC)
	install(
		FILES $<TARGET_PDB_FILE:${XASH_VGUI_SUPPORT}>
		DESTINATION . OPTIONAL
	)
endif()
