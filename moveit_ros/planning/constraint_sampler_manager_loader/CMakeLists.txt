set(MOVEIT_LIB_NAME moveit_constraint_sampler_manager_loader)

add_library(${MOVEIT_LIB_NAME} SHARED
    src/constraint_sampler_manager_loader.cpp)

set_target_properties(${MOVEIT_LIB_NAME} PROPERTIES VERSION "${PROJECT_VERSION}")
ament_target_dependencies(${MOVEIT_LIB_NAME}
  moveit_core
  rclcpp
  Boost
  pluginlib
  ament_index_cpp
)
target_link_libraries(${MOVEIT_LIB_NAME}
  moveit_rdf_loader
)

install(TARGETS ${MOVEIT_LIB_NAME}
        EXPORT export_${PROJECT_NAME}
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)
