cmake_minimum_required(VERSION 3.30)

include(FetchContent)

# Eigen
FetchContent_Declare(
    eigen
    GIT_REPOSITORY https://gitlab.com/libeigen/eigen.git
    GIT_TAG        3.4.0
)

# Google Test
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG        v1.15.2
)

# matplotlib-cpp
FetchContent_Declare(
    matplotlib-cpp
    GIT_REPOSITORY https://github.com/lava/matplotlib-cpp.git
    GIT_TAG        ef0383f1315d32e0156335e10b82e90b334f6d9f  # Latest commit as of 9/1/2024
)

# Make the dependencies available
FetchContent_MakeAvailable(eigen googletest matplotlib-cpp)