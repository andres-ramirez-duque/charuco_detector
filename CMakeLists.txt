cmake_minimum_required(VERSION 2.8.3)
project(charuco_detector)


#######################################################################################################################
## flags
#######################################################################################################################

set(${PROJECT_NAME}_CATKIN_COMPONENTS
    cv_bridge
    geometry_msgs
    image_transport
    rosconsole
    roscpp
    rostime
    sensor_msgs
    tf2
    tf2_ros
)


#######################################################################################################################
## packages
#######################################################################################################################

find_package(catkin REQUIRED COMPONENTS ${${PROJECT_NAME}_CATKIN_COMPONENTS})
find_package(OpenCV REQUIRED)
find_package(Eigen3 REQUIRED)


#######################################################################################################################
## catkin specific configuration
#######################################################################################################################

catkin_package(
    INCLUDE_DIRS
        include
    LIBRARIES
        charuco_detector
    CATKIN_DEPENDS
        ${${PROJECT_NAME}_CATKIN_COMPONENTS}
    DEPENDS
        OpenCV
        EIGEN3
)


#######################################################################################################################
## build
#######################################################################################################################

add_definitions(-std=c++11)

#==============================================================================
# includes
#==============================================================================

include_directories(
    include
    ${catkin_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${EIGEN3_INCLUDE_DIR}
)


#==============================================================================
# libraries
#==============================================================================

add_library(charuco_detector
    src/charuco_detector.cpp
    src/aruco/apriltag_quad_thresh.cpp
    src/aruco/aruco.cpp
    src/aruco/charuco.cpp
    src/aruco/dictionary.cpp
    src/aruco/zmaxheap.cpp
)


#==============================================================================
# executables
#==============================================================================

add_executable(charuco_detector_node
    src/charuco_detector_node.cpp
)


#==============================================================================
# library link
#==============================================================================

target_link_libraries(charuco_detector
    ${catkin_LIBRARIES}
    ${OpenCV_LIBS}
)


#==============================================================================
# executables link
#==============================================================================

target_link_libraries(charuco_detector_node
    charuco_detector
    ${catkin_LIBRARIES}
)
