set(MOVEIT_LIB_NAME moveit_planning_pipeline)

add_library(${MOVEIT_LIB_NAME} SHARED src/planning_pipeline.cpp)
set_target_properties(${MOVEIT_LIB_NAME} PROPERTIES VERSION "${PROJECT_VERSION}")

ament_target_dependencies(${MOVEIT_LIB_NAME}
  rclcpp
  Boost
  pluginlib
  moveit_core)

install(TARGETS ${MOVEIT_LIB_NAME}
  EXPORT export_${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)
