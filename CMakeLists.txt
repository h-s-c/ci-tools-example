cmake_minimum_required(VERSION 3.0)

project (ci-tools-example C)
    add_executable(example ${CMAKE_SOURCE_DIR}/source/example.c)

    include(CTest)
    if(BUILD_TESTING)
        add_test(example example)
    endif()
    
    if(DEFINED ENV{CI})
        if(DEFINED CI_CC_FLAGS)
            set_target_properties(example PROPERTIES COMPILE_FLAGS "${CI_CC_FLAGS}")
        endif() 
        if(DEFINED CI_LD_FLAGS)
            set_target_properties(example PROPERTIES LINK_FLAGS "${CI_LD_FLAGS}")
        endif()      
    endif()