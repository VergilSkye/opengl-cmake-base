cmake_minimum_required(VERSION 3.11.0)
project(base VERSION 0.1.0)

# Carregando pastas
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libraries")
set(INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")
# Setando o sources que é o arquivo que fica o nosso main, pode ser .cpp
set(SOURCES "${SRC_DIR}/main.c")

# Cdicionando a pasta include, onde os arquivos .h iram ficar
include_directories(${INCLUDE_DIR})

# Cria o execultavel
add_executable(${PROJECT_NAME} ${SOURCES}) # name and folder source from the project

# Encontra o Opengl no sistema
find_package(OpenGL REQUIRED)
# Encontra o GLUT no sistema
find_package(GLUT REQUIRED)
if(NOT ${OPENGL_FOUND})
    message("OPENGL not found")
endif()

# Aadiciona os diretorios do opengl e do glut
include_directories( ${OPENGL_INCLUDE_DIRS}  ${GLUT_INCLUDE_DIRS} )
# faz o link do execultavel com as bibliotecas necessarias 
target_link_libraries(base ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} )

# Coisas do cmake
set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
