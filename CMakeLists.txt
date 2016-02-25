cmake_minimum_required(VERSION 3.0)

project (ci-tools-example C)

    add_executable(example ${CMAKE_SOURCE_DIR}/source/example.c)

    if(CI_TESTS)
        add_test(example example)
    endif()

    if(MSVC)
        set(CC_FLAGS "/W4 /WX ${CI_CC_FLAGS}")
    else()
        set(CC_FLAGS "-Wall -Wextra -Werror -Wshadow ${CI_CC_FLAGS}")
    endif()
    
    if(DEFINED ENV{CI})
        set_target_properties(example PROPERTIES COMPILE_FLAGS ${CC_FLAGS})
    endif()