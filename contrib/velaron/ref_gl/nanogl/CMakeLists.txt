cmake_minimum_required(VERSION 2.8.0)
project(nanogl CXX)

set(XASH_NANOGL_SRC_DIR "${XASH_REF_GL_SRC_DIR}/nanogl")
set(XASH_NANOGL nanogl)

file(GLOB XASH_NANOGL_SRC "${XASH_NANOGL_SRC_DIR}/*.cpp")

add_definitions(-D__MULTITEXTURE_SUPPORT__ -DNANOGL_MANGLE_PREPEND)

include_directories(
	"${XASH_NANOGL_SRC_DIR}/"
	"${XASH_NANOGL_SRC_DIR}/GL"
)

add_library(${XASH_NANOGL} STATIC ${XASH_NANOGL_SRC})
