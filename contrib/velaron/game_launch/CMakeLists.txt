cmake_minimum_required(VERSION 2.8.0)
project(game_launch C)

set(XASH_GAME_LAUNCH_SRC_DIR "${XASH_SRC_DIR}/game_launch")
set(XASH_GAME_LAUNCH xash3d)

include_directories(
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/public"
)

add_executable(${XASH_GAME_LAUNCH} WIN32 "${XASH_GAME_LAUNCH_SRC_DIR}/game.cpp" "${XASH_GAME_LAUNCH_SRC_DIR}/game.rc")

install(
	TARGETS ${XASH_GAME_LAUNCH}
	DESTINATION .
)

if(WIN32 AND MSVC)
	install(
		FILES $<TARGET_PDB_FILE:${XASH_GAME_LAUNCH}>
		DESTINATION . OPTIONAL
	)
endif()
