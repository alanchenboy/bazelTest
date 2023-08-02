cmake_minimum_required(VERSION 2.8.12)


add_library(test-lib STATIC src/lib.cpp)

target_include_directories(test-lib PUBLIC include)
