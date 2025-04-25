cmake_minimum_required(VERSION 3.31)
project(mcaviewer)

set(CMAKE_CXX_STANDARD 20)

include(FetchContent)

FetchContent_Declare(SDL2
    GIT_REPOSITORY https://github.com/libsdl-org/SDL
    GIT_TAG release-2.32.4
    GIT_PROGRESS TRUE
    GIT_SHALLOW TRUE
)
FetchContent_MakeAvailable(SDL2)

add_executable(mcaviewer WIN32 main.c
    cave_main.c
    cave_mesher.c
    cave_parse.c
    cave_render.c
)
target_include_directories(mcaviewer PRIVATE include)
target_link_libraries(mcaviewer SDL2-static opengl32 glu32)
add_custom_command(TARGET mcaviewer POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory "${CMAKE_CURRENT_SOURCE_DIR}/assets" "${CMAKE_CURRENT_BINARY_DIR}/"
)