cmake_minimum_required(VERSION 3.10.2)
project(moveit_kinematics VERSION 2.0.0)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_EXTENSIONS OFF)

if(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

find_package(ament_cmake REQUIRED)

find_package(Boost REQUIRED program_options system)
find_package(Eigen3 REQUIRED)
find_package(orocos_kdl REQUIRED)
find_package(tf2_kdl REQUIRED)
find_package(kdl_parser REQUIRED)
find_package(rclcpp REQUIRED)
find_package(random_numbers REQUIRED)
find_package(class_loader REQUIRED)
find_package(pluginlib REQUIRED)
find_package(moveit_core REQUIRED)
find_package(moveit_ros_planning REQUIRED)
find_package(moveit_msgs REQUIRED)

set(THIS_PACKAGE_INCLUDE_DIRS
    kdl_kinematics_plugin/include
    lma_kinematics_plugin/include
    srv_kinematics_plugin/include
    cached_ik_kinematics_plugin/include
)

pluginlib_export_plugin_description_file(moveit_core kdl_kinematics_plugin_description.xml)
pluginlib_export_plugin_description_file(moveit_core lma_kinematics_plugin_description.xml)
pluginlib_export_plugin_description_file(moveit_core srv_kinematics_plugin_description.xml)

include_directories(${THIS_PACKAGE_INCLUDE_DIRS})

add_subdirectory(kdl_kinematics_plugin)
add_subdirectory(lma_kinematics_plugin)
add_subdirectory(srv_kinematics_plugin)
# add_subdirectory(ikfast_kinematics_plugin)
# add_subdirectory(cached_ik_kinematics_plugin)
add_subdirectory(test)

ament_export_interfaces(export_${PROJECT_NAME} HAS_LIBRARY_TARGET)
ament_export_libraries(
    moveit_kdl_kinematics_plugin
    moveit_lma_kinematics_plugin
    moveit_srv_kinematics_plugin)
ament_export_include_directories(include)
ament_export_dependencies(pluginlib)
ament_export_dependencies(moveit_core)
ament_export_dependencies(moveit_ros_planning)
ament_export_dependencies(Boost)
ament_package()
