cmake_minimum_required(VERSION 3.22)

project(imgui)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED true)

add_library(imgui STATIC
    imgui/imgui.cpp
    imgui/imgui_demo.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_tables.cpp
    imgui/imgui_widgets.cpp
    imgui/misc/cpp/imgui_stdlib.cpp
)
target_include_directories(imgui PUBLIC
    imgui
    imgui/misc/cpp
)

install(TARGETS imgui)
file(GLOB IMGUI_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/imgui/*.h")
install(FILES ${IMGUI_HEADERS} DESTINATION include)
install(FILES imgui/misc/cpp/imgui_stdlib.h DESTINATION include)