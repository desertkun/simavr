
cmake_minimum_required(VERSION 3.7)
project(simavr)

file(GLOB_RECURSE SRCS "simavr/sim/*.c" "simavr/cores/*.c" "simavr/sim/*.h" "simavr/cores/*.h")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake/Modules/")

find_package(LibElf REQUIRED)

include_directories(simavr/cores
					simavr/sim
					simavr
					${LIBELF_INCLUDE_DIRS})

if (UNIX)
	include_directories(/usr/local/include)
endif()

add_library(simavr ${SRCS})

target_link_libraries(simavr ${LIBELF_LIBRARIES})