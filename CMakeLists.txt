cmake_minimum_required(VERSION 3.20)
project(ImGUI CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -g")
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(PROJECT_SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR})
set(PROJECT_INCLUDE_DIR ${CMAKE_CURRENT_LIST_DIR})
set(CMAKE_BINARY_DIR ${CMAKE_CURRENT_LIST_DIR}/../build)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

set(SOURCE_FILES
  ${PROJECT_SOURCE_DIR}/imgui.cpp
  ${PROJECT_SOURCE_DIR}/imgui_draw.cpp
  ${PROJECT_SOURCE_DIR}/imgui_tables.cpp
  ${PROJECT_SOURCE_DIR}/imgui_widgets.cpp
  ${PROJECT_SOURCE_DIR}/imgui_demo.cpp
)
set(HEADER_FILES
  ${PROJECT_INCLUDE_DIR}/imgui.h
  ${PROJECT_INCLUDE_DIR}/imgui_internal.h
  ${PROJECT_INCLUDE_DIR}/imstb_rectpack.h
  ${PROJECT_INCLUDE_DIR}/imstb_textedit.h
  ${PROJECT_INCLUDE_DIR}/imstb_truetype.h 
 )

set(MISC_HEADERS
  ${PROJECT_INCLUDE_DIR}/misc/cpp/imgui_stdlib.h
  ${PROJECT_INCLUDE_DIR}/misc/single_file/imgui_single_file.h
  )

set(MISC_SOURCE
  ${PROJECT_INCLUDE_DIR}/misc/cpp/imgui_stdlib.cpp
)

set(BACKEND_SOURCE_GLFW
  ${PROJECT_INCLUDE_DIR}/backends/imgui_impl_glfw.cpp
  ${PROJECT_INCLUDE_DIR}/backends/imgui_impl_opengl3.cpp
  )

set(BACKEND_HEADERS_GLFW
  ${PROJECT_INCLUDE_DIR}/backends/imgui_impl_glfw.h 
  ${PROJECT_INCLUDE_DIR}/backends/imgui_impl_opengl3.h
  )

include_directories(${PROJECT_INCLUDE_DIR})
add_library(${PROJECT_NAME} SHARED 
  ${SOURCE_FILES} 
  ${HEADER_FILES} 
  ${MISC_HEADERS}
  ${MISC_SOURCE}
  ${BACKEND_SOURCE_GLFW}
  ${BACKEND_HEADERS_GLFW}
  )

target_include_directories(${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${PROJECT_INCLUDE_DIR}>
                                           PUBLIC $<BUILD_INTERFACE:${PROJECT_INCLUDE_DIR}>)
target_link_directories(${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${CMAKE_LIBRARY_OUTPUT_DIRECTORY}>)

get_property(dirs DIRECTORY ${CMAKE_CURRENT_LIST_DIR} PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
  message(STATUS "dir='${dir}'")
endforeach()
