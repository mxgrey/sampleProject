cmake_minimum_required(VERSION 2.8.3)
project(euclidean)

include_directories(${PROJECT_SOURCE_DIR})
include_directories(${CMAKE_BINARY_DIR})

add_definitions("-Wall -Wextra")

list(APPEND CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")

add_subdirectory(euclidean)

file(GLOB apps_source "apps/*.cpp")
LIST(SORT apps_source)

set(exec_dependencies euclidean)

message(STATUS "\n    Applications: ")
foreach(app_src_file ${apps_source})
    get_filename_component(app_base ${app_src_file} NAME_WE)
    message(STATUS "Adding application ${app_base}")
    add_executable(${app_base} ${app_src_file})
    target_link_libraries(${app_base} ${exec_dependencies})
endforeach(app_src_file)
