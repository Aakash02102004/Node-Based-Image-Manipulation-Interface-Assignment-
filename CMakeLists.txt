set(CMAKE_TOOLCHAIN_FILE "${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "Vcpkg toolchain file")

cmake_minimum_required(VERSION 3.15)
project(ImNodesTest)

set(CMAKE_CXX_STANDARD 17)

# Add ImGui source files
file(GLOB IMGUI_SRC
    libs/imgui/*.cpp
    libs/imgui/backends/imgui_impl_sdl2.cpp
    libs/imgui/backends/imgui_impl_opengl3.cpp
)

# Add ImNodes
file(GLOB IMNODES_SRC
    libs/imnodes/*.cpp
)

add_executable(ImNodesTest main.cpp ${IMGUI_SRC} ${IMNODES_SRC})

target_include_directories(ImNodesTest PRIVATE
    libs/imgui
    libs/imgui/backends
    libs/imnodes
    ${SDL2_INCLUDE_DIRS}
)

find_package(OpenGL REQUIRED)
find_package(SDL2 CONFIG REQUIRED)
target_link_libraries(ImNodesTest PRIVATE SDL2::SDL2 SDL2::SDL2main)

target_link_libraries(ImNodesTest PRIVATE
    OpenGL::GL
    SDL2::SDL2
)
