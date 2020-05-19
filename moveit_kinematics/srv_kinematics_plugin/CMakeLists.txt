set(MOVEIT_LIB_NAME moveit_srv_kinematics_plugin)

add_library(${MOVEIT_LIB_NAME} SHARED src/srv_kinematics_plugin.cpp)
set_target_properties(${MOVEIT_LIB_NAME} PROPERTIES VERSION "${PROJECT_VERSION}")

ament_target_dependencies(${MOVEIT_LIB_NAME}
  rclcpp
  class_loader
  moveit_core
  moveit_msgs
)

install(
  TARGETS ${MOVEIT_LIB_NAME}
  EXPORT export_${PROJECT_NAME}
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY include/ DESTINATION include)