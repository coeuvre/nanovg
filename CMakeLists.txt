cmake_minimum_required(VERSION 3.0)
project(nanovg)

file(GLOB NANOVG_SOURCE src/*.c)
add_library(nanovg ${NANOVG_SOURCE})
target_compile_definitions(nanovg PUBLIC
        _CRT_SECURE_NO_WARNINGS
        $<$<CONFIG:Debug>:DEBUG>
        $<$<CONFIG:Release>:NDEBUG>)

find_package(glfw3 REQUIRED)
find_package(OpenGL REQUIRED)

add_executable(example_gl3 example/example_gl3.c example/demo.c example/perf.c)
target_include_directories(example_gl3 PUBLIC src example)
target_link_libraries(example_gl3 nanovg)
target_link_libraries(example_gl3 glfw ${OPENGL_LIBRARIES})
target_compile_definitions(example_gl3 PUBLIC
        _CRT_SECURE_NO_WARNINGS
        $<$<CONFIG:Debug>:DEBUG>
        $<$<CONFIG:Release>:NDEBUG>)
