cmake_minimum_required(VERSION 3.16..3.30)

project(
    MyFooProject
    VERSION 0.1.0
    LANGUAGES CXX
)

add_executable(my_foo example.cpp)

set_target_properties(my_foo PROPERTIES
    CXX_STANDARD 20
)

target_include_directories(my_foo PRIVATE
    # for including reflect
    /usr/local/include/metalium-thirdparty
)

target_link_directories(my_foo PRIVATE
    # for libtt_metal.so
    /usr/local/lib
)

target_compile_definitions(my_foo PRIVATE
    # use the fmt lib that comes with the system
    # so you dont have to use CPM spdlog dependency, thats messy...
    SPDLOG_FMT_EXTERNAL
)

target_link_libraries(my_foo PRIVATE
    fmt
    tt_metal
)
