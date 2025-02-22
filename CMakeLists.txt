cmake_minimum_required(VERSION 3.16..3.30)

project(
    MyFooProject
    VERSION 0.1.0
    LANGUAGES CXX
)

add_executable(my_foo example.cpp)

list(PREPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
set(ENV{CPM_SOURCE_CACHE} "${PROJECT_SOURCE_DIR}/.cpmcache")
include(CPM)

add_subdirectory(dependencies EXCLUDE_FROM_ALL SYSTEM)

set_target_properties(my_foo PROPERTIES
    CXX_STANDARD 20
)

target_compile_definitions(my_foo PRIVATE
    FMT_HEADER_ONLY
)

target_compile_options(my_foo PRIVATE
    -fsized-deallocation
    $<$<CXX_COMPILER_ID:Clang>:-Wno-c++11-narrowing>
    $<$<CXX_COMPILER_ID:Clang>:-Wno-deprecated-this-capture>
    $<$<CXX_COMPILER_ID:GNU>:-Wno-narrowing>
    $<$<CXX_COMPILER_ID:GNU>:-Wno-deprecated>
)

target_include_directories(my_foo PRIVATE
    # tt_metal APIs
    $ENV{TT_METAL_HOME}/tt_metal/api/
    $ENV{TT_METAL_HOME}/tt_metal/hostdevcommon/api

    # UMD
    $ENV{TT_METAL_HOME}/tt_metal/third_party/umd/device/api/

    # Tracy
    $ENV{TT_METAL_HOME}/tt_metal/third_party/tracy/public/
)

target_link_directories(my_foo PRIVATE
    $ENV{TT_METAL_HOME}/build/lib
)

target_link_libraries(my_foo PRIVATE
    magic_enum
    Reflect::Reflect
    nlohmann_json::nlohmann_json
    tt_metal
)
