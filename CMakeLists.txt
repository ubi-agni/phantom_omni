cmake_minimum_required(VERSION 2.8.3)
project(phantom_omni)

find_package(catkin REQUIRED COMPONENTS roscpp std_msgs geometry_msgs genmsg rosconsole tf urdf)

add_message_files(FILES PhantomButtonEvent.msg OmniFeedback.msg)

generate_messages(DEPENDENCIES geometry_msgs)

catkin_package(CATKIN_DEPENDS roscpp std_msgs geometry_msgs genmsg rosconsole tf urdf)

include_directories(${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})

add_executable(omni src/omni.cpp)
add_dependencies(omni ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(omni HD HDU rt ncurses ${catkin_LIBRARIES})


# Mark executables and/or libraries for installation
install(TARGETS omni 
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch cfg 
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)


