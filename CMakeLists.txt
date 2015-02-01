cmake_minimum_required(VERSION 2.4.6)
project(qbo_self_recognizer)

set(opencv_DIR /usr/share/OpenCV)

find_package(OpenCV REQUIRED)

find_package(catkin REQUIRED COMPONENTS
 roscpp
 cv_bridge
 sensor_msgs
 image_transport
 qbo_arduqbo 
)
#include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)


#set the default path for built executables to the "bin" directory
#set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
#set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
add_service_files(FILES QboRecognize.srv) 
generate_messages()

catkin_package()

include_directories(  ${catkin_INCLUDE_DIRS}  ${OpenCV_INCLUDE_DIRS} )

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#target_link_libraries(example ${PROJECT_NAME})
add_executable(qbo_detector_node src/qbo_detector.cpp)

target_link_libraries(qbo_detector_node ${OpenCV_LIBRARIES} ${catkin_LIBRARIES})
