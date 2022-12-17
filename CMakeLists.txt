cmake_minimum_required(VERSION 3.8)
project(diff_bot_control)

find_package(ament_cmake_auto REQUIRED)

ament_auto_find_build_dependencies()

add_library(${PROJECT_NAME} SHARED src/diff_bot_hardware.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)

ament_target_dependencies(
  ${PROJECT_NAME}
  rclcpp
  hardware_interface
  pluginlib
)

pluginlib_export_plugin_description_file(hardware_interface diff_bot_hardware.xml)

install(
  TARGETS ${PROJECT_NAME}
  DESTINATION lib
)
install(
  DIRECTORY include/
  DESTINATION include
)

ament_export_include_directories(
  include
)

ament_export_libraries(
  ${PROJECT_NAME}
)

ament_export_dependencies(
  hardware_interface
  pluginlib
  rclcpp
  rclcpp_lifecycle
)

ament_auto_package(
  INSTALL_TO_SHARE
  config
  launch
  include
)