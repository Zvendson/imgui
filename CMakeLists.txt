cmake_minimum_required(VERSION 3.16)

project(imgui LANGUAGES CXX)

option(USE_GLFW   "Adds imgui GLFW backends" OFF)
option(USE_SDL3   "Adds imgui SDL3 backends" OFF)
option(USE_VULKAN "Adds imgui vulkan backends" OFF)

file(GLOB SOURCES_IMGUI
    "imgui.h"
    "imgui_internal.h"
    "imgui.cpp"
    "imgui_demo.cpp"
    "imgui_draw.cpp"
    "imgui_tables.cpp"
    "imgui_widgets.cpp"
    "backends/imgui_impl_dx*.h"
    "backends/imgui_impl_dx*.cpp"
    "backends/imgui_impl_win32.h"
    "backends/imgui_impl_win32.cpp"
)

add_library(imgui ${SOURCES_IMGUI})

target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

if(USE_GLFW)
    target_sources(imgui PUBLIC
    "backends/imgui_impl_glfw.h"
    "backends/imgui_impl_glfw.cpp"
    )
endif()

if(USE_SDL3)
    target_sources(imgui PUBLIC
    "backends/imgui_impl_sdl3.h"
    "backends/imgui_impl_sdl3.cpp"
    )
endif()

if(USE_VULKAN)
    target_sources(imgui PUBLIC
        "backends/imgui_impl_vulkan.h"
        "backends/imgui_impl_vulkan.cpp"
    )
endif()