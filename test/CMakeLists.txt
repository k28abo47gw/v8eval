cmake_minimum_required(VERSION 2.8)

project(v8eval-test)

add_executable(v8eval-test
    v8eval_test.cxx
)

set_target_properties(v8eval-test PROPERTIES
    COMPILE_FLAGS "${v8eval-cflags}"
)

set(v8eval-linklibs
    v8eval
    v8_libplatform
    v8_base
    v8_libbase
    v8_libsampler
    v8_init
    v8_initializers
    v8_nosnapshot
    torque_generated_initializers
    gtest
    gtest_main
)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    set(v8eval-linklibs
        ${v8eval-linklibs}
        dl
        rt
        pthread
        c++
        c++abi
    )
endif(CMAKE_SYSTEM_NAME STREQUAL "Linux")

target_link_libraries(v8eval-test
    ${v8eval-linklibs}
)
