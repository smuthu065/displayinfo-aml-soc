cmake_minimum_required(VERSION 3.3)

# Project Name
project(DeviceInfoSoc)

# Set Library Name
set(LIB_NAME DeviceinfoSoc)

# Set C++ Standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add Include Directories
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# Source Files
set(SRC_FILES
    DeviceSettings/Amlogic/SoC_abstraction.cpp
    DeviceSettings/Amlogic/kms.c
)

# Create Shared Library
add_library(${LIB_NAME} SHARED ${SRC_FILES})

# Set Library Output Name
set_target_properties(${LIB_NAME} PROPERTIES OUTPUT_NAME "DeviceinfoSoc")

# Link Required Libraries (if any)
target_link_libraries(${LIB_NAME}
    PRIVATE
    drm   # DRM Library for Linux graphics backend
)

# Install Library
install(TARGETS ${LIB_NAME}
    DESTINATION lib
)

message("Library ${LIB_NAME} built successfully")
