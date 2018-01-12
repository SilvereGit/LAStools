cmake_minimum_required(VERSION 2.8.3)
project(LAStools)

set(CMAKE_CXX_FLAGS "-pthread -std=c++11 -fPIC -Wall")

#set(CMAKE_CXX_STANDARD 11) # C++11...
#set(CMAKE_CXX_STANDARD_REQUIRED ON) #...is required...
#set(CMAKE_CXX_EXTENSIONS OFF) #...without compiler extensions like gnu++11


# for using SLAM manager
find_package(catkin REQUIRED COMPONENTS
  roscpp
)

# for using all required components of the slam
find_package(catkin REQUIRED COMPONENTS ${PACKAGE_DEPENDENCIES})

#make laslib
#add_custom_command(OUTPUT LASlib/lib/liblas.a
#                   COMMAND make run
#                   WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/LASlib
#)

#catkin_package( LIBRARIES LAStools INCLUDE_DIRS LASlib/inc)
catkin_package(
   INCLUDE_DIRS LASlib/inc LASlib/src
#  LIBRARIES vectornav
   CATKIN_DEPENDS roscpp
#  DEPENDS system_lib
)

###########
## Build ##
###########

#add_subdirectory(LASlib/src)
include_directories(LASlib/inc ${catkin_INCLUDE_DIRS})
include_directories(LASzip/src/ ${catkin_INCLUDE_DIRS})
set(SOURCE
        LASlib/src/lasreader.cpp LASlib/src/laswriter.cpp LASlib/src/lasreader_las.cpp LASlib/src/lasreader_bin.cpp LASlib/src/lasreader_qfit.cpp LASlib/src/lasreader_shp.cpp LASlib/src/lasreader_asc.cpp LASlib/src/lasreader_bil.cpp LASlib/src/lasreader_dtm.cpp LASlib/src/lasreader_txt.cpp LASlib/src/lasreadermerged.cpp LASlib/src/lasreaderbuffered.cpp LASlib/src/lasreaderpipeon.cpp LASlib/src/laswriter_las.cpp LASlib/src/laswriter_bin.cpp LASlib/src/laswriter_qfit.cpp LASlib/src/laswriter_wrl.cpp LASlib/src/laswriter_txt.cpp LASlib/src/laswritercompatible.cpp LASlib/src/laswaveform13reader.cpp LASlib/src/laswaveform13writer.cpp LASlib/src/lasutility.cpp LASlib/src/lasfilter.cpp LASlib/src/lastransform.cpp LASlib/src/fopen_compressed.cpp LASlib/inc/laszip.cpp LASlib/inc/lasreadpoint.cpp LASlib/inc/lasreaditemcompressed_v1.cpp LASlib/inc/lasreaditemcompressed_v2.cpp LASlib/inc/lasreaditemcompressed_v3.cpp LASlib/inc/laswritepoint.cpp  LASlib/inc/laswriteitemcompressed_v1.cpp LASlib/inc/laswriteitemcompressed_v2.cpp LASlib/inc/laswriteitemcompressed_v3.cpp LASlib/inc/integercompressor.cpp LASlib/inc/arithmeticdecoder.cpp LASlib/inc/arithmeticencoder.cpp LASlib/inc/arithmeticmodel.cpp LASlib/inc/lasindex.cpp LASlib/inc/lasquadtree.cpp LASlib/inc/lasinterval.cpp)

#include_directories(
#    include)

add_library(liblas ${SOURCE})


## Specify additional locations of header files
## Your package locations should be listed before other locations

#link_directories(vnproglib-1.1/cpp/build/bin)

## Declare a cpp library
## Declare a cpp executable
#add_library(liblas LASlib/src/lasreader.cpp LASlib/src/laswriter.cpp LASlib/src/lasreader_las.cpp LASlib/src/lasreader_bin.cpp LASlib/src/lasreader_qfit.cpp LASlib/src/lasreader_shp.cpp LASlib/src/lasreader_asc.cpp LASlib/src/lasreader_bil.cpp LASlib/src/lasreader_dtm.cpp LASlib/src/lasreader_txt.cpp LASlib/src/lasreadermerged.cpp LASlib/src/lasreaderbuffered.cpp LASlib/src/lasreaderpipeon.cpp LASlib/src/laswriter_las.cpp LASlib/src/laswriter_bin.cpp LASlib/src/laswriter_qfit.cpp LASlib/src/laswriter_wrl.cpp LASlib/src/laswriter_txt.cpp LASlib/src/laswritercompatible.cpp LASlib/src/laswaveform13reader.cpp LASlib/src/laswaveform13writer.cpp LASlib/src/lasutility.cpp LASlib/src/lasfilter.cpp LASlib/src/lastransform.cpp LASlib/src/fopen_compressed.cpp)

## Specify libraries to link a library or executable target against
#target_link_libraries(liblas
#  vncxx
#  ${catkin_LIBRARIES}
#)


## Uncomment if the package has a setup.py
#catkin_python_setup()

#######################################
## Declare ROS messages and services ##
#######################################

# Generate messages in the 'msg' folder
#add_message_files(
#   FILES
#   SequoiaMsg.msg
#)

## Generate added messages and services with any dependencies listed here
#generate_messages(
#  DEPENDENCIES
#  std_msgs 
#)

#catkin_package(
#  CATKIN_DEPENDS
#    ${PACKAGE_DEPENDENCIES} sensor_msgs
#  DEPENDS message_runtime
#  INCLUDE_DIRS "."
#  LIBRARIES ${PROJECT_NAME}
#)



#############
## Install ##
#############

install(DIRECTORY LASlib/inc DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
#install(TARGETS LASzip/src/mydefs.hpp DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
#install(DIRECTORY LASlib/lib DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})

install(PROGRAMS
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(TARGETS liblas
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
