cmake_minimum_required(VERSION 2.8.12)
project(HelloWorld)

# add_subdirectory(libs)
add_subdirectory(lib)
add_subdirectory(freetype)
add_subdirectory(harfbuzz)


add_executable(HelloWorld "main.cpp")

target_link_libraries(HelloWorld test-lib)

option(BAZEL_BUILD "Bazel build option" OFF)

if(BAZEL_BUILD) 

    message("BAZEL_BUILD patch")

    if(CMAKE_HOST_SYSTEM_NAME STREQUAL "Windows")
        set_target_properties(test-lib PROPERTIES OUTPUT_NAME "libtest-lib")
    else()
        set_target_properties(test-lib PROPERTIES OUTPUT_NAME "test-lib")
    endif()

    set_target_properties(test-lib PROPERTIES LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

    install(TARGETS test-lib ARCHIVE DESTINATION lib)

    file(GLOB libIncludes
        "lib/include/*.h"
    )
    install(FILES ${libIncludes} DESTINATION include/lib)
endif()


