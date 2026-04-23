cmake_minimum_required(VERSION 3.10)
project(MaLib1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

add_library(MaLib1 SHARED src/lib1.cpp)
target_include_directories(MaLib1 PUBLIC include)

install(TARGETS MaLib1 DESTINATION lib)
install(FILES include/lib1.h DESTINATION include)
