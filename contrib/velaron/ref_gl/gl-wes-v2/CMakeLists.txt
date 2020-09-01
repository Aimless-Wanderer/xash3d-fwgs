cmake_minimum_required(VERSION 2.8.0)
project(gl-wes-v2 C)

set(XASH_WES_SRC_DIR "${XASH_REF_GL_SRC_DIR}/gl-wes-v2")
set(XASH_WES gl-wes-v2)

file(GLOB XASH_WES_SRC "${XASH_WES_SRC_DIR}/src/*.c")

add_definitions(-DWES_MANGLE_PREPEND)

include_directories(
	"${XASH_WES_SRC_DIR}/src"
)

add_library(${XASH_WES} STATIC ${XASH_WES_SRC})
