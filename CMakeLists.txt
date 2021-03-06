cmake_minimum_required(VERSION 2.8.3)
project(roscv)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS cv_bridge image_transport roscpp sensor_msgs std_msgs tf message_generation genmsg pcl pcl_ros)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/groovy/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

#######################################
## Declare ROS messages and services ##
#######################################

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )
add_message_files(
  DIRECTORY
  msg	
  FILES
  ObjectSize.msg
  ObjectPosition.msg
  ObjectPose.msg
)


## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs
# )

generate_messages(
  DEPENDENCIES geometry_msgs
)

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
   INCLUDE_DIRS include
#  LIBRARIES roscv
#  CATKIN_DEPENDS cv_bridge image_transport opencv2 roscpp sensor-msgs std_msgs
   CATKIN_DEPENDS message_runtime
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(include
  ${catkin_INCLUDE_DIRS}
)

## Declare a cpp library
# add_library(roscv
#   src/${PROJECT_NAME}/roscv.cpp
# )

## Declare a cpp executable
# add_executable(roscv_node src/roscv_node.cpp)

## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodCMakeFiles/subtractBackground.dir/src/subtractBackground.cpp.o:es
# add_dependencies(roscv_node roscv_generate_messages_cpp)

## Specify libraries to link a library or executable target against
# target_link_libraries(roscv_node
#   ${catkin_LIBRARIES}
# )

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/groovy/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS roscv roscv_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_roscv.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()
add_executable( simplecanny src/simplecanny.cpp)
target_link_libraries( simplecanny ${catkin_LIBRARIES})
add_dependencies( simplecanny roscv_gencpp)

add_executable( boundingBox src/boundingBox.cpp)
target_link_libraries( boundingBox ${catkin_LIBRARIES})
add_dependencies( boundingBox roscv_gencpp)

add_executable( captureBackground src/captureBackground.cpp)
target_link_libraries( captureBackground ${catkin_LIBRARIES})
add_dependencies( captureBackground roscv_gencpp)

#add_executable( subtractBackground src/subtractBackground.cpp)
#target_link_libraries( subtractBackground ${caclustertkin_LIBRARIES})
#add_dependencies(subtractBackground roscv_gencpp)

add_executable( computeObjectPose src/computeObjectPose.cpp)
target_link_libraries( computeObjectPose ${catkin_LIBRARIES})
add_dependencies(computeObjectPose roscv_gencpp)

add_executable( computeObjectPoseusing2D src/computeObjectPoseusing2D.cpp)
target_link_libraries( computeObjectPoseusing2D ${catkin_LIBRARIES})
add_dependencies(computeObjectPoseusing2D roscv_gencpp)

add_executable( readTransform src/readTransform.cpp)
target_link_libraries( readTransform ${catkin_LIBRARIES})
add_dependencies(readTransform roscv_gencpp)

add_executable( simpleSubscriber src/simpleSubscriber.cpp)
target_link_libraries( simpleSubscriber ${catkin_LIBRARIES})
add_dependencies(simpleSubscriber roscv_gencpp)

add_executable( advancedCaptureBackground src/advancedCaptureBackground.cpp)
target_link_libraries( advancedCaptureBackground ${catkin_LIBRARIES})
add_dependencies(advancedCaptureBackground roscv_gencpp)

add_executable( advancedSubtractBackground src/advancedSubtractBackground.cpp)
target_link_libraries( advancedSubtractBackground ${catkin_LIBRARIES})
add_dependencies(advancedSubtractBackground roscv_gencpp)

add_executable( pcd_write src/pcd_write.cpp)
target_link_libraries( pcd_write ${catkin_LIBRARIES})
add_dependencies(pcd_write roscv_gencpp)

add_executable( passFilter src/passFilter.cpp)
target_link_libraries( passFilter ${catkin_LIBRARIES})
add_dependencies(passFilter roscv_gencpp)

add_executable( range_image_border_extraction src/range_image_border_extraction.cpp)
target_link_libraries( range_image_border_extraction ${catkin_LIBRARIES} libvtkCommon.so  libvtkFiltering.so)
add_dependencies(range_image_border_extraction roscv_gencpp)

add_executable( depthSubtractBackground src/depthSubtractBackground.cpp)
target_link_libraries( depthSubtractBackground ${catkin_LIBRARIES})
add_dependencies(depthSubtractBackground roscv_gencpp)

add_executable( gaussianSubtractBackground src/gaussianSubtractBackground.cpp)
target_link_libraries( gaussianSubtractBackground ${catkin_LIBRARIES})
add_dependencies(gaussianSubtractBackground roscv_gencpp)
## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
# add_dependencies( roscv roscv_gencpp)
#rosbuild_genmsg()
