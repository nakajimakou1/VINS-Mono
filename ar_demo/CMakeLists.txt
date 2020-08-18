cmake_minimum_required(VERSION 2.8.3)
project(ar_demo)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++11 -DEIGEN_DONT_PARALLELIZE")
#-DEIGEN_USE_MKL_ALL")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  image_transport
  sensor_msgs
  cv_bridge  # 2020.08.18 uncomment  https://stackoverflow.com/questions/43577496/build-error-undefined-reference-to-cv-bridgecvimagetoimagemsg-const/43577676
  message_filters
  camera_model
)

set(cv_bridge_DIR /opt/ros/melodic/share/cv_bridge/cmake)
find_package(cv_bridge REQUIRED)
find_package(OpenCV REQUIRED)
# find_package(OpenCV 3.4.1 REQUIRED)

catkin_package(

)


include_directories(
  ${catkin_INCLUDE_DIRS}
)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
find_package(Eigen3)
include_directories(
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
)

add_executable(ar_demo_node src/ar_demo_node.cpp)

 target_link_libraries(ar_demo_node
   ${catkin_LIBRARIES} ${OpenCV_LIBS}
 )


