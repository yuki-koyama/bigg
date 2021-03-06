# This is free and unencumbered software released into the public domain. 

cmake_minimum_required( VERSION 3.0 )
project( bigg )
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_subdirectory( deps )
include( deps/bgfx.cmake/cmake/util/ConfigureDebugging.cmake )
add_library( bigg STATIC src/bigg.cpp src/bigg_assets.h src/bigg_imgui.hpp src/bigg_shaders.hpp include/bigg.hpp )
target_link_libraries( bigg PUBLIC bgfx imgui glfw glm )
target_include_directories( bigg PUBLIC include )

option( BIGG_EXAMPLES "Build examples." ON )
if( BIGG_EXAMPLES )
	add_subdirectory( examples )
endif()

option( BIGG_ASSET_GEN "Generate binary assets." OFF )
if( BIGG_ASSET_GEN )
	add_subdirectory( assets/gen )
endif()
