cmake_minimum_required(VERSION 3.22)

project(imgui_example)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED true)

find_program(TEX3DS NAMES tex3ds REQUIRED)

execute_process(
    COMMAND ${TEX3DS} -o "${CMAKE_CURRENT_SOURCE_DIR}/romfs/gfx/test.t3x" -i "${CMAKE_CURRENT_SOURCE_DIR}/gfx/test.t3s"
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

set(APP_NAME "imgui_example")
set(APP_DESC "ImGui 3ds Example using v1.89")
set(APP_AUTHOR "npid7")
set(APP_ICON "${CMAKE_CURRENT_SOURCE_DIR}/app/icon.png")
set(APP_ROMFS "${CMAKE_CURRENT_SOURCE_DIR}/romfs")

add_executable(imgui_example
    source/main.cpp
)
target_link_libraries(imgui_example PRIVATE
    m
    z
    ctru
    citro3d
    imgui
    imgui-ctr
)

# Generate 3DSX
ctr_generate_smdh(
    ${CMAKE_BINARY_DIR}/${PROJECT_NAME}.smdh
    NAME "${APP_NAME}"
    DESCRIPTION "${APP_DESC}"
    AUTHOR "${APP_AUTHOR}"
    ICON "${APP_ICON}"
)
ctr_create_3dsx(
    ${PROJECT_NAME}
    OUTPUT "${CMAKE_BINARY_DIR}/${PROJECT_NAME}.3dsx"
    SMDH "${CMAKE_BINARY_DIR}/${PROJECT_NAME}.smdh"
    ROMFS "${APP_ROMFS}"
    DEPENDS create_resources
)