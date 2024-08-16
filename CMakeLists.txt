cmake_minimum_required(VERSION 3.14)

project(HelloRaylib VERSION 0.1.0 LANGUAGES CXX)

include(FetchContent)
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(BUILD_GAMES OFF CACHE BOOL "" FORCE)

FetchContent_Declare(
    raylib
    GIT_REPOSITORY "https://github.com/raysan5/raylib.git"
    GIT_TAG "master"
    GIT_PROGRESS TRUE
)
set(RAYLIB_VERSION 4.5.0)

FetchContent_Declare(
    raylib
    URL https://github.com/raysan5/raylib/archive/refs/tags/${RAYLIB_VERSION}.tar.gz
    FIND_PACKAGE_ARGS ${RAYLIB_VERSION} EXACT
)

FetchContent_MakeAvailable(raylib)

add_executable(HelloRaylib src/main.cpp)

if (MSVC)
    target_compile_options(HelloRaylib PUBLIC /W4)
else()
    target_compile_options(HelloRaylib PUBLIC -Wall -Wextra -Wpedantic)
endif()

set_target_properties(HelloRaylib PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF)

target_link_libraries(HelloRaylib PRIVATE raylib)