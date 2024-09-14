cmake_minimum_required(VERSION 3.29)
project(cmpct VERSION 0.1.0)
set(CMAKE_CXX_STANDARD 20)

# --- INCLUDE DEPENDENCIES ---
include(cmake/pkg.cmake)

# --- LIB ---
file(GLOB_RECURSE cmpct-files src/*.cpp)
add_library(cmpct-library ${cmpct-files})
target_include_directories(cmpct-library PUBLIC include)
target_compile_features(cmpct-library PUBLIC cxx_std_20)

# --- APPLICATION ---
file(GLOB_RECURSE cmpct-app-files app/main.cpp)
add_executable(cmpct ${cmpct-app-files})
target_link_libraries(cmpct PRIVATE cmpct-library)
target_compile_features(cmpct PUBLIC cxx_std_20)

# --- TEST ---
file(GLOB_RECURSE cmpct-test-files test/*.cpp)
add_executable(cmpct-test ${cmpct-test-files})
target_include_directories(cmpct-test PRIVATE include)
target_link_libraries(cmpct-test gtest cmpct-library)