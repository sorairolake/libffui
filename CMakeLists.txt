cmake_minimum_required(VERSION 3.28)

set(OUT_NAME ffui_app)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(RAPIDFUZZ_INSTALL ON)
# set(FFUI_SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/src)


project(
  ffui
  VERSION 1.0
  LANGUAGES CXX)


include(FetchContent)

find_package(Curses REQUIRED)
include_directories(${CURSES_INCLUDE_DIR})
include_directories(src)

FetchContent_Declare(rapidfuzz
  GIT_REPOSITORY https://github.com/rapidfuzz/rapidfuzz-cpp.git
  GIT_TAG main)
FetchContent_MakeAvailable(rapidfuzz)


add_executable(${OUT_NAME} src/main.cpp src/ffui.cpp)

# add_executable(appc src/main.c src/ffui.cpp)

target_link_libraries(${OUT_NAME} PRIVATE rapidfuzz::rapidfuzz)
target_link_libraries(${OUT_NAME} PRIVATE ${CURSES_LIBRARY})

# target_link_libraries(appc PRIVATE rapidfuzz::rapidfuzz)
# target_link_libraries(appc PRIVATE ${CURSES_LIBRARY})

add_library(ffui STATIC
    src/ffui.cpp
)

target_link_libraries(ffui PUBLIC rapidfuzz::rapidfuzz)
target_link_libraries(ffui PRIVATE ${CURSES_LIBRARY})
