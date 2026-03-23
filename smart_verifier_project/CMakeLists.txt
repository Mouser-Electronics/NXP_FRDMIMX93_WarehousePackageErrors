cmake_minimum_required(VERSION 3.10)
project(smart_verifier)

set(CMAKE_CXX_STANDARD 17)

# 1. Define Source Files
# Includes the missing logic and GUI files mentioned in the document
file(GLOB_RECURSE SOURCES 
    "src/main.c"
    "src/logistics_verifier.c"
    "src/ui.c"
    "src/events_init.c"
    "src/images.c"
)

add_executable(smart_verifier ${SOURCES})

# 2. Include Directories
# Points to the headers for LVGL and LiteRT
target_include_directories(smart_verifier PRIVATE 
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lvgl
)

# 3. Link Libraries
# Explicitly links the NPU delegate and Graphics engine
target_link_libraries(smart_verifier 
    tensorflow-lite 
    ethosu_delegate   # Critical for NPU Acceleration
    lvgl              # Graphics Engine
    v4l2              # Camera API
    pthread 
    rt 
    dl
)
