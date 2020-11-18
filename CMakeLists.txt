cmake_minimum_required(VERSION 3.14)

project(
    "ImGui"
    VERSION 1.79
    DESCRIPTION "Dear ImGui: Bloat-free Graphical User interface for C++ with minimal dependencies"
    LANGUAGES CXX)

if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    set_property(GLOBAL PROPERTY USE_FOLDERS ON)
    set_property(GLOBAL PROPERTY PREDEFINED_TARGETS_FOLDER "CMake")
endif()

add_library(imgui STATIC
    backends/imgui_impl_dx11.cpp
    backends/imgui_impl_dx11.h
    backends/imgui_impl_win32.cpp
    backends/imgui_impl_win32.h
    imconfig.h
    imgui.cpp
    imgui.h
    imgui_draw.cpp
    imgui_internal.h
    imgui_widgets.cpp
    imstb_rectpack.h
    imstb_textedit.h
    imgui_demo.cpp)

target_compile_features(imgui PRIVATE cxx_std_17)
target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/backends)

if (MSVC)
	target_compile_options(imgui PRIVATE
		"/MP"                      # Multi-processor compilation
		"$<$<CONFIG:RELEASE>:/MT>" # Non-DLL CRT
		"$<$<CONFIG:DEBUG>:/MTd>"  # Non-DLL CRT
	)
endif()