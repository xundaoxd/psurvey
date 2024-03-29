cmake_minimum_required(VERSION 3.17)
project(ebpf-demo VERSION 0.0.1)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

set(CMAKE_CXX_STANDARD 17 CACHE STRING "C++ standard to conform to")
set(CMAKE_CXX_STANDARD_REQUIRED ON CACHE BOOL "Require the specified C++ standard for all targets")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pipe" CACHE STRING "Flags used by the compiler")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0 -rdynamic -fno-omit-frame-pointer -fno-optimize-sibling-calls -fno-inline" CACHE STRING "Flags used by the compiler during Debug builds")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3" CACHE STRING "Flags used by the compiler during Release builds")

find_package(bpf REQUIRED)

bpf_executable(example SRCS example.cc BPF_SRCS example.bpf.c)
bpf_executable(kprobe SRCS kprobe.cc BPF_SRCS kprobe.bpf.c)

bpf_objects(xdp_router_bpf_objs xdp_router.bpf.c)

