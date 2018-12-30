cmake_minimum_required(VERSION 3.6)
project(insaned)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

find_library(LIB_SANE sane REQUIRED)

set(SOURCE_FILES
    src/insaned.cpp
    src/InsaneDaemon.cpp
    src/InsaneException.cpp
    src/Timer.cpp)

add_executable(insaned ${SOURCE_FILES})
target_link_libraries(insaned sane)

install(TARGETS insaned RUNTIME DESTINATION bin)
install(DIRECTORY events/
        DESTINATION ${CMAKE_INSTALL_PREFIX}/etc/insaned.d
        PATTERN "events/*"
        PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
                    GROUP_EXECUTE GROUP_READ)