cmake_minimum_required(VERSION 3.16)
project(ScratchedHologramFrom3DWeb)

cmake_minimum_required(VERSION 3.15)

set(CMAKE_TOOLCHAIN_FILE ${EM_CMAKE_TOOLCHAIN})
add_definitions(-std=c++11 -O3)
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-s DISABLE_EXCEPTION_CATCHING=0 -s USE_PTHREADS=1 -s PTHREAD_POOL_SIZE=4 -s PROXY_TO_PTHREAD=1 -s WASM=1")

option(SCRATCH_STATIC_LIB_LINKING "Static linking enabled" ON)
option(DISABLE_TESTING "Tests compiling disabled" ON)
add_subdirectory(./ScratchedHologramFrom3D)

message(STATUS "Setting compilation target to WASM")
set(CMAKE_EXECUTABLE_SUFFIX ".js")
set_target_properties(ScratchedHologramFrom3DApp PROPERTIES LINK_FLAGS "-s EXPORTED_FUNCTIONS='[_main]'")
set_target_properties(ScratchedHologramFrom3DApp
        PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/public"
        )
