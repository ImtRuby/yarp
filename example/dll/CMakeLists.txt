# Copyright (C) 2006-2018 Istituto Italiano di Tecnologia (IIT)
# All rights reserved.
#
# This software may be modified and distributed under the terms of the
# BSD-3-Clause license. See the accompanying LICENSE file for details.

cmake_minimum_required(VERSION 3.5)

find_package(YARP REQUIRED)

include_directories(${CMAKE_SOURCE_DIR})

add_library(hello SHARED Hello.cpp Hello.h)
target_link_libraries(hello ${YARP_LIBRARIES})

add_executable(program program.cpp)
target_link_libraries(program ${YARP_LIBRARIES})
