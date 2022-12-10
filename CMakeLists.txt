cmake_minimum_required(VERSION 3.8)
project(learnogl LANGUAGES C CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/CMake/Modules/")

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)


set(EXT_SOURCE_DIR "${CMAKE_SOURCE_DIR}/external/src")
set(EXT_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/external/include")
add_library(glad "${EXT_INCLUDE_DIR}/glad/glad.h" "${EXT_SOURCE_DIR}/glad.c")
add_subdirectory("${PROJECT_SOURCE_DIR}/external/glfw-3.3.8")
target_include_directories(glad PUBLIC ${EXT_INCLUDE_DIR})

add_executable(${PROJECT_NAME} "${CMAKE_SOURCE_DIR}/src/main.cpp")

target_link_libraries(
  ${PROJECT_NAME}
  PUBLIC glfw glad
  PRIVATE ${CMAKE_DL_LIBS})
