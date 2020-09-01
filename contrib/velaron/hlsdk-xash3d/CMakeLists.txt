cmake_minimum_required(VERSION 2.8.0)
project(hlsdk-xash3d)

set(XASH_SDK_DIR "${XASH_SRC_DIR}/contrib/velaron/android/hlsdk-xash3d")

add_subdirectory(cl_dll)
add_subdirectory(dlls)
