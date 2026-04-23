cmake_minimum_required(VERSION 3.10)
project(MaLib1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

add_library(MaLib1 SHARED src/lib1.cpp)
target_include_directories(MaLib1 PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

install(TARGETS MaLib1 
    EXPORT MaLib1Targets
    DESTINATION lib
    INCLUDES DESTINATION include
)

install(FILES include/lib1.h DESTINATION include)

install(EXPORT MaLib1Targets
    FILE MaLib1Config.cmake
    DESTINATION lib/cmake/MaLib1
)
