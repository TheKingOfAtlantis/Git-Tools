cmake_minimum_required (VERSION 3.9)

macro(set_option option value)
  set(${option} ${value} CACHE INTERNAL "" FORCE)
endmacro()

project(Git-Tools)

if(MSVC)
	set(MSVC_STD_MODULES [["$(VCToolsInstallDir_150)ifc\$(PlatformTarget)"]])

	set(CXX_WARNING_FLAGS "/Wall")
	set(CXX_MODULE_FLAGS "/std:c++latest /experimental:module /module:interface /module:stdIfcDir ${MSVC_STD_MODULES} /module:search ")
else()
	set(CXX_WARNING_FLAGS "-Wall -Wextra -pedantic")
endif()

add_subdirectory(${CMAKE_SOURCE_DIR}/deps/libgitxx/)

set(LIBGITXX_INCLUDE_DIR ${CMAKE_SOURCE_DIR}/deps/libgitxx/include)
set(LIBGITXX_LIBRARIES gitxx)
set(LIBGITXX_MODULES_DIR ${CMAKE_BINARY_DIR}/deps/libgitxx)
set(LIBGITXX_FOUND 1)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${CXX_WARNING_FLAGS} ${CXX_MODULE_FLAGS} ${LIBGITXX_MODULES_DIR}")
