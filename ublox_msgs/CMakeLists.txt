cmake_minimum_required(VERSION 3.0.2)
project(ublox_msgs)

find_package(catkin REQUIRED COMPONENTS message_generation ublox_serialization std_msgs sensor_msgs)

add_message_files(DIRECTORY msg)
add_message_files(FILES MgaACK.msg)
add_message_files(FILES CfgNAVX5_GET.msg)
generate_messages(DEPENDENCIES std_msgs sensor_msgs)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS message_runtime ublox_serialization std_msgs sensor_msgs)

include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(${ublox_serialization_INCLUDE_DIRS})

add_library(${PROJECT_NAME} src/ublox_msgs.cpp)

add_dependencies(${PROJECT_NAME}
  ${${PROJECT_NAME}_EXPORTED_TARGETS}
  ${catkin_EXPORTED_TARGETS}
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/
  DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  PATTERN ".svn" EXCLUDE
)
