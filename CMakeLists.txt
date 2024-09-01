cmake_minimum_required(VERSION 3.30)

# Read version from YAML file
file(READ "${CMAKE_CURRENT_SOURCE_DIR}/version.yaml" VERSION_YAML)
string(REGEX MATCH "major: ([0-9]+)" _ ${VERSION_YAML})
set(VERSION_MAJOR ${CMAKE_MATCH_1})
string(REGEX MATCH "minor: ([0-9]+)" _ ${VERSION_YAML})
set(VERSION_MINOR ${CMAKE_MATCH_1})
string(REGEX MATCH "patch: ([0-9]+)" _ ${VERSION_YAML})
set(VERSION_PATCH ${CMAKE_MATCH_1})

project(hpml
    VERSION ${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_PATCH}
    LANGUAGES CXX)

# Output version information
message(STATUS "Project version: ${PROJECT_VERSION}")

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Options
option(BUILD_TESTS "Build the tests" ON)
option(WITHOUT_NUMPY "Build matplotlib-cpp without NumPy support" ON)

# Include third-party dependencies
add_subdirectory(third_party)

# Function to add a library and its test
function(add_ml_library LIB_NAME)
    add_subdirectory(libraries/${LIB_NAME})
    if(BUILD_TESTS)
        add_subdirectory(libraries/${LIB_NAME}/tests)
    endif()
endfunction()

# Add libraries
add_ml_library(nonparametric)
#add_ml_library(neural_network)

# Add applications
add_subdirectory(projects/project1)
#add_subdirectory(projects/project2)

# Enable testing
if(BUILD_TESTS)
    enable_testing()
endif()