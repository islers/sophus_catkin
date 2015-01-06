cmake_minimum_required(VERSION 2.8.3)
project(sophus_catkin)
SET(CMAKE_BUILD_TYPE Release)

IF (CMAKE_COMPILER_IS_GNUCXX )
   SET(CMAKE_CXX_FLAGS_DEBUG  "-O0 -g")
   SET(CMAKE_CXX_FLAGS_RELEASE "-O3 -DNDEBUG ")

  ADD_DEFINITIONS("-Wall -Werror -Wno-unused-local-typedefs -Wno-unused-variable
                   -Wno-unused-but-set-variable -Wno-unknown-pragmas ")
ENDIF()

find_package(catkin REQUIRED COMPONENTS eigen_catkin)

catkin_package(
 INCLUDE_DIRS sophus
 LIBRARIES sophus
 CATKIN_DEPENDS eigen_catkin
 DEPENDS 
)

SET (SOURCE_DIR "sophus")
SET (CLASSES  sophus/so2
              sophus/se2
              sophus/se3
              sophus/so3
              sophus/scso3
              sophus/sim3
)

SET (SOURCES)

FOREACH(class ${CLASSES})
  LIST(APPEND SOURCES ${SOURCE_DIR}/${class}.cpp ${SOURCE_DIR}/${class}.h)
ENDFOREACH(class)

INCLUDE_DIRECTORIES(
  ${catkin_INCLUDE_DIRS}
)
ADD_LIBRARY(sophus SHARED ${SOURCES})