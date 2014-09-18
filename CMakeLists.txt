cmake_minimum_required(VERSION 2.8)
project(object_recognition_ros_visualization)

find_package(catkin REQUIRED cmake_modules geometric_shapes geometry_msgs object_recognition_ros
                             object_recognition_msgs pluginlib rosbag roscpp rviz sensor_msgs tf
                             visualization_msgs
)
catkin_package()

# build some cells
include_directories(SYSTEM ${catkin_INCLUDE_DIRS})

find_package(Boost REQUIRED system filesystem serialization)

add_subdirectory(src)

# add docs
ecto_sphinx(${CMAKE_CURRENT_SOURCE_DIR}/doc/source doc)

# install
install(FILES ork_rviz_plugin.xml
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
