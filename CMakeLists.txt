cmake_minimum_required(VERSION 3.3)

# Project Name
project(DisplayInfoSoc)

# Set Library Name
set(LIB_NAME displayinfosoc)

# Set C++ Standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")

find_package(LibDRM REQUIRED)
find_path (STAGING_INCDIR glib-2.0)
include_directories(include)
include_directories(${STAGING_INCDIR})
include_directories(${STAGING_INCDIR}/libdrm)

# Add Include Directories
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# Source Files
set(SRC_FILES
    SoC_abstraction.cpp
    kms.c
)

# Create Shared Library
add_library(${LIB_NAME} SHARED ${SRC_FILES})

# Set Library Output Name
set_target_properties(${LIB_NAME} PROPERTIES OUTPUT_NAME "displayinfosoc")

# Link Required Libraries (if any)
target_link_libraries(${LIB_NAME}
    PRIVATE
    drm   # DRM Library for Linux graphics backend
)

message("Library ${LIB_NAME} built successfully")
