cmake_minimum_required(VERSION 2.8.0)
project(public C)

set(XASH_PUBLIC_SRC_DIR "${XASH_SRC_DIR}/public")
set(XASH_PUBLIC public)

file(GLOB XASH_PUBLIC_SRC "${XASH_PUBLIC_SRC_DIR}/*.c")

include_directories(
	"${XASH_SRC_DIR}/common"
	"${XASH_SRC_DIR}/engine"
	"${XASH_PUBLIC_SRC_DIR}/"
)

add_library(${XASH_PUBLIC} STATIC ${XASH_PUBLIC_SRC})
