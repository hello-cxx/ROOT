cmake_minimum_required(VERSION 3.1)

if (NOT HELLO_NAMESPACE)
get_filename_component(CURRENT_DIR ${CMAKE_CURRENT_LIST_DIR} NAME)
set(HELLO_NAMESPACE ${CURRENT_DIR} CACHE STRING
    "Top level namespace"
    FORCE)
endif()

project(${HELLO_NAMESPACE} VERSION 1.0.0)

add_compile_options(-DHELLO_NAMESPACE=${HELLO_NAMESPACE})

file(GLOB PROJECTS "${CMAKE_CURRENT_LIST_DIR}/" [a-zA-Z]*)
foreach(PROJECT ${PROJECTS})
    if(EXISTS "${PROJECT}/CMakeLists.txt")
        get_filename_component(PROJECT ${PROJECT} NAME)
        add_subdirectory(${PROJECT})
        message(STATUS "Add subproject: ${PROJECT}")
    endif()
endforeach()