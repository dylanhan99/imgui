cmake_minimum_required(VERSION 3.8)
project(imgui_docking)
set(TARGET imgui)

set(IMGUI_CMAKE_DIR "${CMAKE_CURRENT_LIST_DIR}")
file(REAL_PATH "${IMGUI_CMAKE_DIR}/../" IMGUI_SOURCE_DIR)

file(GLOB IM_SOURCES_0 CONFIGURE_DEPENDS "${IMGUI_SOURCE_DIR}/*.cpp")
file(GLOB IM_SOURCES_1 CONFIGURE_DEPENDS "${IMGUI_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp" "${IMGUI_SOURCE_DIR}/backends/glfw.cpp")

set(IMGUI_REQ_SOURCES ${IM_SOURCES_0} ${IM_SOURCES_1})
list(REMOVE_ITEM IMGUI_REQ_SOURCES "${IMGUI_SOURCE_DIR}/imgui_demo.*")

add_library(${TARGET} STATIC "${IMGUI_REQ_SOURCES}")
target_include_directories(${TARGET} 
	PUBLIC "${IMGUI_SOURCE_DIR}"
	PUBLIC "${IMGUI_SOURCE_DIR}/backends/"
)
