cmake_minimum_required(VERSION 3.0)

project (ci-tools-example C)

    add_executable(example ${CMAKE_SOURCE_DIR}/source/example.c)
    add_test(example example)

    if(DEFINED ENV{CI})
        set_target_properties(example PROPERTIES COMPILE_FLAGS $ENV{CI_CC_FLAGS} LINK_FLAGS $ENV{CI_LD_FLAGS})
    endif()