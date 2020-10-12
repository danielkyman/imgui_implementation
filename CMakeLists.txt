# CMakeList.txt : CMake project for imgui_dev, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("imgui_dev" VERSION 0.1)
message("Project Name: " ${CMAKE_PROJECT_NAME})

find_package(OpenGL REQUIRED)

SET (PROGRAMS-PREFIX "c:/dev")

add_library("glad" "${PROGRAMS-PREFIX}/glad/src/glad.c")
find_library(GLFW glfw3 PATHS "${PROGRAMS-PREFIX}/glfw-3.3.2.bin.WIN64/glfw-3.3.2.bin.WIN64/lib-vc2019")

include_directories(
	"${PROGRAMS-PREFIX}/glad/include"
	"${PROGRAMS-PREFIX}/glfw-3.3.2.bin.WIN64/glfw-3.3.2.bin.WIN64/include"
)

set(
	sources
    main.cpp
    functions.cpp
	imgui/imconfig.h
    imgui/imgui_demo.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_impl_glfw.cpp
    imgui/imgui_impl_glfw.h
    imgui/imgui_impl_opengl3.cpp
    imgui/imgui_impl_opengl3.h
    imgui/imgui_internal.h
    imgui/imgui_widgets.cpp
    imgui/imgui.cpp
    imgui/imgui.h
    imgui/imstb_rectpack.h
    imgui/imstb_textedit.h
    imgui/imstb_truetype.h

)
# Add source to this project's executable.
add_executable (${CMAKE_PROJECT_NAME} ${sources})

target_link_libraries(
    ${CMAKE_PROJECT_NAME}
    ${OPENGL_gl_LIBRARY}
    "glad"
    ${GLFW}
)

add_custom_command(
    TARGET ${CMAKE_PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
            ${CMAKE_SOURCE_DIR}/verdana.ttf
            ${CMAKE_CURRENT_BINARY_DIR}/verdana.ttf
)

# TODO: Add tests and install targets if needed.

