cmake_minimum_required(VERSION 3.0)

project (ci-tools-example C)
    add_executable(example ${CMAKE_SOURCE_DIR}/source/example.c)

    include(CTest)
    if(BUILD_TESTING)
        add_test(example example)
    endif()
    
    set_target_properties(example PROPERTIES POSITION_INDEPENDENT_CODE "True")
    if(DEFINED ENV{CI})
        if(DEFINED CI_FLAGS)
            set_target_properties(example PROPERTIES COMPILE_FLAGS "${CI_FLAGS}" LINK_FLAGS "${CI_FLAGS}")
        endif()  
    endif()