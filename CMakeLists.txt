cmake_minimum_required(VERSION 3.15)
project(test CXX)

find_package(glog REQUIRED)

add_library(test src/test.cpp)
target_include_directories(test PUBLIC include)
target_link_libraries(test PRIVATE glog::glog)

set_target_properties(test PROPERTIES PUBLIC_HEADER "include/test.h")
install(TARGETS test)
