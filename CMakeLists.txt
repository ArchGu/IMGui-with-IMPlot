cmake_minimum_required(VERSION 3.11)
 
project(DEMO)

set(CMAKE_CXX_STANDARD 11)


set(GUI_DIR ${PROJECT_SOURCE_DIR}/gui)

include_directories(
  ${GUI_DIR}/imgui-1.90
  ${GUI_DIR}/imgui-1.90/backends
  ${GUI_DIR}/implot-0.16
)

# set common source
file(GLOB SRC
    ./gui/imgui-1.90/*.h
    ./gui/imgui-1.90/*.cpp
)

if (UNIX)
    file (GLOB PLATFORM_SRC
        ./gui/imgui-1.90/backends/imgui_impl_glfw.*
        ./gui/imgui-1.90/backends/imgui_impl_opengl3.*
        ./gui/implot-0.16/*.h
        ./gui/implot-0.16/*.cpp
        ./src/main.cpp
    )
endif()

# generate binary
add_executable(${PROJECT_NAME} ${SRC} ${PLATFORM_SRC})

if (UNIX)
    # linux: sudo apt install libglfw3-dev
    target_link_libraries(${PROJECT_NAME}
        GL
        glfw # use this lib name
        dl
    )
endif()