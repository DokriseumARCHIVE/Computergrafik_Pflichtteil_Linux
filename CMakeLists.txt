#Please note that this configuration was made by someone who is new to CMake. It can be messy :D
#For this to run you have to copy all provided files into a subdirectory called "ogl" from the root of your project.
#My project name is "CG", if yours is different you have to replace all "CG"s in this file with your project name.

cmake_minimum_required(VERSION 3.17)
project(CG CXX)

#if some of these cause an error you probably have to install it, you can search for it on "pkgs.org"
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(glm REQUIRED)

include_directories(
        ogl/external/glew-1.13.0
        ogl/external/glfw-3.1.2
        ogl/external/glm-0.9.4.0
        .
)

set(ALL_LIBS
        ${OPENGL_LIBRARY}
        glfw
        GLEW
        glm
        )

#copies the needed shader files into the binary directory, you may have to add some later!
configure_file(ogl/TransformVertexShader.vertexshader ${CMAKE_CURRENT_BINARY_DIR}/TransformVertexShader.vertexshader COPYONLY)
configure_file(ogl/ColorFragmentShader.fragmentshader ${CMAKE_CURRENT_BINARY_DIR}/ColorFragmentShader.fragmentshader)

set(CMAKE_CXX_STANDARD 14)

add_executable(CG
        ogl/objects.cpp
        ogl/shader.cpp
        ogl/CGTutorial.cpp
)
target_link_libraries(CG ${ALL_LIBS})