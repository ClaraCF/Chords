cmake_minimum_required(VERSION 3.0.0 FATAL_ERROR)

project(Chords LANGUAGES CXX VERSION 0.0.1)


# Set the CMake Build Type to Release by default
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()


include(src/)
