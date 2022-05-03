# version 3.11 or later of CMake needed later for installing GoogleTest
# so let's require it now.
cmake_minimum_required( VERSION 3.11 )

project( main_project
         VERSION 0.1
         DESCRIPTION "Main Project" )

set( MAIN_ROOT_SOURCE_DIR ${PROJECT_SOURCE_DIR} )

add_subdirectory( ${PROJECT_SOURCE_DIR}/external/package_manager/conan )  # look in subdirectory for CMakeLists.txt to process

add_subdirectory( ${PROJECT_SOURCE_DIR}/application )  # look in apps subdirectory for CMakeLists.txt to process
