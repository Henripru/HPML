cmake_minimum_required(VERSION 3.30)

add_library(nonparametric
    source/knn.cpp
    source/utils.cpp
)

target_include_directories(nonparametric
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/source
)

# Link against Eigen
target_link_libraries(nonparametric PUBLIC Eigen3::Eigen)

# Specify C++ standard for this library
target_compile_features(nonparametric PUBLIC cxx_std_17)

# Install rules
include(GNUInstallDirs)
install(TARGETS nonparametric
    EXPORT NonparametricTargets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# Generate and install export file
install(EXPORT NonparametricTargets
    FILE NonparametricTargets.cmake
    NAMESPACE HPML::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/Nonparametric
)