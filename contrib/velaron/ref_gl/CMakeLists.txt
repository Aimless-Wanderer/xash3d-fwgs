cmake_minimum_required(VERSION 2.8.0)
project(ref_gl C)

set(XASH_REF_GL_SRC_DIR "${XASH_SRC_DIR}/ref_gl")
set(XASH_REF_GL ref_gl)
set(XASH_REF_GLES1 ref_gles1)
set(XASH_REF_GLES2 ref_gles2)

file(GLOB XASH_REF_GL_SRC "${XASH_REF_GL_SRC_DIR}/*.c")

add_definitions(-DREF_DLL)

include_directories(
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/engine"
	"${XASH_SRC_DIR}/engine/common"
	"${XASH_SRC_DIR}/engine/server"
	"${XASH_SRC_DIR}/engine/client"
	"${XASH_SRC_DIR}/pm_shared"
	"${XASH_SRC_DIR}/public"
	"${XASH_REF_GL_SRC_DIR}/"
)

if(ANDROID)
add_subdirectory(nanogl)
add_library(${XASH_REF_GLES1} MODULE ${XASH_REF_GL_SRC})
target_compile_definitions(${XASH_REF_GLES1} PRIVATE XASH_NANOGL)
target_link_libraries(${XASH_REF_GLES1} public nanogl log)

add_subdirectory(gl-wes-v2)
add_library(${XASH_REF_GLES2} MODULE ${XASH_REF_GL_SRC})
target_compile_definitions(${XASH_REF_GLES2} PRIVATE XASH_WES)
target_link_libraries(${XASH_REF_GLES2} public gl-wes-v2 log)
else()
add_library(${XASH_REF_GL} MODULE ${XASH_REF_GL_SRC})
target_link_libraries(${XASH_REF_GL} public)

install(
	TARGETS ${XASH_REF_GL}
	DESTINATION .
)
endif()

if(WIN32 AND MSVC)
	install(
		FILES $<TARGET_PDB_FILE:${XASH_REF_GL}>
		DESTINATION . OPTIONAL
	)
endif()
