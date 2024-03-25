cmake_minimum_required( VERSION 3.23 )
project( CPPFRONT LANGUAGES CXX )

set( CMAKE_CXX_STANDARD 20 )
set( CMAKE_CXX_STANDARD_REQUIRED ON )
set( CMAKE_CXX_EXTENSIONS OFF )


set( CPPFRONT_ROOT ${CMAKE_CURRENT_LIST_DIR} CACHE STRING "" )
add_executable( cppfront ${CPPFRONT_ROOT}/source/cppfront.cpp )


function( target_enable_cpp2 target )
    get_property( target_cpp2_sources TARGET "${target}" PROPERTY SOURCES )
    list( FILTER target_cpp2_sources INCLUDE REGEX "\\.cpp2" )

    set( new_sources "" )
    foreach( source IN LISTS target_cpp2_sources )
        get_filename_component( raw_filename ${source} NAME_WE )
        set( cpp1_file "${raw_filename}.cpp" )
        get_filename_component( cpp2_file_with_path ${source} ABSOLUTE )
        add_custom_command(
            OUTPUT "${cpp1_file}"
            COMMAND cppfront "${cpp2_file_with_path}" -o "${cpp1_file}" ${CPPFRONT_FLAGS}
            DEPENDS cppfront
            VERBATIM
        )
        list( APPEND new_sources "${cpp1_file}" )
    endforeach()

    target_sources( ${target} PRIVATE ${new_sources} )
    target_include_directories( ${target} PRIVATE ${CPPFRONT_ROOT}/include )
endfunction()