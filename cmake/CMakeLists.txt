cmake_minimum_required(VERSION 3.8)
project(imgui_docking)

set(IMGUI_CMAKE_DIR
    "${CMAKE_CURRENT_LIST_DIR}"
    CACHE STRING
    "Path to cmake files. Must be absolute."
)
set(IMGUI_SOURCE_DIR
    "${IMGUI_CMAKE_DIR}/../"
    CACHE STRING
    "Path to source files. Must be absolute."
)
#file(REAL_PATH "${IMGUI_CMAKE_DIR}/../" IMGUI_SOURCE_DIR)
mark_as_advanced(IMGUI_CMAKE_DIR)

function(imgui_add_library TARGET)
    target_compile_definitions("${PROJECT_NAME}" 
	    PUBLIC GLFW_INCLUDE_NONE=1
    ) 

    message(STATUS "IMGUI_CMAKE_DIR > ${IMGUI_CMAKE_DIR}")
    message(STATUS "IMGUI_SOURCE_DIR > ${IMGUI_SOURCE_DIR}")

    file(GLOB IM_SOURCES_0 CONFIGURE_DEPENDS
        "${IMGUI_SOURCE_DIR}/*.cpp"
    )
    file(GLOB IM_SOURCES_1 CONFIGURE_DEPENDS
        "${IMGUI_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp"
        "${IMGUI_SOURCE_DIR}/backends/imgui_impl_glfw.cpp"
    )

    set(IMGUI_REQ_SOURCES ${IM_SOURCES_0} ${IM_SOURCES_1})
    list(REMOVE_ITEM IMGUI_REQ_SOURCES "${IMGUI_SOURCE_DIR}/imgui_demo.*")

    message(STATUS "IMGUI_REQ_SOURCES > ${IMGUI_REQ_SOURCES}")

    add_library(${TARGET} STATIC "${IMGUI_REQ_SOURCES}")
    target_include_directories(${TARGET} 
	    PUBLIC "${IMGUI_SOURCE_DIR}"
	    PUBLIC "${IMGUI_SOURCE_DIR}/backends/"
    )

    target_link_libraries(${TARGET}
	    PRIVATE glfw
    )
endfunction()
