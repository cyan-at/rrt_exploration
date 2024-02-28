cmake_minimum_required(VERSION 3.8)
project(rrt_exploration)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(visualization_msgs REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
    "msg/PointArray.msg"
    DEPENDENCIES std_msgs geometry_msgs
)


# set(SOURCES 
#   src/powerboard.cpp
#   src/usb_com.cpp
# )

include_directories(
  include/
  ${rclcpp_INCLUDE_DIRS}
  ${rrt_exploration_INCLUDE_DIRS}
)

add_executable(local_rrt_detector src/local_rrt_detector.cpp src/functions.cpp src/mtrand.cpp)
ament_target_dependencies(local_rrt_detector rclcpp sensor_msgs std_msgs)
install(TARGETS
  local_rrt_detector
  DESTINATION lib/${PROJECT_NAME})

add_executable(global_rrt_detector src/global_rrt_detector.cpp src/functions.cpp src/mtrand.cpp)
ament_target_dependencies(global_rrt_detector rclcpp sensor_msgs std_msgs)
install(TARGETS
  global_rrt_detector
  DESTINATION lib/${PROJECT_NAME})


# install(
#     DIRECTORY launch
#     DESTINATION share/${PROJECT_NAME}
# )



ament_package()

# catkin_package( 

# CATKIN_DEPENDS message_runtime
# )





# include_directories(include ${catkin_INCLUDE_DIRS})

# add_executable(global_rrt_detector src/global_rrt_detector.cpp src/functions.cpp src/mtrand.cpp)
# target_link_libraries(global_rrt_detector ${catkin_LIBRARIES})

# add_executable(local_rrt_detector src/local_rrt_detector.cpp src/functions.cpp src/mtrand.cpp)
# target_link_libraries(local_rrt_detector ${catkin_LIBRARIES})
