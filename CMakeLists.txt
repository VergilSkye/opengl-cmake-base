cmake_minimum_required(VERSION 3.11.0)
project(base VERSION 0.1.0)

# Source Files
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libraries")
set(INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")
set(SOURCES "${SRC_DIR}/main.c")

#add headers on include, this is the place to put .h files
include_directories(${INCLUDE_DIR})
add_executable(${PROJECT_NAME} ${SOURCES}) # name and folder source from the project

find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
if(NOT ${OPENGL_FOUND})
    message("OPENGL not found")
endif()

include_directories( ${OPENGL_INCLUDE_DIRS}  ${GLUT_INCLUDE_DIRS} )
target_link_libraries(base ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} )

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
