cmake_minimum_required(VERSION 3.9)

project(opengl-playground)

#
#
# Put glfw3 directory and glad directory to the same directory as opengl-playground
#
#

# Turn on the ability to create folders to organize projects (.vcproj)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Command to output information to the console
message ("cxx Flags:" ${CMAKE_CXX_FLAGS})

file(COPY ../glad/src/glad.c DESTINATION ../)

file(GLOB sources
	"*.h"
	"*.cpp"
	"*.c"
)

add_executable(opengl-demo ${sources})

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory(../glfw-3.3 _build-glfw-3.3)

target_link_libraries(opengl-demo _build-glfw-3.3/src/Debug/glfw3)

find_package(OpenGL REQUIRED)

target_include_directories(opengl-demo PUBLIC ${OPENGL_INCLUDE_DIR})
target_link_libraries(opengl-demo ${OPENGL_gl_LIBRARY})

include_directories(../glfw-3.3/include)
include_directories(../glad/include)

