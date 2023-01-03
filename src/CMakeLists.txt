# PkgConfig to find libraries on Unix systems
if(NOT WIN32)
    # This will throw an error and exit if PkgConfig
    # is not installed in the user's computer
    find_package(PkgConfig REQUIRED)
endif()


# SFML Library
# We are only going to be using the Graphics and Audio
# Version 2.5
# This will throw an error if SFML is not installed
find_package(SFML 2.5 COMPONENTS graphics audio REQUIRED)


set(PROJECT_HEADERS
    #${CMAKE_SOURCE_DIR}/include
)

set(PROJECT_SOURCES
    ${CMAKE_SOURCE_DIR}/src/main.cpp
)


# Target binary
add_executable(${PROJECT_NAME} ${PROJECT_HEADERS} ${PROJECT_SOURCES})

# Add a version string
target_compile_definitions(${PROJECT_NAME} PRIVATE "VERSION=\"${PROJECT_VERSION}-alpha\"")

# Configure CXX properties
set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)

# Add additional flags for performance to Release build type
if(CMAKE_BUILD_TYPE EQUAL "Release")
    target_compile_options(${PROJECT_NAME} PUBLIC "-march=native -mtune=native -O3 -pipe")
    target_link_libraries(${PROJECT_NAME} PUBLIC "-march=native -mtune=native -O3 -pipe -s")
endif()


# Link SFML and add its Include Dirs
target_include_directories(${PROJECT_NAME} PUBLIC ${SFML_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PUBLIC optimized ${SFML_LIBRARIES})
