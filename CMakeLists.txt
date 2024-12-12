cmake_minimum_required(VERSION 3.30)
get_filename_component(CURRENT_DIR_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)
message(STATUS "Current directory name: " ${CURRENT_DIR_NAME})
project(${CURRENT_DIR_NAME})

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_BINARY_DIR})
message("CMAKE_INSTALL_PREFIX = ${CMAKE_INSTALL_PREFIX}")

set(CMAKE_SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/src)

include_directories("${CMAKE_CURRENT_LIST_DIR}/src")
set(MAIN "${CMAKE_CURRENT_LIST_DIR}/src/main.cpp")
file(GLOB_RECURSE SOURCES "${CMAKE_CURRENT_LIST_DIR}/src/**.[ic]pp")
list(REMOVE_ITEM SOURCES ${MAIN})
message("SOURCE FILES = ${SOURCES}")
message("MAIN = ${MAIN}")

add_executable(${PROJECT_NAME} ${MAIN} ${SOURCES})

target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra)
# CREATE FORMAT COMMAND
file(GLOB_RECURSE SRC_FILES "src/**.[chi]pp" "tests/**.[chi]pp")
add_custom_target(format
	COMMAND clang-format -i ${SRC_FILES}
    WORKING_DIRECTORY 
    COMMENT "Formatting source and test files with clang-format"
)



