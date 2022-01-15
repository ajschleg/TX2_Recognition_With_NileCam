# require CMake 2.8 or greater
cmake_minimum_required(VERSION 2.8)

# declare my-recognition project
project(imagenet-camera)

# import jetson-inference and jetson-utils packages.
# note that if you didn't do "sudo make install"
# while building jetson-inference, this will error.
find_package(jetson-utils)
find_package(jetson-inference)

# CUDA and Qt4 are required
find_package(CUDA)
find_package(Qt4)

# setup Qt4 for build
include(${QT_USE_FILE})
add_definitions(${QT_DEFINITIONS})

# include header
include_directories(${PROJECT_SOURCE_DIR})
include_directories(/usr/local/include/jetson-inference)
include_directories(/usr/local/include/jetson-utils)
include_directories(/usr/include/gstreamer-1.0 /usr/lib/aarch64-linux-gnu/gstreamer-1.0/include /usr/include/glib-2.0 /usr/include/libxml2 /usr/lib/aarch64-linux-gnu/glib-2.0/include/)

file(GLOB imagenetCameraSources *.cpp)
file(GLOB imagenetCameraIncludes *.h )

cuda_add_executable(imagenet-camera ${imagenetCameraSources})

target_link_libraries(imagenet-camera jetson-inference)

install(TARGETS imagenet-camera DESTINATION bin)
