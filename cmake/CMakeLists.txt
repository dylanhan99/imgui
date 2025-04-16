cmake_minimum_version(VERSION 3.8)
project(imgui_docking)
set(TARGET imgui)

set(IMGUI_CMAKE_DIR
	"${CMAKE_CURRENT_LIST_DIR}"
	CACHE STRING
	"Directory containing imgui cmake files. Must be absolute."	
)

set(IMGUI_SOURCES_DIR
	"${IMGUI_CMAKE_DIR}/../"
	CACHE_STRING
	"Directory containing imgui headers and source files. Must be absolute."
)

mark_as_advanced(IMGUI_CMAKE_DIR) # Probably don't need this

file(GLOB IM_SOURCES_0 CONFIGURE_DEPENDS "${IMGUI_SOURCES_DIR}/*.cpp")
file(GLOB IM_SOURCES_1 CONFIGURE_DEPENDS "${IMGUI_SOURCES_DIR}/backends/imgui_impl_opengl3.cpp")

list(REMOVE_ITEM IM_SOURCES_0 "${IMGUI_SOURCES_DIR}/imgui_demo.*")
set(IMGUI_REQ_SOURCES ${IM_SOURCES_0} ${IM_SOURCES_1})

add_library(${TARGET} STATIC "${IMGUI_REQ_SOURCES}")

target_include_directories(${TARGET} 
	PUBLIC "${IMGUI_SOURCES_DIR}"
)
