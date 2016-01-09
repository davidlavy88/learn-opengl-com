# CMake entry point
cmake_minimum_required (VERSION 2.6)
#cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
project (shaders)

set(CMAKE_MODULE_PATH /home/david/Libraries/findGLM)

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

find_package(OpenGL REQUIRED)
include_directories(${OpenGL_INCLUDE_DIRS})
link_directories(${OpenGL_LIBRARY_DIRS})
add_definitions(${OpenGL_DEFINITIONS})

find_package(GLEW REQUIRED)
include_directories(${GLEW_INCLUDE_DIRS})
link_directories(${GLEW_LIBRARY_DIRS})
add_definitions(${GLEW_DEFINITIONS})

find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)
include_directories(${GLFW_INCLUDE_DIRS})

find_package(GLM REQUIRED)
include_directories(${GLM_INCLUDE_DIRS})
link_directories(${GLM_LIBRARY_DIRS})
add_definitions(${GLM_DEFINITIONS})

#########################################################
# Include Files
#########################################################
add_executable(shaders shaders.cpp)
#add_executable(exercise_hellotriangle exercise_helloTriangle.cpp)

target_link_libraries(shaders ${GLFW_STATIC_LIBRARIES} ${GLEW_LIBRARIES} ${OPENGL_LIBRARIES} ${GLM_LIBRARIES})
#target_link_libraries(exercise_hellotriangle ${GLFW_STATIC_LIBRARIES} ${GLEW_LIBRARIES} ${OPENGL_LIBRARIES} ${GLM_LIBRARIES})

#target_compile_features(hellowindow PRIVATE cxx_range_for)

#########################################################
# FIND GLUT
#########################################################
#find_package(GLUT REQUIRED)
#include_directories(${GLUT_INCLUDE_DIRS})
#link_directories(${GLUT_LIBRARY_DIRS})
#add_definitions(${GLUT_DEFINITIONS})
#if(NOT GLUT_FOUND)
#    message(ERROR " GLUT not found!")
#endif(NOT GLUT_FOUND)

## create the program "test"
#  target_link_libraries(test ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} )
