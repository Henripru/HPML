cmake_minimum_required(VERSION 3.30)

add_executable(project1 main.cpp)

add_definitions(-DWITHOUT_NUMPY=true)

target_include_directories(project1
    PRIVATE
    ${CMAKE_BINARY_DIR}/_deps/matplotlib-cpp-src/)

target_link_libraries(project1
    PRIVATE
        nonparametric
        Eigen3::Eigen
        matplotlib_cpp
)

target_compile_features(project1 PRIVATE cxx_std_17)

# Install rules
include(GNUInstallDirs)
install(TARGETS project1
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)