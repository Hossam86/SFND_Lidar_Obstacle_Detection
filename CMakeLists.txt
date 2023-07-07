cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

add_definitions(-std=c++11)

set(CXX_FLAGS "-Wall")
set(CMAKE_CXX_FLAGS, "${CXX_FLAGS}")

project(playback)

# find_package(PCL 1.2 REQUIRED)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake )

# external dependencies
include(CPM)
set(BUILD_TESTING OFF)
CPMAddPackage(
        NAME Boost
        VERSION 1.81.0
        GITHUB_REPOSITORY "boostorg/boost"
        GIT_TAG "boost-1.81.0"
)
CPMAddPackage(
        NAME Eigen
        GIT_REPOSITORY https://gitlab.com/libeigen/eigen
        GIT_TAG 3.4
)
CPMAddPackage(
        NAME flann
        GIT_REPOSITORY git@github.com:flann-lib/flann.git
        GIT_TAG 1.8.5
)
CPMAddPackage(
        NAME cminpack
        GIT_REPOSITORY git@github.com:devernay/cminpack.git
        GIT_TAG v1.3.6
)
CPMAddPackage(
  NAME pcl
  GIT_REPOSITORY git@github.com:PointCloudLibrary/pcl.git
  GIT_TAG pcl-1.2
)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
list(REMOVE_ITEM PCL_LIBRARIES "vtkproj4")


add_executable (environment src/environment.cpp src/render/render.cpp src/processPointClouds.cpp)
target_link_libraries (environment ${PCL_LIBRARIES})




