cmake_minimum_required(VERSION 3.3)
project(CSE167)

## pkg-config
find_package(PkgConfig REQUIRED)
find_package (OpenGL REQUIRED)
if (APPLE)
    find_library(COCOA_LIBRARY Cocoa REQUIRED)
    find_library(IOKIT_LIBRARY IOKit REQUIRED)
    find_library(COREVID_LIBRARY CoreVideo REQUIRED)
endif (APPLE)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILES
    Cube.cpp
    Cube.h
    main.cpp
    main.h
    OBJObject.cpp
    OBJObject.h
    Window.cpp
    Window.h)

set(RASTERIZER
    Rasterizer.cpp)




## GLFW
pkg_search_module(GLFW REQUIRED glfw3)
#include_directories(${GLFW_INCLUDE_DIRS})
#link_libraries(${GLFW_LIBRARIES})

## GLEW
find_package(GLEW REQUIRED)
#include_directories(${GLEW_INCLUDE_DIRS})
#link_libraries(${GLEW_LIBRARIES})


## GLM
find_package(GLM REQUIRED)
#include_directories(${GLM_INCLUDE_DIRS})
#link_libraries(${GLM_LIBRARIES})


set(LIBS  ${GLFW_LIBRARIES}
        ${OPENGL_LIBRARIES}
        ${GLEW_LIBRARY}
        ${COCOA_LIBRARY} ${COREVID_LIBRARY} ${IOKIT_LIBRARY})


add_executable(MAIN ${SOURCE_FILES})
target_link_libraries (MAIN ${LIBS})

add_executable(Rasterizer ${RASTERIZER})
target_link_libraries(Rasterizer ${LIBS})