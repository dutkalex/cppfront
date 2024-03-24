cmake_minimum_required( VERSION 3.23 )
project( CPPFRONT LANGUAGES CXX )

set( CMAKE_CXX_STANDARD 20 )
set( CMAKE_CXX_STANDARD_REQUIRED ON )
set( CMAKE_CXX_EXTENSIONS OFF )

set( CPPFRONT_ROOT ${CMAKE_CURRENT_LIST_DIR} )
add_executable( cppfront ${CPPFRONT_ROOT}/source/cppfront.cpp )

# add_custom_command(
#     OUTPUT main.cpp
#     COMMAND cppfront ${CMAKE_CURRENT_LIST_DIR}/main.cpp2 -o main.cpp
#     DEPENDS cppfront
#     VERBATIM
# )
# add_executable( main main.cpp )
# target_include_directories( main PRIVATE ${CMAKE_CURRENT_LIST_DIR}/tpls/cppfront/include )