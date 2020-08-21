cmake_minimum_required(VERSION 2.8.0)
project(ref_soft C)

set(XASH_REF_SOFT_SRC_DIR "${XASH_SRC_DIR}/ref_soft")
set(XASH_REF_SOFT ref_soft)

file(GLOB XASH_REF_SOFT_SRC "${XASH_REF_SOFT_SRC_DIR}/*.c")

add_definitions(-DREF_DLL)

include_directories(
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/engine"
	"${XASH_SRC_DIR}/engine/common"
	"${XASH_SRC_DIR}/engine/server"
	"${XASH_SRC_DIR}/engine/client"
	"${XASH_SRC_DIR}/pm_shared"
	"${XASH_SRC_DIR}/public"
	"${XASH_REF_SOFT_SRC_DIR}/"
)

add_library(${XASH_REF_SOFT} MODULE ${XASH_REF_SOFT_SRC})
target_link_libraries(${XASH_REF_SOFT} public)

install(
	TARGETS ${XASH_REF_SOFT}
	DESTINATION .
)

if(WIN32 AND MSVC)
	install(
		FILES $<TARGET_PDB_FILE:${XASH_REF_SOFT}>
		DESTINATION . OPTIONAL
	)
endif()
