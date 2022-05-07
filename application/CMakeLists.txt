# version 3.11 or later of CMake or needed later for installing GoogleTest
# so let's require it now.
cmake_minimum_required( VERSION 3.11-3.12 )

project( main )

set( CMAKE_FIND_LIBRARY_SUFFIXES ".a" ) # <--- Change the preference to .a and not .so/.dll
set( CMAKE_EXE_LINKER_FLAGS "-static" ) # <-- full static executable. Get segmentation fault
#set( CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++" ) # <-- Partial static executable. It is work
#set( CMAKE_EXE_LINKER_FLAGS "-fsanitize=address" ) # <-- active the address sanitizer in development

file( GLOB_RECURSE SOURCES "src/main_01.cpp" )

add_executable( ${PROJECT_NAME} ${SOURCES} )

# ***************** Conan Integration ***************

#Full static link fix pthare segmentation fail
# https://github.com/sewenew/redis-plus-plus/issues/356
# https://stackoverflow.com/questions/9002264/starting-a-stdthread-with-static-linking-causes-segmentation-fault
target_link_libraries( ${PROJECT_NAME} PRIVATE -Wl,--whole-archive pthread -Wl,--no-whole-archive PACKAGE_MANAGER_CONAN_LIBS )

# ***************** Conan Integration ***************

# Tell C++ compiler to use C++20 features. We don't actually use any of them.
target_compile_features( ${PROJECT_NAME} PUBLIC cxx_std_20 )
