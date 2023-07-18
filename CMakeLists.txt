cmake_minimum_required(VERSION 3.12)
project(opengl-starter)

# Set C++ version
set(CMAKE_CXX_STANDARD 20)

add_subdirectory(glfw)
add_subdirectory(glm)
add_subdirectory(assimp)
add_subdirectory(glad)

# Find packages
find_package(OpenGL REQUIRED)

# Set include directories
include_directories(
    glfw/include
    glm/glm
    assimp/include
    imgui
    imgui/backends
)

set(SOURCES
    src/main.cpp
)

# Add executable
add_executable(${CMAKE_PROJECT_NAME} ${SOURCES})

# Link libraries
target_link_libraries(${CMAKE_PROJECT_NAME}
    glfw
    glm
    assimp
    glad
    ${OPENGL_LIBRARIES}
)

# Add Dear ImGui
add_library(imgui
    imgui/imgui.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_widgets.cpp
    imgui/imgui_demo.cpp
    imgui/backends/imgui_impl_glfw.cpp
    imgui/backends/imgui_impl_opengl3.cpp
)

target_include_directories(imgui PUBLIC imgui)
target_link_libraries(${CMAKE_PROJECT_NAME} imgui)
