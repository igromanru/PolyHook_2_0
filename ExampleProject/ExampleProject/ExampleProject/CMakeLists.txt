﻿# CMakeList.txt : CMake project for ExampleProject, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

# Add source to this project's executable.
add_executable (ExampleProject "ExampleProject.cpp" "ExampleProject.h")

set(PLH_DIR C:/Users/steve/Source/Repos/PolyHook_2_0)

include_directories(${PLH_DIR})

set(PLH_LIB_PATH_64 ${PLH_DIR}/build64)
set(PLH_LIB_PATH_86 ${PLH_DIR}/build32)
set(CAPSTONE_LIB_PATH_64 ${PLH_DIR}/capstone/build64)
set(CAPSTONE_LIB_PATH_86 ${PLH_DIR}/capstone/build32)

target_compile_options(${PROJECT_NAME} PRIVATE /std:c++latest)
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
    # 64 bits
	
	#Link the capstone lib according to config mode
	target_link_libraries(${PROJECT_NAME} debug ${CAPSTONE_LIB_PATH_64}/Debug/capstone.lib)
	target_link_libraries(${PROJECT_NAME} optimized ${CAPSTONE_LIB_PATH_64}/Release/capstone.lib)
	target_link_libraries(${PROJECT_NAME} debug ${PLH_LIB_PATH_64}/Debug/PolyHook_2.lib)
	target_link_libraries(${PROJECT_NAME} optimized ${PLH_LIB_PATH_64}/Release/PolyHook_2.lib)
elseif(CMAKE_SIZEOF_VOID_P EQUAL 4)
    # 32 bits

	#Link the capstone lib according to config mode
	target_link_libraries(${PROJECT_NAME} debug ${CAPSTONE_LIB_PATH_86}/Debug/capstone.lib)
	target_link_libraries(${PROJECT_NAME} optimized ${CAPSTONE_LIB_PATH_86}/Release/capstone.lib)
	target_link_libraries(${PROJECT_NAME} debug ${PLH_LIB_PATH_86}/Debug/PolyHook_2.lib)
	target_link_libraries(${PROJECT_NAME} optimized ${PLH_LIB_PATH_86}/Release/PolyHook_2.lib)
endif()
# TODO: Add tests and install targets if needed.
