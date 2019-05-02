cmake_minimum_required(VERSION 2.8.12)
project(roscpp_initializer)

find_package(catkin REQUIRED roscpp)
find_package(Boost REQUIRED COMPONENTS system filesystem python)
find_package(PythonLibs 2.7 REQUIRED)

catkin_python_setup() 

catkin_package()

include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
  ${PYTHON_INCLUDE_DIRS}
)

add_library(roscpp_initializer SHARED
  src/roscpp_initializer.cpp)

set_target_properties(roscpp_initializer PROPERTIES
  PREFIX ""
  LIBRARY_OUTPUT_DIRECTORY ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_PYTHON_DESTINATION}
)

target_link_libraries(roscpp_initializer
  ${catkin_LIBRARIES}
  ${Boost_LIBRARIES}
  ${PYTHON_LIBRARIES}
)

install(TARGETS roscpp_initializer
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_PYTHON_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_PYTHON_DESTINATION}
)

